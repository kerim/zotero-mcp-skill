# Zotero MCP Search Skill for Claude

A comprehensive, **context-aware** skill that enables advanced, multi-strategy searching of your Zotero library through the Zotero MCP (Model Context Protocol) server. Works intelligently in both **Claude Desktop** and **Claude Code**.

## What This Is

This is a **universal Claude skill** that teaches Claude how to search your Zotero reference library intelligently and comprehensively, adapting to the environment:

- **In Claude Code:** Uses autonomous agents for comprehensive multi-step searches
- **In Claude Desktop:** Uses safe batched searches with conversation crash protection

Instead of simple one-off searches, Claude learns to:

- Use **semantic/AI-powered search** to find conceptually related papers
- Try **multiple search angles** with different phrasings and synonyms
- **Combine search methods** (semantic + keyword + tags + full-text + annotations)
- **Iteratively refine** searches based on results
- **Ask clarifying questions** when your query is ambiguous
- **Adapt strategy** based on environment (agents in Code, batching in Desktop)

## Why This Skill Exists

### The Problem

The Zotero MCP server provides powerful semantic search capabilities, but using it effectively requires:
- Understanding multiple search strategies (semantic vs. keyword vs. tag-based)
- Knowing when to use each search method
- Trying multiple variations and phrasings
- Searching across metadata, full-text, notes, and annotations
- **Claude Desktop:** Avoiding response limits that can crash conversations
- **Claude Code:** Leveraging agents for autonomous comprehensive searches

Without guidance, Claude might:
- Use only one search method and miss relevant papers
- Try only one search phrase and return incomplete results
- **In Desktop:** Request too many results at once (causing crashes)
- **In Code:** Not utilize agents for complex multi-step searches
- Not explore alternative search angles

### The Solution

This skill provides Claude with:
- **Environment detection** - Automatically detects Claude Code vs Claude Desktop
- **Mandatory multi-angle search strategies** (minimum 3 semantic + 3 keyword variations)
- **Safe batching guidelines** for Desktop (limit=10 per search to prevent crashes)
- **Agent-based patterns** for Code (comprehensive autonomous searches)
- **Comprehensive search patterns** combining multiple methods
- **Iterative refinement workflows** to improve results
- **Bibliography formatting** for Logseq with Chinese/English translation support

## Features

### Core Capabilities

- **Context-Aware Operation:** Detects environment and adapts search strategy
  - **Claude Code:** Launches autonomous agents for multi-step comprehensive searches
  - **Claude Desktop:** Uses safe batched searches with crash protection
- **Semantic-First Discovery:** AI-powered conceptual search to find related work
- **Multi-Strategy Search:** Combines semantic, keyword, tag-based, and full-text methods
- **Iterative Refinement:** Analyzes initial results and refines search strategy
- **Safety-First Design:** Built-in protections against Claude Desktop crash bugs
- **Comprehensive Coverage:** Searches metadata, full-text PDFs, annotations, and notes
- **Logseq Integration:** Formats bibliographies for Logseq with proper outline hierarchy
- **Translation Support:** Handles Chinese-English bilingual content

### Search Methods Taught

1. **Semantic Search** - Conceptual similarity using AI embeddings
2. **Keyword Search** - Traditional text matching with variations
3. **Advanced Search** - Multi-criteria filtering (author + keyword + year)
4. **Tag Search** - Leverage your existing Zotero tags
5. **Full-Text Search** - Search within PDF contents
6. **Annotation Search** - Find your highlights and notes
7. **Collection Search** - Navigate your Zotero collections

### Environment-Specific Features

#### Claude Code
- **Agent-Based Searches:** Autonomous multi-step search execution
- **No Limit Restrictions:** Can retrieve comprehensive results safely
- **Parallel Searches:** Multiple search strategies executed simultaneously
- **Intelligent Synthesis:** Agents deduplicate and prioritize results

#### Claude Desktop
- **Safe Batching:** limit=10 per search to prevent crashes
- **Iterative Presentation:** Progressive result display with user confirmation
- **Multi-Angle Coverage:** Multiple small searches instead of large ones
- **Crash Protection:** Built-in safeguards against conversation deletion

