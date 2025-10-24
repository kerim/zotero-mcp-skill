# Zotero MCP Search Skill for Claude

A comprehensive Claude Desktop skill that enables advanced, multi-strategy searching of your Zotero library through the Zotero MCP (Model Context Protocol) server.

## What This Is

This is a **Claude Desktop skill** that teaches Claude how to search your Zotero reference library intelligently and comprehensively. Instead of simple one-off searches, Claude learns to:

- Use **semantic/AI-powered search** to find conceptually related papers
- Try **multiple search angles** with different phrasings and synonyms
- **Combine search methods** (semantic + keyword + tags + full-text + annotations)
- **Iteratively refine** searches based on results
- **Ask clarifying questions** when your query is ambiguous

## Why This Skill Exists

### The Problem

The Zotero MCP server provides powerful semantic search capabilities, but using it effectively requires:
- Understanding multiple search strategies (semantic vs. keyword vs. tag-based)
- Knowing when to use each search method
- Trying multiple variations and phrasings
- Searching across metadata, full-text, notes, and annotations
- Avoiding response limits that can crash Claude Desktop

Without guidance, Claude might:
- Use only one search method and miss relevant papers
- Try only one search phrase and return incomplete results
- Request too many results at once (causing crashes)
- Not explore alternative search angles

### The Solution

This skill provides Claude with:
- **Mandatory multi-angle search strategies** (minimum 3 semantic + 3 keyword variations)
- **Safe batching guidelines** (limit=10 per search to prevent crashes)
- **Comprehensive search patterns** combining multiple methods
- **Iterative refinement workflows** to improve results

## Features

### Core Capabilities

- **Semantic-First Discovery:** AI-powered conceptual search to find related work even without exact keyword matches
- **Multi-Strategy Search:** Automatically combines semantic, keyword, tag-based, and full-text methods
- **Iterative Refinement:** Analyzes initial results and refines search strategy accordingly
- **Safety-First Design:** Built-in protections against Claude Desktop crash bugs
- **Comprehensive Coverage:** Searches metadata, full-text PDFs, annotations, and notes

### Search Methods Taught

1. **Semantic Search** - Conceptual similarity using AI embeddings
2. **Keyword Search** - Traditional text matching with variations
3. **Advanced Search** - Multi-criteria filtering (author + keyword + year)
4. **Tag Search** - Leverage your existing Zotero tags
5. **Full-Text Search** - Search within PDF contents
6. **Annotation Search** - Find your highlights and notes
7. **Collection Search** - Navigate your Zotero collections

### Safety Features

**Critical Bug Protection:** Claude Desktop has a known bug where large MCP responses can timeout and delete entire conversations. This skill enforces:

- Default `limit=10` for all searches (max 15-20 only when critical)
- Multiple small searches instead of one large search
- Iterative interactive approaches for user-guided exploration

## Installation

### Prerequisites

1. **Zotero Desktop** with your reference library
2. **Zotero MCP Server** installed and configured
   - Repository: https://github.com/54yyyu/zotero-mcp
   - Follow their installation instructions
3. **Claude Desktop** with MCP support
4. The Zotero MCP server configured in your Claude Desktop MCP settings

### Installing This Skill

#### Option 1: Download and Import

1. Download the [latest release](../../releases) zip file
2. Open Claude Desktop
3. Go to Settings → Skills
4. Click "Import Skill" and select the downloaded zip file

#### Option 2: Install from URL

If Claude Desktop supports direct URL import:
```
https://github.com/kerim/zotero-mcp-skill/archive/main.zip
```

#### Option 3: Manual Installation

1. Clone or download this repository
2. Copy the `zotero-mcp-skill` folder contents to your Claude skills directory
3. Restart Claude Desktop or reload skills

## Usage

### When Claude Uses This Skill

Claude automatically activates this skill when you need to:
- Search your Zotero library for papers or references
- Explore a research topic in your collection
- Find related work on a concept or theme
- Locate specific authors or papers
- Search through your annotations and notes

### Example Queries

**Conceptual Discovery:**
```
"Find papers about embodied cognition"
```
→ Claude uses semantic search with multiple phrasings + keyword variations + tag checking + annotation search

