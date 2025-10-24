---
name: zotero-mcp
description: Interface with Zotero's MCP server to search and retrieve bibliographic data using advanced semantic search and multi-strategy approaches. Use this skill when the user needs to search their Zotero library for papers, citations, or references using comprehensive multi-angle search strategies.
---

# Zotero MCP Search Skill

Interface with Zotero's MCP server to search and retrieve bibliographic data using advanced semantic search and multi-strategy approaches.

## Core Philosophy

**Search comprehensively, not narrowly.** Never settle for a single search attempt. Always:
- Use semantic search for conceptual discovery
- Try multiple search angles and variations
- Combine different search methods
- Iteratively refine based on results
- Ask clarifying questions when needed

## ⚠️ CRITICAL: Avoiding Claude Desktop Crashes ⚠️

**KNOWN BUG**: Claude Desktop has a critical bug where large MCP responses cause request timeouts that DELETE the entire conversation without warning or recovery.

### Safe Search Strategy: Batched Iteration

To get comprehensive results safely, use **iterative batched searches**:

**✅ SAFE: Multiple small searches**
- Each search limited to 10-15 results maximum
- Multiple searches with different angles/filters
- Combine results across searches

**❌ UNSAFE: Single large search**
- limit=50 or higher in one call
- Risks conversation deletion
- No recovery possible

### Recommended Approaches

#### Approach 1: Multi-Angle Coverage (Preferred)
Instead of one search with limit=50, do **5 searches** with different angles:
```
1. Semantic search: "main concept" (limit=10)
2. Semantic search: "related concept variation" (limit=10)
3. Keyword search: "specific terms" (limit=10)
4. Tag-based search: relevant tags (limit=10)
5. Notes/annotations search: "concept" (limit=10)
```
This gives ~50 results from different perspectives, safer than one large call.

#### Approach 2: Agent-Based Batched Search
For complex searches needing many results:
```
1. Launch agent with Task tool
2. Agent performs multiple limit=10 searches
3. Agent synthesizes and prioritizes results
4. Agent returns curated summary (not raw data dump)
```

#### Approach 3: Iterative Interactive
For user-guided exploration:
```
1. First batch: limit=10
2. Present results
3. Ask: "Would you like more results, or shall I search from a different angle?"
4. Next batch based on user feedback
```

### Default Limits

**Always use these safe defaults:**
- `limit=10` for initial searches
- `limit=15` if user explicitly needs more
- **Never exceed limit=20** in a single call
- For comprehensive results: use multiple searches, not larger limits

## Search Strategy Framework

### 1. Initial Query Analysis

Before searching, analyze what the user is looking for:
- **Conceptual queries** (theories, approaches, themes) → Start with semantic search
- **Specific items** (author, title, year) → Start with keyword/advanced search
- **Exploratory queries** ("What do I have about...") → Use multi-method approach
- **Vague queries** → Ask clarifying questions first

### 2. Multi-Method Search Approach

**ALWAYS use multiple search methods in combination:**

#### A. Semantic Search (Primary for Conceptual Discovery)
- Use `zotero_semantic_search` for conceptual, thematic, or exploratory queries
- Try multiple phrasings of the same concept
- Use natural language descriptions, not just keywords
- Example variations:
  - "theories of embodied cognition"
  - "how body influences thought and reasoning"
  - "physical experience shapes cognitive processes"

#### B. Keyword Search (Complementary)
- Use `zotero_search_items` with multiple keyword variations
- Try synonyms, related terms, broader/narrower terms
- Use different word forms (singular/plural, verb/noun)
- Example variations for "reading comprehension":
  - "reading comprehension"
  - "text understanding"
  - "literacy"
  - "comprehension strategies"

#### C. Advanced Search (Targeted)
- Use `zotero_advanced_search` for precise criteria
- Combine multiple fields (author + keyword, year + tag)
- Use for filtering after broader searches

#### D. Tag & Collection Filtering
- Use `zotero_get_tags` to discover relevant tags
- Use `zotero_search_by_tag` with multiple tag variations
- Use `zotero_get_collections` and `zotero_get_collection_items` for organized searches

