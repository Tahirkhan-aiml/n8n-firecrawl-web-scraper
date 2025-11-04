Firecrawl Web Scraper for n8n

Scrape 100s of URLs → Get clean Markdown + All Links 
Rate-limited, memory-safe, production-ready

> Turn any website into AI-ready content — automatically.


 What It Does

| Feature | Description |
|-------|-----------|
| Input | Any list of URLs (from DB, CSV, Airtable, etc.) |
| Scraping | Uses [Firecrawl.dev](https://firecrawl.dev) to extract clean markdown |
| Links | Extracts all internal/external links per page |
| Batching | Processes 40 URLs at a time (memory-safe) |
| Rate Limiting | 10 requests/min → Respects Firecrawl free tier |
| Output | `title`, `description`, `content` (markdown), `links` |

 How to Use
 
 1. Import Workflow
→ Click [firecrawl-web-scraper.json](firecrawl-web-scraper.json) → Copy all  
→ In n8n: New → Import from Clipboard (or drag file)

 2. Fix Red Warnings (Credentials)

| Credential | Name |
|----------|------|
| Firecrawl API Key | `Firecrawl Bearer` |

How to set it up:
1. Go to [https://firecrawl.dev](https://firecrawl.dev) → Get API key
2. In n8n → Credentials → HTTP Header Auth
3. Name: `Firecrawl Bearer`
4. Header: `Authorization` → Value: `Bearer YOUR_API_KEY`

 3. Connect Your Data Source
Replace these nodes with your own:

| Node | Replace With |
|------|--------------|
| `Get urls from own data source` | Your DB (PostgreSQL, Airtable, Google Sheets, etc.) |
| `Connect to your own data source` | Your output DB (to save results) |

Column must be named: `Page` (one URL per row)

 4. Test It

1. Click "Test workflow"
2. Wait → Processes 40 URLs → Pauses 45 sec → Next batch
3. Output example:
   ```json
   {
     "title": "n8n - Workflow Automation",
     "description": "Fair-code workflow automation tool",
     "content": "# Welcome to n8n...\n\nn8n is a...",
     "links": "https://n8n.io/pricing, https://docs.n8n.io"
   }
