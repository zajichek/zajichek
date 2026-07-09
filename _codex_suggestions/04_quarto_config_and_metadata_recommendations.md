# Quarto Config and Metadata Recommendations

## Recommendation 1: Verify Sitemap Generation Rather Than Adding Unsupported Config

### Purpose
Sitemaps help search engines discover and refresh pages. The practical goal is to preserve the sitemap Quarto is already generating and avoid adding unsupported configuration that could create false confidence or render warnings.

### Current issue
`_site/sitemap.xml` exists in rendered output, and `_quarto.yml` has `site-url: https://www.zajichekstats.com/`. Quarto's public website options reference does not show a simple `website.sitemap: true` option in the same way it documents `open-graph`, `twitter-card`, listings, and feeds, so the earlier suggestion to add `sitemap: true` should not be treated as a known-valid configuration change.

### Suggested change
Do not add a speculative `sitemap: true` key. Instead, keep `site-url` set, confirm that a clean render continues to generate `_site/sitemap.xml`, and focus on making sure public pages have good titles/descriptions and drafts are excluded.

### Where to implement
- `_quarto.yml`, `website.site-url`
- Rendered `_site/sitemap.xml`, for verification only

### Implementation sketch
```yaml
website:
  site-url: https://www.zajichekstats.com/
```

### Sequential implementation steps
1. Confirm the current Quarto version with `quarto --version`.
2. Render the site.
3. Confirm `_site/sitemap.xml` is generated.
4. Confirm draft posts do not appear in the sitemap.
5. Confirm important public pages, topic hubs, and `start-here.qmd` appear after they are created.

### Risk / possible site issues
Adding unsupported YAML may be ignored or produce warnings. Verification is safer than adding a key that is not clearly documented.

### How to verify
Run `quarto render` and confirm `_site/sitemap.xml` exists and includes the expected public pages.

## Recommendation 2: Enable Quarto `llms.txt` Output After Metadata Cleanup

### Purpose
Quarto can generate an `llms.txt` index and clean `.llms.md` Markdown versions of pages for AI tools. This directly supports AI-search discoverability and is more actionable than relying only on semantic headings.

### Current issue
`_quarto.yml` does not currently include `llms-txt: true`. The site has strong explanatory content, but no generated LLM-friendly output file was observed at the project root or under `_site/`.

### Suggested change
After cleaning obvious metadata issues and confirming draft status, enable Quarto's `llms.txt` output.

### Where to implement
- `_quarto.yml`, `website:` section
- Individual posts where LLM-specific exclusions or additions are needed

### Implementation sketch
```yaml
website:
  llms-txt: true
```

### Sequential implementation steps
1. Update the site description and the worst post descriptions first.
2. Confirm that draft posts are intentionally marked `draft: true`.
3. Add `llms-txt: true` under `website:`.
4. Render the site.
5. Inspect `_site/llms.txt` and a few generated `.llms.md` files.
6. If a page contains content that should be excluded from LLM output, use Quarto conditional content classes.

### Risk / possible site issues
The generated Markdown can expose rough draft-like introductions, weak descriptions, or pages that are technically public but not meant to be prominent. Draft pages are excluded, but published pages should be reviewed.

### How to verify
Render the site and open `_site/llms.txt`. Confirm it lists the intended public pages and that generated `.llms.md` files are readable.

## Recommendation 3: Strengthen Site-Wide Metadata Defaults

### Purpose
Good default metadata helps every page produce better browser titles, social cards, and search snippets.

### Current issue
`_quarto.yml` includes `description: "Statistician/data scientist in Central Wisconsin."`, `open-graph: true`, `site-url`, `favicon`, `repo-url`, and Google Analytics. The description is accurate but too generic to represent the site's strongest topics.

### Suggested change
Use a more specific site description that mentions practical statistics, healthcare analytics, R/Shiny, reproducible analytics, and data science writing.

### Where to implement
- `_quarto.yml`, `website.description`

### Implementation sketch
```yaml
description: "Practical writing on statistics, healthcare analytics, R/Shiny applications, reproducible workflows, and data science infrastructure."
```

### Sequential implementation steps
1. Draft 2 or 3 candidate descriptions.
2. Choose one under roughly 160 characters if possible.
3. Update `website.description`.
4. Render and inspect homepage metadata.

### Risk / possible site issues
Overloading the description with too many keywords can feel spammy. Keep it natural and accurate.

### How to verify
Inspect the rendered homepage HTML title/meta description and share-card preview if available.

## Recommendation 4: Add Twitter/X Card Metadata If Social Sharing Matters

### Purpose
Open Graph helps link previews broadly, while Twitter/X card metadata can improve previews on X and some other platforms.

