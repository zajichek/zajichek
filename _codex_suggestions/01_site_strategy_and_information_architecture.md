# Site Strategy and Information Architecture Recommendations

## Recommendation 1: Create Topic Pillar Hub Pages

### Purpose
Topic hub pages give readers, search engines, and AI-answer systems a clear map of what the site is about. They also help convert a broad archive into recognizable expertise areas: healthcare analytics, statistical thinking, reproducible analytics, Shiny apps, infrastructure, and AI for analytics.

### Current issue
The homepage at `index.qmd` lists posts directly from `post/`, but there are no visible topic hub pages beyond Quarto category pages. The categories in post front matter are useful, but they are mostly archive labels rather than curated entry points. Strong clusters already exist, especially readmissions/healthcare, statistical significance/decision making, Shiny/web apps, and AI-assisted analytics.

### Suggested change
Add a small set of curated topic hub pages that introduce each pillar, define who it is for, and link to the best related posts. Start with 4 or 5 hubs rather than trying to classify everything at once.

Suggested initial hubs:

- Healthcare Analytics
- Statistical Thinking
- Reproducible Analytics
- R / Shiny Applications
- AI for Analytics

### Where to implement
- New files such as `topics/healthcare-analytics.qmd`, `topics/statistical-thinking.qmd`, `topics/reproducible-analytics.qmd`, `topics/r-shiny.qmd`, and `topics/ai-for-analytics.qmd`
- `_quarto.yml`, `website.navbar.left`, after the pages exist
- `index.qmd`, for links from the homepage
- Existing post files only when adding cross-links manually

### Implementation sketch
```yaml
---
title: "Healthcare Analytics"
description: "Articles on healthcare data, hospital readmissions, risk adjustment, and practical analytics workflows."
listing:
  contents: ../post
  categories:
    - Healthcare
    - Readmissions
  type: default
  sort: "date desc"
---
```

Then add 2 to 4 paragraphs above the listing explaining the pillar in plain language.

### Sequential implementation steps
1. Create `topics/healthcare-analytics.qmd` first because the strongest topical cluster appears to be healthcare/readmissions.
2. Add a short introduction describing what readers will learn and when the material is useful.
3. Add 3 to 5 manually curated "Start with these" links above the listing.
4. Preview the page locally.
5. Repeat for `statistical-thinking`, then `r-shiny`, then `ai-for-analytics`.
6. Add the topic pages to the navbar only after the first 2 or 3 are ready.

### Risk / possible site issues
Quarto category filtering inside listing pages can be sensitive to relative paths and exact category spelling. The site currently uses both `Web Applications` and `Web applications`, which may split results unexpectedly.

### How to verify
Run `quarto preview` and inspect each hub. Confirm that listings render, links work, and the page title/description appear in the rendered HTML metadata.

## Recommendation 2: Standardize Pillar Categories Without Removing Existing Tags

### Purpose
Consistent categories improve archive navigation, feed usefulness, topic landing pages, and machine interpretation of the site's main themes.

### Current issue
Posts use many categories, but the vocabulary is not fully normalized. Examples observed in `post/*/index.qmd` include `Web Applications` and `Web applications`, `Javascript` rather than `JavaScript`, and separate but related labels such as `Modeling`, `Prediction`, `Regression`, and `Estimation`.

### Suggested change
Adopt a two-layer category convention:

- Pillar category: broad reader-facing topic, such as `Healthcare Analytics`, `Statistical Thinking`, `R / Shiny`, `Data Science Infrastructure`, `AI for Analytics`
- Specific tags: narrower concepts, such as `Readmissions`, `Regression`, `Causal Inference`, `DuckDB`, `JavaScript`, `Deployment`

Do this incrementally when updating posts rather than all at once.

### Where to implement
- `post/*/index.qmd`, `categories:` front matter
- Future topic hub pages in `topics/`
- Any future `start-here.qmd`

### Implementation sketch
```yaml
categories:
  - Healthcare Analytics
  - Readmissions
  - R / Shiny
```