**Author Search:**
```
"What do I have by Susan Carey?"
```
→ Claude searches by author + checks citations in notes + uses semantic search for the author's main concepts

**Complex Topic:**
```
"Research about skill transfer in mathematical reasoning"
```
→ Claude combines semantic and keyword methods + cross-references results + searches annotations

**Exploratory:**
```
"What's in my library about cognitive development?"
```
→ Claude uses multiple conceptual phrasings + discovers related tags + searches notes + presents thematic clusters

### Search Patterns You'll See

When you ask Claude to search, it will typically:

1. **Analyze your query** - Determine if it's conceptual, specific, or exploratory
2. **Execute multi-angle searches** - Run 5-10 different searches with small limits
3. **Combine results** - Merge and deduplicate findings
4. **Refine if needed** - Try alternative angles if results are poor
5. **Present findings** - Show results with search path explanation

## Search Philosophy

This skill enforces a **"search comprehensively, not narrowly"** philosophy:

### Core Principles

- **Never settle for one search** - Always try multiple angles
- **Never use one search term** - Always try variations and synonyms
- **Always combine methods** - Semantic + keyword + tags + full-text
- **Always check tags first** - Discover user's tagging conventions
- **Always refine iteratively** - Analyze results and adjust strategy
- **Always ask when unclear** - Clarifying questions for vague queries

### Minimum Search Requirements

For any user query, Claude will try AT MINIMUM:
- 3 semantic search variations (different phrasings)
- 3 keyword variations (synonyms, related terms)
- 1 tag search (after checking available tags)
- 1 full-text/annotation search (if applicable)

## Configuration

### Customization

You can customize this skill by editing `SKILL.md`:

- Modify default search limits (currently limit=10)
- Add domain-specific search patterns
- Adjust search variation requirements
- Add custom presentation preferences

### Search Database

The skill will check and update your Zotero semantic search database when needed using:
- `zotero_get_search_database_status` - Check database status
- `zotero_update_search_database` - Update with latest items

## Technical Details

### MCP Tools Used

This skill teaches Claude to use these Zotero MCP server tools:

| Tool | Purpose | Default Limit |
|------|---------|---------------|
| `zotero_semantic_search` | AI-powered conceptual search | 10 |
| `zotero_search_items` | Keyword matching | 10 |
| `zotero_advanced_search` | Multi-criteria filtering | 10 |
| `zotero_get_tags` | Discover available tags | - |
| `zotero_search_by_tag` | Tag-based filtering | 10 |
| `zotero_search_notes` | Search annotations/notes | 10 |
| `zotero_get_annotations` | Retrieve highlights | 10 |
| `zotero_get_item_fulltext` | Access full-text content | - |
| `zotero_get_collections` | List collections | - |
| `zotero_get_recent` | Recent additions | 10 |

### Safety Mechanisms

1. **Hard limit defaults** - All searches use limit=10 by default
2. **Batched iteration** - Multiple small searches instead of large ones
3. **Interactive fallback** - Progressive result presentation with user confirmation

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

## Contributing

Contributions welcome! To improve this skill:

1. Fork this repository
2. Make your changes to `SKILL.md`
3. Test with Claude Desktop
4. Submit a pull request

### Ideas for Contributions

- Domain-specific search patterns (medical, legal, etc.)
- Additional search failure recovery strategies
- Integration with other Zotero MCP features
- Result presentation templates
- Language-specific search variations

## Related Projects

- **Zotero MCP Server:** https://github.com/54yyyu/zotero-mcp
- **Model Context Protocol:** https://modelcontextprotocol.io/
- **Claude Desktop:** https://claude.ai/download

## License

MIT License - see [LICENSE](LICENSE) file for details

## Acknowledgments

- Built for the [Zotero MCP Server](https://github.com/54yyyu/zotero-mcp) by @54yyyu
- Developed for Claude Desktop
- Semantic search powered by Claude's embedding models

## Support

- **Issues:** [GitHub Issues](../../issues)
- **Discussions:** [GitHub Discussions](../../discussions)
- **Zotero MCP Server Issues:** https://github.com/54yyyu/zotero-mcp/issues

---

**Made for researchers who want comprehensive, intelligent search of their Zotero libraries.**
