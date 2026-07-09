# Blog Post Template and SEO Recommendations

## Recommendation 1: Add Direct-Answer Introductions To High-Value Posts

### Purpose
AI search systems and readers both benefit from direct, concise answers near the top of an article. This improves summarization, featured-snippet potential, and reader trust.

### Current issue
Several posts begin conversationally or with background. For example, `post/building-an-llm-powered-shiny-app-for-hospital-readmissions/index.qmd` starts with a video and exploratory context before a direct answer to what the post teaches. That tone is engaging, but the page could be easier for AI/search systems to summarize.

As of the July 2026 review, there are also newer AI/data-science workflow drafts, including `post/sweet-spot-for-ai-coding-assistants-in-data-science-work/index.qmd` and `post/why-an-estimand-for-flux/index.qmd`, that should receive this treatment before publication.

### Suggested change
For cornerstone posts, add a short "In brief" or direct-answer paragraph after the front matter and before long background, videos, or code.

### Where to implement
- Selected `post/*/index.qmd`
- Start with healthcare, AI/Shiny, and statistical decision-making posts

### Implementation sketch
```markdown
**In brief:** This article shows how to build a Shiny application that lets users filter hospital readmission data with natural language. The app uses R, Shiny, `ellmer`, and `querychat` to translate user prompts into SQL-style data queries without sending raw data to the LLM.
```

### Sequential implementation steps
1. Choose 5 cornerstone posts.
2. Add a 2 to 4 sentence direct-answer intro to each.
3. Keep the original voice after the intro.
4. Check that the intro includes the primary keywords naturally.
5. Preview each post.

### Risk / possible site issues
The main risk is making posts feel formulaic. Keep the intro short and specific.

### How to verify
Read the first screen of each post and confirm a new reader can tell what the article answers without scrolling.

## Recommendation 2: Improve Post Descriptions For Search Snippets

### Purpose
The `description` field is important for listings, social previews, and search snippets. It should describe the article's substance, not only the author's motivation.

### Current issue
Many post descriptions are present but short or vague. Examples observed:

- `post/deriving-a-bernoulli-mle/index.qmd`: "Trying to remember calculus"
- `post/bernoullis-fallacy-of-the-transposed-conditional/index.qmd`: empty description
- `post/tips-on-creating-your-own-shiny-server/index.qmd`: "Incolcating ambuguity and poor practice", which appears typo-heavy and unrelated to Shiny Server
- `post/objectifying-statistics/index.qmd`: "Incolcating ambuguity and poor practice", with spelling issues

### Suggested change
Use descriptions of roughly 120 to 160 characters that state the concept, audience, and payoff.

### Where to implement
- `description:` in `post/*/index.qmd`

### Implementation sketch
```yaml
description: "A step-by-step derivation of the Bernoulli maximum likelihood estimator, with the calculus and intuition shown explicitly."
```

### Sequential implementation steps
1. Audit published posts first.
2. Replace empty, typo-heavy, or overly vague descriptions.
3. Keep draft post descriptions updated before publishing.
4. Preview the homepage listing to see how descriptions read in cards.

### Risk / possible site issues
Descriptions with quotes or colons may need YAML quoting. Keep them in double quotes or avoid complex punctuation.

### How to verify
Preview the homepage and a few post pages. Inspect rendered HTML if needed to confirm descriptions appear in metadata.

## Recommendation 3: Add Consistent Post Metadata Defaults

### Purpose
Consistent metadata improves author attribution, table of contents behavior, social cards, and listing quality while reducing repeated front matter.

### Current issue
`post/_metadata.yml` only sets `freeze: true`. Each post repeats `author`, image, code-fold, code-tools, and sometimes `toc`. There is no shared post metadata for author, default image behavior, citation/date formatting, or table of contents.

### Suggested change
Add sensible defaults in `post/_metadata.yml`, then override per post only when needed.

### Where to implement
- `post/_metadata.yml`
- Individual post files for exceptions

### Implementation sketch
```yaml
freeze: true
author: "Alex Zajichek"
image: "feature.png"
format:
  html:
    code-fold: true
    code-tools: true
    toc: true
    toc-depth: 3
```

### Sequential implementation steps
1. Add only one default at a time.
2. Start with `author`, since it is repeated consistently.
3. Consider `code-fold` and `code-tools` next.
4. Preview posts with and without code to ensure the page chrome still feels right.
5. Remove duplicated per-post fields only after verifying behavior.

### Risk / possible site issues
Changing defaults can affect every post. Some posts may not need a table of contents or code tools, so use cautious defaults and override exceptions.

### How to verify
Render a sample of short, long, code-heavy, and non-code posts. Confirm metadata, TOC, and code controls behave as expected.

## Recommendation 4: Add Related-Reading Blocks To Cornerstone Posts

