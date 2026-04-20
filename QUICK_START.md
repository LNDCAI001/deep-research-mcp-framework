# Quick Start: Deep Research with MCP Tools

## ⚡ 5-Minute Setup

1. **Clone this repo** (optional but recommended):
   ```bash
   git clone https://github.com/LNDCAI001/deep-research-mcp-framework.git
   cd deep-research-mcp-framework
   ```

2. **Define your research question** clearly:
   ```
   ❌ Too broad: "Tell me about AI"
   ✅ Focused: "What are the ethical frameworks proposed for generative AI in healthcare between 2023-2026?"
   ```

3. **Start with FireCrawl Search** (most powerful entry point):
   ```json
   {
     "query": "generative AI healthcare ethics framework 2023..2026",
     "limit": 10,
     "sources": ["web", "news"],
     "scrapeOptions": {
       "formats": ["markdown"],
       "onlyMainContent": true
     }
   }
   ```

---

## 🎯 One-Page Workflow

### Step 1: Discovery (5-10 min)
```
🔍 Search Strategy:
├─ Primary: FireCrawl Search with targeted query
├─ Supplement: Brave Search for recent news
└─ Cross-check: DuckDuckGo for diverse perspectives

💡 Pro Tip: Use search operators:
• "exact phrase" for precision
• site:.edu OR site:.gov for authoritative sources
• intitle:keyword for title-focused results
• -exclude to filter noise
```

### Step 2: Prioritize Sources (2-3 min)
```
✅ Keep sources that:
• Match your timeframe (e.g., 2023-2026)
• Come from authoritative domains (.edu, .gov, peer-reviewed)
• Directly address your research question
• Have clear methodology or citations

❌ Skip sources that:
• Are opinion pieces without evidence
• Are older than your timeframe (unless foundational)
• Don't provide actionable data or insights
```

### Step 3: Extract Content (10-20 min)
```
📄 For single articles:
{
  "url": "https://example.com/article",
  "formats": ["markdown"],
  "onlyMainContent": true,
  "maxAge": 172800000
}

🌐 For multi-page sites:
1. Map first: {"url": "https://example.com", "limit": 30}
2. Crawl strategically: 
   {
     "url": "https://example.com/research/*",
     "maxDiscoveryDepth": 2,
     "limit": 15,
     "deduplicateSimilarURLs": true
   }

📊 For structured data:
{
  "urls": ["url1", "url2"],
  "prompt": "Extract: author, date, key findings, methodology",
  "schema": { /* define your fields */ }
}
```

### Step 4: Synthesize & Document (5-10 min)
```
📝 Quick Documentation:
1. Create GitHub Issue for each key finding:
   {
     "title": "Finding: [brief description]",
     "body": "Source: [URL]\nKey point: [summary]\nRelevance: [why it matters]",
     "labels": ["finding", "high-priority"]
   }

2. Track contradictions as separate issues

3. Commit extracted content to /sources/raw/
```

### Step 5: Iterate (as needed)
```
🔄 Refinement Loop:
1. Review findings → Identify gaps
2. Refine search queries with new keywords
3. Follow citation trails from strong sources
4. Update documentation with new insights
```

---

## 🚀 Copy-Paste Templates

### Template: Basic Research Query
```json
{
  "query": "[your topic] [key aspect] [timeframe if relevant]",
  "limit": 10,
  "sources": ["web"],
  "scrapeOptions": {
    "formats": ["markdown"],
    "onlyMainContent": true
  }
}
```

### Template: Academic-Focused Search
```json
{
  "query": "[topic] peer reviewed study site:.edu OR site:.gov OR site:arxiv.org",
  "limit": 10,
  "sources": ["web"],
  "scrapeOptions": {
    "formats": ["markdown"],
    "onlyMainContent": true
  }
}
```

### Template: Recent News Search
```json
{
  "query": "[topic] news analysis",
  "limit": 10,
  "sources": ["news", "web"],
  "scrapeOptions": {
    "formats": ["markdown"],
    "onlyMainContent": true
  }
}
```

### Template: Single Page Scrape
```json
{
  "url": "https://example.com/important-article",
  "formats": ["markdown"],
  "onlyMainContent": true,
  "maxAge": 172800000,
  "removeBase64Images": true
}
```

### Template: Structured Data Extraction
```json
{
  "urls": ["https://source1.com", "https://source2.com"],
  "prompt": "Extract the following: publication date, author name, main conclusion, sample size, limitations",
  "schema": {
    "type": "object",
    "properties": {
      "publication_date": {"type": "string"},
      "author": {"type": "string"},
      "main_conclusion": {"type": "string"},
      "sample_size": {"type": "string"},
      "limitations": {"type": "array", "items": {"type": "string"}}
    },
    "required": ["publication_date", "main_conclusion"]
  },
  "enableWebSearch": false
}
```