#### E. Full-Text & Annotations
- Use `zotero_search_notes` to search annotations and highlights
- Use `zotero_get_item_fulltext` for content not in metadata
- Critical for finding concepts mentioned in text but not in titles/abstracts

### 3. Iterative Refinement Process

**Never stop at first results.** Follow this workflow:

```
1. Initial Search (semantic + keyword)
   ↓
2. Analyze Results
   - Too many? Add filters (tags, date, collection)
   - Too few? Broaden terms, try synonyms
   - Wrong direction? Refine concept
   ↓
3. Second Round (refined terms + complementary methods)
   ↓
4. Cross-Check (full-text, annotations, related tags)
   ↓
5. Present Results (with search path explanation)
```

### 4. Required Search Variations

For ANY user query, try AT MINIMUM:

- **3 semantic search variations** (different phrasings)
- **3 keyword variations** (synonyms, related terms)
- **1 tag search** (check tags first, then search)
- **1 full-text/annotation search** (if applicable)

## Specific Tool Usage Guidelines

### zotero_semantic_search
**Use for:** Conceptual discovery, theme exploration, finding related work
**Strategies:**
- Try query as natural question: "What causes skill transfer?"
- Try query as descriptive phrase: "factors influencing skill transfer between contexts"
- Try query with synonyms: "skill generalization determinants"
- **SAFETY**: Always use `limit=10` (max 15-20 for critical needs)
- **For comprehensive results**: Use multiple searches with different phrasings, NOT larger limits

### zotero_search_items
**Use for:** Keyword matching, author/title searches
**Strategies:**
- Try multiple keyword combinations
- Use partial matches (author last name only)
- Combine with date ranges if too many results

### zotero_advanced_search
**Use for:** Precise filtering, combining criteria
**Strategies:**
- Start broad, then narrow with additional conditions
- Combine author + keyword for specific works
- Use itemType to filter by publication type

### zotero_search_notes & zotero_get_annotations
**Use for:** Finding your own thoughts, highlighted concepts
**Strategies:**
- Search for concepts you annotate but might not be in titles
- Look for methodology terms in annotations
- Check for cited authors mentioned in your notes

### zotero_get_tags
**Always check tags** before searching to discover:
- User's tagging conventions
- Related tags to search
- Collection organization patterns

## Common Search Patterns

### Pattern 1: "Find me papers about X" (Safe Comprehensive Search)
```
OPTION A: Multi-angle (do all searches yourself)
1. zotero_semantic_search: "X" (limit=10)
2. zotero_semantic_search: "X alternative phrasing" (limit=10)
3. zotero_search_items: keyword variations of X (limit=10)
4. zotero_get_tags: look for X-related tags
5. zotero_search_by_tag: if relevant tags found (limit=10)
6. zotero_search_notes: "X" (limit=10)
Result: ~50+ results safely retrieved

OPTION B: Agent-based (for complex searches)
1. Launch agent with Task tool
2. Agent prompt: "Search my Zotero library for papers about X using multiple approaches.
   For each search use limit=10. Try: semantic search variations, keyword searches,
   tag-based searches, and note searches. Synthesize the most relevant 20-30 results."
3. Agent performs batched searches and returns curated results
```

### Pattern 2: "What do I have on [author]?"
```
1. zotero_search_items: author="[Author]"
2. zotero_advanced_search: author + recent years
3. zotero_search_notes: "[Author]" (citations in notes)
4. zotero_semantic_search: "[Author]'s main concepts"
```

### Pattern 3: "Research about X in context Y"
```
1. zotero_semantic_search: "X in Y" + variations
2. zotero_advanced_search: keyword=X AND keyword=Y
3. zotero_get_tags: check for X-tags and Y-tags
4. zotero_search_notes: "X" + "Y" separately
5. Cross-reference results
```