### Purpose
Internal links help readers continue through a topic, distribute authority across related articles, and make the site's knowledge graph clearer for AI search.

### Current issue
Some posts already link to prior work naturally, such as `post/ai-assisted-shiny-development-in-positron/index.qmd` linking to the LLM-powered Shiny post. But there is no consistent related-reading pattern at the bottom of posts.

### Suggested change
Add manual related-reading blocks to cornerstone posts. Keep them short and topic-specific.

### Where to implement
- Bottom of selected `post/*/index.qmd`
- Topic hub pages for reciprocal links

### Implementation sketch
```markdown
## Related Reading

- [Making an AI statistical consultant](../making-an-ai-statistical-consultant/)
- [Building a custom LLM-powered Shiny app for hospital readmissions](../building-an-llm-powered-shiny-app-for-hospital-readmissions/)
- [Low cost ways to build and deploy analytical web apps](../low-cost-ways-to-build-and-deploy-apps/)
```

### Sequential implementation steps
1. Create related-reading blocks for 5 cornerstone posts.
2. Use 3 to 5 links per post.
3. Prefer strong topical links over generic "recent posts".
4. Add reciprocal links from topic hubs.
5. Recheck links after rendering.

### Risk / possible site issues
Relative links from nested post directories can be easy to mistype. Use local preview and click testing.

### How to verify
Preview each post and click every related link. Confirm no related link points to a draft or unpublished page.

## Recommendation 5: Add FAQ-Style Sections Only Where They Fit

### Purpose
FAQ sections can improve AI-search discoverability because they use direct questions and answers. They are especially useful for tutorial, definition, and decision-oriented posts.

### Current issue
Long technical posts contain valuable explanations but not always in question-answer form. For example, the Shiny/LLM, readmissions, and statistical significance posts have concepts readers may search as direct questions.

### Suggested change
Add a brief `## Frequently Asked Questions` or `## Common Questions` section to selected posts. Use 3 to 5 real questions, not filler.

### Where to implement
- Selected `post/*/index.qmd`

### Implementation sketch
```markdown
## Common Questions

### Does querychat send my raw dataset to the LLM?

No. In this setup, the LLM receives metadata and context about the dataset, then generates queries that are executed inside the app.
```

### Sequential implementation steps
1. Add FAQ sections to tutorial posts first.
2. Write questions in the language a reader would search.
3. Keep answers concise and link back to the relevant section if the article explains it in detail.
4. Avoid adding FAQ sections to reflective essays unless they genuinely help.

### Risk / possible site issues
FAQ sections can feel artificial if overused. Add them only to posts where they improve clarity.

### How to verify
Read the final section of the post and confirm the FAQ answers common reader questions without repeating the whole article.

## Recommendation 6: Review Draft Status And Publication Metadata Before Publishing

### Purpose
Dates affect RSS feeds, listings, sitemap timing, and reader trust. Draft status, publication date, and descriptions should be intentional before a post becomes public.

### Current issue
As of July 9, 2026, the sampled post dates are not future-dated, but several posts are still marked `draft: true`, including:

- `post/bernoullis-fallacy-of-the-transposed-conditional/index.qmd`
- `post/effective-research-data-science/index.qmd`
- `post/i-am-not-data-driven/index.qmd`
- `post/objectifying-statistics/index.qmd`
- `post/subtle-mistranslations-and-their-aggregated-impact/index.qmd`
- `post/sweet-spot-for-ai-coding-assistants-in-data-science-work/index.qmd`
- `post/tips-on-creating-your-own-shiny-server/index.qmd`
- `post/why-an-estimand-for-flux/index.qmd`

The older recommendation named `post/the-worst-lead-in-hockey/index.qmd` as a draft, but it now appears to be published with a June 4, 2026 date.

### Suggested change
Maintain a quick publication checklist for date, draft status, description, image, categories, and links before publishing a post.

### Where to implement
- Individual post front matter
- Optional local checklist in `_codex_suggestions` or your private notes

### Implementation sketch
```markdown
Publication checklist:
- `draft` removed or set to false
- `date` is the intended publication date
- `description` is specific
- `categories` include one pillar and 1 to 3 specific tags
- `image` exists
- intro answers the reader's question directly
```

### Sequential implementation steps
1. Before publishing, inspect the target post's front matter.
2. Confirm the rendered page appears or stays hidden as intended.
3. Check the homepage listing, RSS feed, sitemap, and any `llms.txt` output after rendering.
4. Check that draft posts remain excluded from public discovery outputs.

### Risk / possible site issues
Changing dates can reorder the homepage and RSS feed. Removing `draft: true` can publish unfinished content and make it eligible for generated discovery files.

### How to verify
Render the site and inspect the homepage listing, `index.xml`, `_site/sitemap.xml`, and `_site/llms.txt` if LLM output is enabled.