### Bibliography Features

- **Logseq-Ready Formatting:** Outline hierarchy (no markdown headers)
- **Compact Citations:** Author(s), Year. Title format
- **No Bold Styling:** Plain text throughout
- **Chinese-English Support:** Bilingual titles and abstracts
- **Automatic Translation:** English translations of Chinese content
- **Zotero Links:** Clickable zotero:// URLs for each item
- **Thematic Organization:** Grouped by categories (no summary sections)

## Installation

### Prerequisites

1. **Zotero Desktop** with your reference library
2. **Zotero MCP Server** installed and configured
   - Repository: https://github.com/54yyyu/zotero-mcp
   - Follow their installation instructions
3. **Claude Desktop** and/or **Claude Code** with MCP support
4. The Zotero MCP server configured in your Claude MCP settings

### Installing This Skill

#### For Claude Desktop

1. Download the [latest release](../../releases) zip file
2. Open Claude Desktop
3. Go to Settings → Skills
4. Click "Import Skill" and select the downloaded zip file

#### For Claude Code

1. Clone or download this repository
2. Copy the skill folder to `~/.claude/skills/zotero-mcp/`
3. Restart Claude Code or reload skills

#### Manual Installation

1. Clone or download this repository:
   ```bash
   git clone https://github.com/kerim/zotero-mcp-skill.git
   ```
2. Copy the `SKILL.md` file to your Claude skills directory
3. Restart Claude or reload skills

## Usage

### When Claude Uses This Skill

Claude automatically activates this skill when you need to:
- Search your Zotero library for papers or references
- Explore a research topic in your collection
- Find related work on a concept or theme
- Locate specific authors or papers
- Search through your annotations and notes
- Generate formatted bibliographies for Logseq

### Example Queries

**Conceptual Discovery:**
```
"Find papers about embodied cognition"
```
- **Claude Code:** Launches agent → comprehensive multi-strategy search → curated results
- **Claude Desktop:** Multiple semantic/keyword/tag searches (limit=10 each) → combined results

**Author Search:**
```
"What do I have by Susan Carey?"
```
- **Claude Code:** Agent searches author + citations + concepts
- **Claude Desktop:** Batched searches by author + notes + semantic concepts

**Complex Topic:**
```
"Research about skill transfer in mathematical reasoning"
```
- **Claude Code:** Agent cross-references multiple concepts → thematic synthesis
- **Claude Desktop:** Combined semantic/keyword searches → manual synthesis

**Bibliography Generation:**
```
"Create a Logseq bibliography for all papers on Indigenous language policy"
```
→ Claude searches comprehensively → retrieves metadata → formats with:
  - Logseq outline hierarchy (no headers)
  - Compact citations (Author, Year. Title)
  - Chinese/English bilingual support
  - No bold styling
  - Zotero links

### Search Patterns You'll See

#### Claude Code
1. **Analyze query** → Detect search type
2. **Launch agent** → Autonomous comprehensive search
3. **Agent executes** → Multiple strategies in parallel
4. **Agent synthesizes** → Deduplication and prioritization
5. **Present findings** → Curated results with context

#### Claude Desktop
1. **Analyze query** → Determine approach
2. **Execute batched searches** → 5-10 searches with limit=10
3. **Combine results** → Merge and deduplicate
4. **Refine if needed** → Alternative angles for poor results
5. **Present findings** → Results with search path explanation

## Search Philosophy

This skill enforces a **"search comprehensively, not narrowly"** philosophy:

### Core Principles

- **Never settle for one search** - Always try multiple angles
- **Never use one search term** - Always try variations and synonyms
- **Always combine methods** - Semantic + keyword + tags + full-text
- **Always check tags first** - Discover user's tagging conventions
- **Always refine iteratively** - Analyze results and adjust strategy
- **Always ask when unclear** - Clarifying questions for vague queries
- **Adapt to environment** - Use agents in Code, batching in Desktop

### Minimum Search Requirements

For any user query, Claude will try AT MINIMUM:
- 3 semantic search variations (different phrasings)
- 3 keyword variations (synonyms, related terms)
- 1 tag search (after checking available tags)
- 1 full-text/annotation search (if applicable)

