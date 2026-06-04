# Homepage and Navigation Recommendations

## Recommendation 1: Replace The Homepage HTML Slogan With A Semantic Intro Section

### Purpose
The homepage should immediately communicate who the site is for, what topics it covers, why Alex is credible, and where readers should begin. Semantic Markdown also gives search engines and AI systems clearer page structure than centered inline HTML.

### Current issue
`index.qmd` currently has a listing and two raw HTML blocks: a centered paragraph with a Copperplate/fantasy style and an embedded `subscribe.html` iframe. The intro also appears to have a typo: `<b<</p>` instead of a closing bold tag.

### Suggested change
Use normal Markdown headings and short paragraphs before the post listing. Keep the listing, but add a "Start Here" and topic-card area above it.

### Where to implement
- `index.qmd`
- Optional supporting styles in `styles.scss`
- Future `start-here.qmd` and `topics/*.qmd`

### Implementation sketch
```markdown
# Practical Statistics, Healthcare Analytics, and R/Shiny Development

Zajichek Stats is a technical blog for analysts, statisticians, researchers, and healthcare teams who want clearer statistical thinking and more useful analytic products.

[Start Here](start-here.qmd){.btn .btn-primary}
[View Healthcare Analytics](topics/healthcare-analytics.qmd){.btn .btn-outline-primary}
```

### Sequential implementation steps
1. Draft a 2 to 3 sentence homepage intro in Markdown.
2. Add two primary links: `Start Here` and `Healthcare Analytics`.
3. Keep the existing listing below the intro.
4. Move the newsletter iframe lower on the page or replace it with a text link if it visually crowds the first viewport.
5. Preview on desktop and mobile.

### Risk / possible site issues
Button classes depend on Bootstrap styling included by Quarto. The buttons should work, but spacing may need a small `styles.scss` adjustment.

### How to verify
Run `quarto preview`, open the homepage, and confirm the first viewport answers: who this is for, what the site covers, and where to start.

## Recommendation 2: Add A "Start Here" Navbar Link

### Purpose
New readers need a stable entry point that does not depend on publication date. This is especially useful when the homepage listing includes a wide range of topics.

### Current issue
`_quarto.yml` navbar currently links to Projects & Presentations, Publications, Consultancy, About, and Subscribe. There is no reader onboarding link.

### Suggested change
Add `Start Here` near the left side of the navbar after the page exists.

### Where to implement
- `_quarto.yml`, `website.navbar.left`
- New `start-here.qmd`

### Implementation sketch
```yaml
navbar:
  left:
    - href: start-here.qmd
      text: Start Here
```

### Sequential implementation steps
1. Create and preview `start-here.qmd`.
2. Add the navbar link.
3. Confirm the navbar still fits on common desktop widths.
4. Confirm the mobile menu is readable.

### Risk / possible site issues
The current logo has `max-height: 125px` in `styles.scss`, which makes the navbar visually large. Adding another link could increase wrapping or crowding.

### How to verify
Preview at desktop and mobile widths. Check that navbar links do not wrap awkwardly.

## Recommendation 3: Group Topic Hubs Under A Navbar Dropdown

### Purpose
A topic dropdown makes the site's expertise visible without overloading the top-level navigation.

### Current issue
The navigation is page/type oriented: projects, publications, consultancy, about, subscribe. It does not expose the main content themes directly.

### Suggested change
After creating topic hub pages, add a `Topics` dropdown with 4 to 6 entries.

### Where to implement
- `_quarto.yml`, `website.navbar.left`
- `topics/*.qmd`

### Implementation sketch
```yaml
- text: Topics
  menu:
    - href: topics/healthcare-analytics.qmd
      text: Healthcare Analytics
    - href: topics/statistical-thinking.qmd
      text: Statistical Thinking
    - href: topics/r-shiny.qmd
      text: R / Shiny
```

### Sequential implementation steps
1. Create at least two topic pages.
2. Add a `Topics` dropdown with those pages only.
3. Add the remaining topics as they are created.
4. Keep category pages available through post cards rather than making every tag a nav item.

### Risk / possible site issues
Dropdown styling may inherit the current Copperplate/fantasy navbar styles. Inspect readability and hover behavior after adding it.

### How to verify
Preview and click each dropdown item. Confirm the dropdown works with keyboard and mobile menu navigation.

## Recommendation 4: Curate Featured Articles Above The Chronological Listing

### Purpose
Featured articles help readers find the strongest posts quickly and give crawlers stronger signals about cornerstone content.

### Current issue
`index.qmd` currently puts the chronological/filterable listing at the top. That works as an archive, but it does not distinguish the best starting points from recent or draft-adjacent content.

### Suggested change
Add a small "Featured" section above the listing with 3 or 4 cornerstone articles.

### Where to implement
- `index.qmd`
- Optional `styles.scss` for compact feature cards

### Implementation sketch
```markdown
## Featured

- [What decision are we trying to make, anyway?](post/what-decision-are-we-trying-to-make/) - A practical framing for statistical work.
- [A prediction system for managing the hospital readmission risk pool](post/managing-the-readmission-risk-pool/) - Healthcare analytics and readmission strategy.
- [Building a custom LLM-powered Shiny app for hospital readmissions](post/building-an-llm-powered-shiny-app-for-hospital-readmissions/) - AI-assisted analytics in practice.
```

### Sequential implementation steps
1. Pick 3 or 4 posts that best represent the site.
2. Add one-sentence descriptions for each.
3. Put this section before the listing.
4. Refresh featured links quarterly or after major new posts.

### Risk / possible site issues
If featured links point to draft posts, users may not be able to access them depending on render settings. Avoid draft posts until published.

### How to verify
Preview and click each featured link. Confirm each destination is published and appears in the rendered site.

## Recommendation 5: Rework Newsletter Placement

### Purpose
Email capture is useful, but it should not obscure the site's topic and credibility signals on the first screen.

### Current issue
`index.qmd` embeds `subscribe.html` in a centered 300 by 300 iframe immediately after the intro slogan. This may dominate the above-fold experience and is less semantically meaningful than a normal link or concise signup section.

### Suggested change
Move the newsletter embed below the topic/featured sections, or replace it with a simple "Subscribe" text link in the homepage body while keeping the navbar Subscribe link.

### Where to implement
- `index.qmd`
- Existing `subscribe.html`
- `_quarto.yml`, existing Subscribe navbar item

### Implementation sketch
```markdown
## Subscribe

Get new posts on statistics, healthcare analytics, and R/Shiny projects.

[Subscribe by email](https://dashboard.mailerlite.com/forms/1517199/154300987644839168/share){.btn .btn-outline-primary}
```

### Sequential implementation steps
1. Move the iframe lower on the page or replace it with a link.
2. Confirm the navbar Subscribe link still works.
3. If the iframe remains, test it on mobile.

### Risk / possible site issues
Removing the iframe may reduce immediate form visibility, but it can improve homepage clarity and load behavior.

### How to verify
Preview the homepage and check that the subscription path is still easy to find without crowding the intro.