### Sequential implementation steps
1. Create a short category style guide in your own notes before editing posts.
2. Start with 5 high-traffic or high-value posts.
3. Add one broad pillar category while keeping existing specific labels.
4. Normalize obvious spelling/case variants, especially `Web Applications` and `JavaScript`.
5. Check the category pages after each small batch.

### Risk / possible site issues
Changing categories changes Quarto category archive URLs and may alter listing counts. Existing category links from search engines could become less useful if old category names disappear, so keep important old specific categories when possible.

### How to verify
Preview the homepage and click category links from the listing cards. Confirm the expected posts appear under each category.

## Recommendation 3: Create A "Start Here" Reader Path

### Purpose
A Start Here page gives first-time readers a guided path through the best material. It helps SEO by creating a strong internal linking page, and it helps AI search summarize the site's expertise more accurately.

### Current issue
The current site has `about.qmd`, `presentations.qmd`, `publications.qmd`, and a chronological/filterable homepage listing. There is no curated path for readers who ask, "What should I read first?"

### Suggested change
Create `start-here.qmd` with a short audience statement, topic sections, and 3 to 5 recommended posts per section. Make it editorially curated rather than another raw listing.

### Where to implement
- New `start-here.qmd`
- `_quarto.yml`, navbar
- `index.qmd`, homepage link
- `about.qmd`, optional link from the bio

### Implementation sketch
```markdown
---
title: "Start Here"
description: "A curated guide to the best Zajichek Stats articles on healthcare analytics, statistical thinking, R/Shiny, and AI-assisted analytics."
---

## Healthcare Analytics

- [A prediction system for managing the hospital readmission risk pool](post/managing-the-readmission-risk-pool/)
- [Building a filterable map with leaflet and crosstalk for hospital readmissions](post/filterable-maps/)
```

### Sequential implementation steps
1. Choose 12 to 18 cornerstone posts.
2. Group them under 4 to 5 topic headings.
3. Add one sentence under each link explaining why it is a good starting point.
4. Add `Start Here` to the navbar after `Projects & Presentations` or before it.
5. Link to the page from the homepage intro.

### Risk / possible site issues
Manual links can break if post slugs change. Use relative links and verify after preview.

### How to verify
Preview the site and click every link on `start-here.qmd`. Also check that the page appears in site search.

## Recommendation 4: Clarify The Site's Positioning Around CentralStatz

### Purpose
The site can support consulting/business discovery without making every article feel salesy. Clear positioning helps readers understand that the blog is both a technical writing archive and evidence of practical consulting capability.

### Current issue
`_quarto.yml` links to `https://www.centralstatz.com/` as `Consultancy`, and `about.qmd` says "Need statistical help?" with a consultancy link. Individual posts occasionally link to CentralStatz repositories and resources, but there is no consistent, subtle positioning system.

### Suggested change
Use three levels of business connection:

- Global: navbar/footer link to CentralStatz
- Biographical: about page explains the relationship between Alex Zajichek, Zajichek Stats, and CentralStatz
- Contextual: posts that clearly relate to applied consulting include a short, optional callout near the end

### Where to implement
- `_quarto.yml`, navbar/footer
- `about.qmd`
- Selected high-value posts under `post/`
- Possible new `start-here.qmd`

### Implementation sketch
```markdown
::: {.callout-note}
For applied work in healthcare analytics, Shiny applications, or statistical consulting, see [CentralStatz](https://www.centralstatz.com/).
:::
```

### Sequential implementation steps
1. Update the about page manually to explain CentralStatz in one concise paragraph.
2. Add a footer link or short footer text if desired.
3. Add contextual callouts only to posts where the consulting link feels natural, such as Shiny deployment, hospital readmission analytics, or statistical project planning.
4. Avoid adding CTAs to purely historical/philosophical posts unless there is a clear fit.

### Risk / possible site issues
Too many CTAs can reduce trust. Keep the tone informational and sparse.

### How to verify
Preview a few posts and ask whether the CentralStatz link feels like a natural next step rather than an interruption.