### Pattern 4: "Exploratory: What's related to X?"
```
1. zotero_semantic_search: multiple conceptual phrasings
2. Get tags from initial results
3. Search by related tags found
4. Search notes/annotations with related concepts
5. Present thematic clusters found
```

## Search Failure Recovery

If initial searches yield poor results:

1. **Ask clarifying questions:**
   - "Are you looking for theoretical or empirical work?"
   - "Any specific time period or authors?"
   - "Is this about methodology, findings, or theory?"

2. **Broaden search:**
   - Use more general terms
   - Remove filters
   - Try related fields/disciplines

3. **Check search database status:**
   - Use `zotero_get_search_database_status`
   - Suggest `zotero_update_search_database` if outdated

4. **Try alternative angles:**
   - If searching for method, search for problems it solves
   - If searching for theory, search for phenomena it explains
   - If searching for author, search for concepts they study

## Using Agents for Complex Searches

### When to Use Agents

Use the Task tool to launch an agent when:
- User needs comprehensive results (30+ papers)
- Search requires multiple different strategies
- You want to combine, deduplicate, and synthesize results
- User wants a curated list rather than raw search results

### How to Structure Agent Tasks

**Good agent prompt structure:**
```
Search my Zotero library for [topic]. Use multiple search strategies:

1. Semantic search with 3-4 different phrasings (limit=10 each)
2. Keyword searches with variations (limit=10 each)
3. Tag-based searches if relevant tags exist (limit=10 each)
4. Note/annotation searches (limit=10)

IMPORTANT: Use limit=10 for all searches to avoid crashes.

Combine all results, remove duplicates, and return the 25 most relevant papers
with brief explanations of why each is relevant.
```

### Agent Safety Guidelines

**Tell agents:**
- Always use limit=10 (max 15) for individual searches
- Perform multiple small searches rather than large ones
- Synthesize and prioritize results
- Return curated findings, not raw data dumps

**Agent benefits:**
- Can perform many searches autonomously
- Combines and deduplicates results
- Provides synthesis and prioritization
- Safer than single large searches

## Presentation Guidelines (Brief)

When presenting results:
- Explain what search strategies you used
- Show why you chose those strategies
- Note if results were refined/filtered
- Suggest related searches if appropriate

**Save detailed presentation preferences for later discussion.**

## Critical Reminders

- **Never use just one search method**
- **Never try just one search term variation**
- **Always check tags before searching**
- **Always search both metadata and full-text/annotations**
- **Always explain your search path**
- **Always refine based on initial results**
- **🚨 SAFETY: Always use limit=10 (max 15-20) to prevent conversation deletion**
- **🚨 SAFETY: For comprehensive results, use multiple searches or agents, NOT large limits**

## Tool Quick Reference

| Tool | Primary Use | When to Use | Safe Limit |
|------|-------------|-------------|------------|
| `zotero_semantic_search` | Conceptual discovery | Themes, theories, exploratory queries | limit=10 |
| `zotero_search_items` | Keyword matching | Authors, specific terms, titles | limit=10 |
| `zotero_advanced_search` | Precise filtering | Multiple criteria, narrow searches | limit=10 |
| `zotero_get_tags` | Discover tags | ALWAYS before tag-based searches | No limit needed |
| `zotero_search_by_tag` | Tag filtering | After discovering relevant tags | limit=10 |
| `zotero_search_notes` | Annotation search | User's thoughts, cited concepts | limit=10 |
| `zotero_get_annotations` | Highlight retrieval | Finding highlighted passages | limit=10 |
| `zotero_get_item_fulltext` | Full-text access | Verify content, detailed review | N/A (single item) |
| `zotero_get_collections` | Collection discovery | Understanding library organization | No limit needed |
| `zotero_get_recent` | Recent additions | "What did I add lately?" | limit=10 |

---

**Remember:**
- **Comprehensive, multi-angle, iterative searching is MANDATORY, not optional**
- **Safety limits are CRITICAL to prevent conversation deletion**
- **For comprehensive results: Use multiple limit=10 searches, NOT one large search**
- **Consider using agents (Task tool) for complex multi-search operations**