### Template: GitHub Issue for Research Question
```json
{
  "title": "Research Question: [clear, specific question]",
  "body": "## Context\n[Why this matters]\n\n## Current Understanding\n[What we know so far]\n\n## Gap\n[What we need to find]\n\n## Sources to Check\n- [ ] Source 1\n- [ ] Source 2",
  "labels": ["research-question", "needs-investigation"]
}
```

---

## ⚠️ Troubleshooting Quick Reference

| Problem | Quick Fix |
|---------|-----------|
| **Search returns irrelevant results** | Add more specific keywords, use `"exact phrase"`, add `site:.edu` filter |
| **Scrape returns empty/no content** | Check if page requires JS, try `waitFor: 3000`, verify URL is accessible |
| **Crawl takes too long** | Reduce `limit` to 10, lower `maxDiscoveryDepth` to 2, enable `deduplicateSimilarURLs` |
| **Extracted data doesn't match schema** | Simplify schema, test on 1 URL first, make prompt more specific |
| **Token limit exceeded** | Break crawl into smaller chunks, reduce `limit`, use map+batch approach |
| **Can't find recent sources** | Use Brave Search, add date filters to query, check news sources |
| **Too many duplicate results** | Enable `deduplicateSimilarURLs: true`, vary search terms, use different search engines |

---

## 📊 Success Metrics

Track these to measure research quality:

```
✅ Source Quality Score:
• 3 pts: Peer-reviewed academic source
• 2 pts: Government/official report
• 1 pt: Reputable news/think tank
• 0 pts: Blog/opinion without citations

✅ Coverage Metrics:
• Number of unique domains consulted
• Timeframe coverage (does it span your target period?)
• Perspective diversity (multiple viewpoints represented?)

✅ Output Quality:
• % of extracted data that matches schema
• Number of actionable insights generated
• Clarity of synthesized conclusions
```

---

## 🔄 When to Use Which Tool (Decision Flow)

```
Start
  │
  ▼
Need to FIND sources? → FireCrawl Search (primary)
  │                      + Brave/DuckDuckGo (supplement)
  ▼
Have specific URLs?
  │
  ├─ Single URL → FireCrawl Scrape
  │
  ├─ Multiple pages, same site → FireCrawl Map → FireCrawl Crawl
  │
  └─ Need structured fields → FireCrawl Extract
        │
        ▼
  Need to track/manage? → GitHub Issues/PRs
        │
        ▼
  Ready to output? → Commit to repo, tag release
```

---

## 💡 Pro Tips for Faster Research

1. **Cache aggressively**: Always use `maxAge: 172800000` (2 days) for repeated requests
2. **Start small**: Test extraction on 1-2 URLs before scaling to 10+
3. **Use markdown format**: Easier to read and process than HTML
4. **Enable onlyMainContent**: Saves tokens and removes noise
5. **Batch similar tasks**: Group extractions by schema to reduce overhead
6. **Log everything**: Keep a research journal in GitHub Issues
7. **Iterate queries**: Use findings from first search to refine second search
8. **Set timeboxes**: 20 min discovery, 40 min extraction, 20 min synthesis

---

## 🎓 Example: Complete Mini-Research Session

**Question**: "What are the main criticisms of current LLM evaluation benchmarks?"

```
1️⃣ Discovery (FireCrawl Search):
{
  "query": "LLM evaluation benchmark criticism limitations 2024",
  "limit": 10,
  "sources": ["web", "news"]
}

→ Found: 3 academic papers, 2 blog posts from researchers, 1 news article

2️⃣ Prioritize:
✅ Keep: arxiv.org paper, conference proceeding, researcher blog with citations
❌ Skip: Generic tech blog without sources

3️⃣ Extract (FireCrawl Scrape):
{
  "url": "https://arxiv.org/abs/2401.xxxxx",
  "formats": ["markdown"],
  "onlyMainContent": true
}

4️⃣ Structure (FireCrawl Extract):
{
  "urls": ["arxiv-url", "conference-url"],
  "prompt": "Extract: benchmark name, criticism type, proposed alternative, evidence",
  "schema": { /* define fields */ }
}

5️⃣ Document (GitHub):
- Create issue: "Criticism: Benchmark X lacks real-world task coverage"
- Commit extracted content to /sources/raw/
- Add finding to /analysis/findings.md

6️⃣ Iterate:
- New query: "alternative LLM evaluation methods 2024"
- Follow citation trail from strongest paper
```

**Time elapsed**: ~45 minutes
**Output**: Structured comparison of 3 benchmark criticisms with sources

---

*Next: Read [RESEARCH_WORKFLOW.md](RESEARCH_WORKFLOW.md) for the complete framework*

*Repository: github.com/LNDCAI001/deep-research-mcp-framework*
