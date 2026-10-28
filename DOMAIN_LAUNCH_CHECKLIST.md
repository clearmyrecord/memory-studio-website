# MemoryStudio.tv — domain cutover and SEO launch checklist

**Updated October 28, 2026.** `MemoryStudio.tv` has been purchased through IONOS. The domain is not yet verified as connected to GitHub Pages. This repository currently has working SEO content with canonicals pointing to its GitHub Pages project URL `https://clearmyrecord.github.io/memory-studio-website/` until the custom domain is verified and serves HTTPS. **Do not prematurely point canonical tags to a domain that does not yet resolve.**

## DNS and GitHub Pages (owner action)

1. The owner reports purchase of `memorystudio.tv` at IONOS. Confirm that it appears under **IONOS → Domains & SSL** and you control its DNS zone.
2. Verify the domain in the GitHub account or organization controlling `clearmyrecord`: follow GitHub's exact TXT ownership challenge. This prevents other accounts from claiming unverified domains. The TXT value is provided by GitHub and must not be invented.
3. Open `https://github.com/clearmyrecord/memory-studio-website/settings/pages`, confirm the site publishes from the `main` branch root, and set **Custom domain** to `memorystudio.tv`. Save. GitHub Pages may write a `CNAME` file for you.
4. At the **domain's DNS provider** configure the apex (@) **A** records for GitHub Pages:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
   Also create `www` **CNAME** → `clearmyrecord.github.io` (without `/memory-studio-website`). Do not leave conflicting apex A/AAAA or www records. Exact supported records must be re-checked against GitHub docs when making the DNS change.
5. Wait for GitHub Pages DNS check to succeed and for `https://memorystudio.tv/` to load the **Memory Studio** page with a valid certificate. Enable **Enforce HTTPS** in Pages settings. Confirm `https://www.memorystudio.tv/` redirects to the chosen apex if configured.
6. **After** domain/HTTPS verification, switch canonical/OG/JSON-LD URLs on `index.html` and all `guides/*.html`, plus the URLs in `sitemap.xml` and `robots.txt`, from `https://clearmyrecord.github.io/memory-studio-website/` to `https://memorystudio.tv/`. The user can ask ChatGPT to perform that repo-wide update after the domain is active. Keep relative guide/navigation links and ensure the GitHub Pages-generated `CNAME` is present in the published source.
7. Search Console: add a **Domain property** for `memorystudio.tv` and verify with the Search Console TXT record (distinct from GitHub's challenge). Submit `https://memorystudio.tv/sitemap.xml`; inspect/index the homepage and three guides. Check crawl status, HTTPS, canonical and duplicate indexing issues. Consider adding the domain to Bing Webmaster Tools. XML sitemap is an indexing hint, not a guarantee of ranking or crawling.
8. Monitor Google Search Console Performance for real user queries, refine helpful guides and product documentation based on what visitors seek, and keep product promises accurate as beta/commercial availability changes.

## Currently implemented in this repository

- Unique homepage title, description, canonical, Open Graph and Twitter summary metadata.
- Organization, WebSite and SoftwareApplication JSON-LD without misleading current paid offers or fabricated reviews.
- Three distinct original guides with unique titles/descriptions, Article and BreadcrumbList metadata and contextual links.
- Linked guide section on the homepage, v42 development beta messaging and unchanged early access (no live sales).
- `sitemap.xml` for 4 crawlable URLs, plus a `robots.txt` staged for the future domain root. Note: on a GitHub **project** Pages site, `/memory-studio-website/robots.txt` is *not* the site-origin robots file; it becomes the root robots file when the custom domain serves the repository at `/`.

## Current limitations

- MemoryStudio.tv ownership, DNS, TLS, search indexing and search-console verification are **not confirmed** just because SEO files exist.
- The existing public beta is manually requested, not a production SaaS checkout. Stripe products remain in test/sandbox.
- Search snippets and results are determined by search engines; structured data does not guarantee rich results.
- Store active media/project files locally. Do not add customer photos, credentials, private license keys or source documentary projects to this public repository.

Official documentation:
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https
- https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap
- https://developers.google.com/search/docs/appearance/structured-data/software-app