### Current issue
`_quarto.yml` sets `open-graph: true`, but there is no visible Twitter card configuration in source.

### Suggested change
If you share posts on X/LinkedIn often, add Quarto-supported Twitter card metadata and ensure each post's `image: "feature.png"` is suitable for cards.

### Where to implement
- `_quarto.yml`, `website:` section
- Individual `post/*/feature.png` images if some are low quality or too small

### Implementation sketch
```yaml
website:
  open-graph: true
  twitter-card:
    site: "@zajichekstats"
    creator: "@zajichekstats"
```

### Sequential implementation steps
1. Confirm Quarto's current `twitter-card` syntax for your installed version.
2. Add creator/site metadata.
3. Render one representative post.
4. Test the post URL with a social card preview tool after deployment.

### Risk / possible site issues
Unsupported keys may be ignored. Some social networks cache old previews aggressively.

### How to verify
Inspect rendered HTML for Twitter card meta tags and test a deployed URL after publishing.

## Recommendation 5: Use A Shared Blog Listing Configuration Where Possible

### Purpose
Shared listing conventions make the homepage and future topic pages feel coherent.

### Current issue
`index.qmd` defines the root blog listing with `contents: post`, `sort`, `filter-ui`, `sort-ui`, `image-align`, `image-placeholder`, `categories`, and `feed`. Future topic pages could drift if each one invents its own listing format.

### Suggested change
Document a preferred listing style and reuse it on hub pages. Keep the homepage listing broad, while hub pages use curated text plus filtered listings.

### Where to implement
- `index.qmd`
- Future `topics/*.qmd`
- Optional short note in `_codex_suggestions` or a private content style guide

### Implementation sketch
```yaml
listing:
  contents: ../post
  type: default
  sort: "date desc"
  image-align: left
  categories: true
```

### Sequential implementation steps
1. Decide whether topic hub listings should include filter UI. For curated hubs, omit filter UI at first.
2. Use consistent `type`, `sort`, and image behavior.
3. Add manual featured links above listings for editorial control.
4. Preview multiple hub pages to confirm consistency.

### Risk / possible site issues
Too many filter controls on every page can feel repetitive. Topic hubs may work better with curated lists plus short listings.

### How to verify
Preview the homepage and hub pages side by side. Confirm listing cards feel related but not overwhelming.

## Recommendation 6: Add A Footer Structure With Useful Links

### Purpose
A footer can reinforce site identity, provide important navigation, and offer a subtle CentralStatz connection without crowding the navbar.

### Current issue
`_quarto.yml` currently has `page-footer: "© 2026 Zajichek Stats"`. This is simple, but it does not help readers move to Start Here, Topics, RSS, About, or CentralStatz.

### Suggested change
Replace the simple string footer with a structured footer once the key pages exist.

### Where to implement
- `_quarto.yml`, `website.page-footer`

### Implementation sketch
```yaml
page-footer:
  left: "© 2026 Zajichek Stats"
  center:
    - text: "Start Here"
      href: start-here.qmd
    - text: "RSS"
      href: index.xml
  right:
    - text: "CentralStatz"
      href: https://www.centralstatz.com/
```

### Sequential implementation steps
1. Create `start-here.qmd`.
2. Add footer links for Start Here, RSS, About, and CentralStatz.
3. Render and inspect post pages, not only the homepage.
4. Keep footer link count modest.

### Risk / possible site issues
Footer YAML structure can be picky. If render fails, simplify to left/center/right text and add links one by one.

### How to verify
Render and check the footer on homepage, post pages, presentations, and publications.

## Recommendation 7: Consider A Lightweight Robots File Source If Deployment Allows

### Purpose
Robots files can point crawlers to the sitemap and clarify indexing intent.

### Current issue
`_site/robots.txt` exists in rendered output, but there is no visible source-level `robots.txt` at the project root.

### Suggested change
If Quarto/deployment does not already generate the desired robots file, consider adding a simple source `robots.txt`. Quarto recognizes and copies root-level `robots.txt` files into the output site.

### Where to implement
- Project root `robots.txt`, only after confirming how the current `_site/robots.txt` is generated

### Implementation sketch
```text
User-agent: *
Allow: /
Sitemap: https://www.zajichekstats.com/sitemap.xml
```

### Sequential implementation steps
1. Inspect `_site/robots.txt` after a clean render.
2. If it already contains the sitemap and desired rules, do nothing.
3. If not, add a minimal root `robots.txt`.
4. Render and confirm it copies to `_site/robots.txt`.

### Risk / possible site issues
An overly restrictive robots file can block indexing. Keep it minimal.

### How to verify
Open the deployed `https://www.zajichekstats.com/robots.txt` and confirm the sitemap URL is present.