## Configuration

### Customization

You can customize this skill by editing `SKILL.md`:

- Modify default search limits (Claude Desktop: currently limit=10)
- Add domain-specific search patterns
- Adjust search variation requirements
- Add custom presentation preferences
- Customize bibliography formatting rules
- Adjust agent prompts (Claude Code only)

### Search Database

The skill will check and update your Zotero semantic search database when needed using:
- `zotero_get_search_database_status` - Check database status
- `zotero_update_search_database` - Update with latest items

## Technical Details

### MCP Tools Used

This skill teaches Claude to use these Zotero MCP server tools:

| Tool | Purpose | Desktop Limit | Code (Agent) |
|------|---------|---------------|--------------|
| `zotero_semantic_search` | AI-powered conceptual search | 10 | No limit |
| `zotero_search_items` | Keyword matching | 10 | No limit |
| `zotero_advanced_search` | Multi-criteria filtering | 10 | No limit |
| `zotero_get_tags` | Discover available tags | - | - |
| `zotero_search_by_tag` | Tag-based filtering | 10 | No limit |
| `zotero_search_notes` | Search annotations/notes | 10 | No limit |
| `zotero_get_annotations` | Retrieve highlights | 10 | No limit |
| `zotero_get_item_fulltext` | Access full-text content | - | - |
| `zotero_get_item_metadata` | Retrieve item metadata | - | - |
| `zotero_get_collections` | List collections | - | - |
| `zotero_get_recent` | Recent additions | 10 | No limit |

### Safety Mechanisms

#### Claude Desktop
1. **Hard limit defaults** - All searches use limit=10 by default
2. **Batched iteration** - Multiple small searches instead of large ones
3. **Interactive fallback** - Progressive result presentation
4. **Crash prevention** - Never exceeds limit=20 in a single call

#### Claude Code
1. **Agent sandboxing** - Agents run searches independently
2. **Parallel execution** - Multiple searches simultaneously
3. **Intelligent synthesis** - Agents deduplicate and prioritize
4. **No conversation risk** - Agents don't cause UI crashes

## Troubleshooting

### "No results found"

Claude will:
- Try broader search terms
- Use more general concepts
- Remove filters
- Search related fields/disciplines
- Ask clarifying questions

### "Search database outdated"

Claude will suggest:
```
zotero_update_search_database
```

### "Too many/few results"

Claude will automatically:
- **Too many:** Add filters (tags, date ranges, collections)
- **Too few:** Broaden terms, try synonyms, search alternative angles

### "Claude Desktop crashed during search"

If you experience conversation deletion:
- The skill enforces limit=10 by default to prevent this
- Ensure you're using the latest version of this skill
- Report persistent issues to both this repo and Zotero MCP server

## Contributing

Contributions welcome! To improve this skill:

1. Fork this repository
2. Make your changes to `SKILL.md`
3. Test with both Claude Desktop and Claude Code
4. Submit a pull request

### Ideas for Contributions

- Domain-specific search patterns (medical, legal, etc.)
- Additional search failure recovery strategies
- Integration with other Zotero MCP features
- Result presentation templates
- Language-specific search variations
- Additional bibliography formatting styles
- More agent task patterns

## Related Projects

- **Zotero MCP Server:** https://github.com/54yyyu/zotero-mcp
- **Model Context Protocol:** https://modelcontextprotocol.io/
- **Claude Desktop:** https://claude.ai/download
- **Claude Code:** https://docs.claude.com/claude-code

## License

MIT License - see [LICENSE](LICENSE) file for details

## Acknowledgments

- Built for the [Zotero MCP Server](https://github.com/54yyyu/zotero-mcp) by @54yyyu
- Developed for Claude Desktop and Claude Code
- Semantic search powered by Claude's embedding models

## Support

- **Issues:** [GitHub Issues](../../issues)
- **Discussions:** [GitHub Discussions](../../discussions)
- **Zotero MCP Server Issues:** https://github.com/54yyyu/zotero-mcp/issues

---

**Made for researchers who want comprehensive, intelligent search of their Zotero libraries - whether in Claude Desktop or Claude Code.**
