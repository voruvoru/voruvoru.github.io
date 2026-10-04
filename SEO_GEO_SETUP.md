# VoruVoru — Google Indexing, SEO & GEO Setup

## 1. Deploy
Upload all files in this package to the root of `voruvoru/voruvoru.github.io`.

## 2. Google Search Console
1. Open https://search.google.com/search-console/
2. Add property: `https://voruvoru.github.io/` using URL-prefix property.
3. Choose HTML file verification.
4. Download Google's verification HTML file and upload it to the repository root.
5. Commit and wait for GitHub Pages deployment.
6. Return to Search Console and click Verify.

## 3. Submit sitemap
In Search Console > Sitemaps, submit:
`https://voruvoru.github.io/sitemap.xml`

## 4. Request indexing
Use URL Inspection for:
- https://voruvoru.github.io/
- https://voruvoru.github.io/about.html
- https://voruvoru.github.io/faq.html
- the three article URLs
Then select Request Indexing.

## 5. Validate
Check:
- Rich Results Test: https://search.google.com/test/rich-results
- PageSpeed Insights: https://pagespeed.web.dev/
- robots.txt: https://voruvoru.github.io/robots.txt
- sitemap: https://voruvoru.github.io/sitemap.xml

## GEO notes
The package includes clear entity information, Organization/WebSite/Service structured data, About/FAQ pages, factual evergreen articles, and `llms.txt`.
`llms.txt` is experimental and not an official Google ranking/indexing standard.
