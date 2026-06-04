# Visual Design and Readability Recommendations

## Recommendation 1: Reduce Decorative Font Usage In Navigation And Homepage Intro

### Purpose
Readable typography improves user experience, accessibility, and perceived professionalism. It also makes the site feel more modern without changing the Quarto foundation.

### Current issue
`styles.scss` applies `font-family: Copperplate, fantasy`, larger size, and oblique style to navbar link text. `index.qmd` also uses inline HTML with `font-family: Copperplate, fantasy`. This creates a distinctive style, but it can reduce readability and make navigation feel less contemporary.

### Suggested change
Use Quarto/Bootstrap's standard sans-serif font for navigation and reserve distinctive branding for the logo. Replace inline homepage font styling with Markdown headings and optional modest CSS classes.

### Where to implement
- `styles.scss`
- `index.qmd`

### Implementation sketch
```scss
.navbar li.nav-item a.nav-link span {
  color: #004163 !important;
  font-size: 1rem;
  font-style: normal;
}
```

### Sequential implementation steps
1. Remove the homepage inline HTML slogan and replace it with Markdown.
2. Adjust navbar font styles in `styles.scss`.
3. Preview the navbar with all current links.
4. Check mobile menu readability.

### Risk / possible site issues
The site may feel less branded at first if the decorative font is removed. The logo can carry most of the brand identity instead.

### How to verify
Preview the homepage and at least one post. Confirm the navbar feels calmer and easier to scan.

## Recommendation 2: Reconsider The Fixed Background Image

### Purpose
Fixed backgrounds can distract from long-form reading and may perform poorly on mobile. A simpler background often makes technical articles easier to read.

### Current issue
`styles.scss` sets `body` to use `background.png` with `background-attachment: fixed`. This applies globally across the site.

### Suggested change
Limit the background image to the homepage or remove the fixed attachment. Let posts use a plain reading background.

### Where to implement
- `styles.scss`
- Possibly `index.qmd` with a homepage-specific class if needed

### Implementation sketch
```scss
body {
  background-image: none;
}

.home-intro {
  /* optional subtle homepage-only treatment */
}
```

### Sequential implementation steps
1. Test the site with the background disabled locally.
2. If the simpler design feels better, remove global background usage.
3. If you want to keep it, apply it only to homepage-specific sections.
4. Check posts with long code blocks and tables.

### Risk / possible site issues
Removing the background changes the site's visual identity. Do this only after comparing screenshots.

### How to verify
Preview a long post, a short post, homepage, about page, and publications page. Confirm readability improves.

## Recommendation 3: Normalize Article Heading Levels

### Purpose
Semantic heading structure helps readers scan, improves accessibility, and makes AI/search extraction more reliable.

### Current issue
Many posts use `#` headings inside the article body after the page title is already provided by front matter. For example, `post/building-an-llm-powered-shiny-app-for-hospital-readmissions/index.qmd` uses `# The App`, `# Some Background on Readmissions`, and `# Code summary`.

### Suggested change
Use `##` for main sections inside posts and `###` for subsections. Keep the page title as the only H1.

### Where to implement
- `post/*/index.qmd`
- Start with cornerstone posts rather than all posts at once

### Implementation sketch
```markdown
## The App

## Some Background On Readmissions

### Penalty Calculation
```

### Sequential implementation steps
1. Pick one long cornerstone post.
2. Change body-level `#` headings to `##`.
3. Change child headings accordingly.
4. Render and inspect the table of contents.
5. Repeat gradually.

### Risk / possible site issues
Changing headings can alter auto-generated anchor links. If external links point to old anchors, preserve important anchors with explicit IDs.

### How to verify
Preview the post and click TOC entries. Check any known external links to section anchors.

## Recommendation 4: Improve Listing Card Scannability

### Purpose
Better listing cards make the homepage and topic hubs easier to scan, especially as the archive grows.

### Current issue
`index.qmd` uses Quarto's default listing with images aligned left, filter UI, sort UI, placeholder image, categories, and feed. This is functional, but the page lacks a curated hierarchy above the listing.

### Suggested change
Keep Quarto listings, but add curated homepage sections above them and optionally use small CSS improvements for listing spacing and card text.

### Where to implement
- `index.qmd`
- `styles.scss`
- Future `topics/*.qmd`

### Implementation sketch
```scss
.quarto-listing-default .listing-title {
  font-weight: 700;
}

.quarto-listing-default .listing-description {
  line-height: 1.45;
}
```

### Sequential implementation steps
1. Add Featured and Topics sections above the listing.
2. Preview before changing CSS.
3. Make only small CSS adjustments if card text still feels hard to scan.
4. Check that category badges remain readable.

### Risk / possible site issues
Quarto listing class names can vary by version or listing type. Inspect rendered HTML if a CSS rule does not apply.

### How to verify
Preview the homepage and verify cards remain readable at desktop and mobile widths.

## Recommendation 5: Use Callouts For Definitions, Summaries, And Contextual CTAs

### Purpose
Callouts help readers identify key ideas in long technical articles without adding custom JavaScript or complex components.

### Current issue
Long posts contain many valuable explanations, but key definitions and practical takeaways are often embedded in normal prose. For example, readmission posts define HRRP concepts and model mechanics that would benefit from more visible summary blocks.

### Suggested change
Use Quarto callouts sparingly for definitions, summaries, and contextual CentralStatz links.

### Where to implement
- Selected `post/*/index.qmd`

### Implementation sketch
```markdown
::: {.callout-tip}
## Key Idea
The excess readmission ratio compares a hospital's predicted readmission rate with its expected readmission rate after risk adjustment.
:::
```

### Sequential implementation steps
1. Add 1 to 2 callouts to one long healthcare article.
2. Use them for genuinely important definitions or takeaways.
3. Avoid placing callouts every few paragraphs.
4. Preview the post and check visual balance.

### Risk / possible site issues
Too many callouts can make articles feel fragmented. Use them as signposts, not decorations.

### How to verify
Read the article in full and confirm the callouts improve comprehension without interrupting flow.

## Recommendation 6: Make The About Page More Credibility-Oriented

### Purpose
The about page is important for reader trust, E-E-A-T style credibility signals, and business positioning. It should connect expertise, publications, professional experience, and CentralStatz clearly.

### Current issue
`about.qmd` has a concise bio, social links, experience, and education. It is accurate but minimal. It does not point readers to key topics, selected publications, or a Start Here path.

### Suggested change
Add short sections for "What I write about", "Selected expertise", and "Working with me / CentralStatz". Keep the current experience and education sections.

### Where to implement
- `about.qmd`
- `publications.qmd`, if linking to selected publications
- Future `start-here.qmd`

### Implementation sketch
```markdown
## What I Write About

I write about practical statistical decision-making, healthcare analytics, reproducible workflows, R/Shiny applications, and data science infrastructure.

For a curated path through the site, start with [Start Here](start-here.qmd).
```

### Sequential implementation steps
1. Add a short paragraph connecting Alex's professional background to the blog topics.
2. Link to Start Here and 2 or 3 topic hubs.
3. Add a concise CentralStatz paragraph.
4. Keep the experience list intact.

### Risk / possible site issues
The about page can become too long if it tries to duplicate the publications page. Link out rather than copying too much.

### How to verify
Preview the about page and confirm it answers: who Alex is, why readers should trust him, what he writes about, and how CentralStatz fits.
