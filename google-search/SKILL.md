---
name: google-search
description: Use web_fetch with Google search URL when you need keyword search (no Brave/Perplexity API).
metadata: { "openclaw": { "emoji": "🔍", "requires": {} } }
---

# Google Search via web_fetch
When you need to search the web by keyword and web_search is unavailable (no Brave/Perplexity API) or you prefer this method, use the web_fetch tool with Google's search URL.

## When to use
- User asks to "search for …", "look up …", "find …" on the web.
- You need recent or factual results and don't have a specific URL.
- web_search is not configured or returns an error.

## How to do it
1. Build the Google search URL:
   - Base: https://www.google.com/search?q=
   - Append the URL-encoded query (e.g. spaces → + or %20, special characters encoded).
2. Call web_fetch with that URL.
   Example: for the query "OpenClaw 安裝" use:
   - https://www.google.com/search?q=OpenClaw+%E5%AE%89%E8%A3%9D
   or (spaces as +):
   - https://www.google.com/search?q=OpenClaw+installation
3. Read the returned content (Google's result page; extraction may be noisy). From it, identify suitable result links: titles, snippets, and target URLs (the actual result links; prefer direct URLs over google.com/url?… redirects when the destination is clear).
4. Continue with web_fetch on chosen targets: For one or more relevant result URLs (e.g. the first 1–2 that best match the user's intent), call web_fetch again with that URL to fetch the full page content. Use that content to answer the user or to refine your summary.
5. Summarize for the user: combine the search snippets and, when you fetched them, the content from the target page(s).

## Notes
- Google's search results page is HTML; web_fetch will extract main content (Readability or Firecrawl if enabled). The result may include ads and layout text—focus on result titles, URLs, and snippets.
- Do not use web_fetch for general browsing; use it only when the user explicitly needs a keyword search and you have no web_search available.
