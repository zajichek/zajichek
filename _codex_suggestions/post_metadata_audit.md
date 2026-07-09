# Post Metadata Audit

Audit date: 2026-07-09

This report intentionally does not change post content. It lists metadata and publishing items to review manually.

## Safe Default Applied

- Added `author: "Alex Zajichek"` to `post/_metadata.yml`.
- No global `image` default was added because some draft folders currently do not contain an actual `feature.png` file.
- No global `toc`, `code-fold`, or `code-tools` defaults were added because those can affect rendering/layout across older posts.

## Posts Missing `description`

- `post/a-look-at-collider-bias/index.qmd`
- `post/nesting-with-tidyr/index.qmd`
- `post/quickly-removing-higher-order-aggregation-text-in-reactable/index.qmd`
- `post/some-takeaways-from-effective-data-storytelling/index.qmd`
- `post/statistical-rethinking-2023-class-notes/index.qmd`

## Posts With Empty Or Placeholder-Like Descriptions

- `post/bernoullis-fallacy-of-the-transposed-conditional/index.qmd`: empty `description`
- `post/objectifying-statistics/index.qmd`: typo-like description, draft
- `post/tips-on-creating-your-own-shiny-server/index.qmd`: typo-like description, draft

## Draft Posts

- `post/bernoullis-fallacy-of-the-transposed-conditional/index.qmd`
- `post/effective-research-data-science/index.qmd`
- `post/i-am-not-data-driven/index.qmd`
- `post/objectifying-statistics/index.qmd`
- `post/subtle-mistranslations-and-their-aggregated-impact/index.qmd`
- `post/sweet-spot-for-ai-coding-assistants-in-data-science-work/index.qmd`
- `post/tips-on-creating-your-own-shiny-server/index.qmd`
- `post/why-an-estimand-for-flux/index.qmd`

## Post Folders Missing Actual `feature.png`

These folders declare `image: "feature.png"` in front matter, but the image file was not found in the folder.

- `post/bernoullis-fallacy-of-the-transposed-conditional`
- `post/objectifying-statistics`
- `post/subtle-mistranslations-and-their-aggregated-impact`
- `post/sweet-spot-for-ai-coding-assistants-in-data-science-work`
- `post/tips-on-creating-your-own-shiny-server`
- `post/why-an-estimand-for-flux`

## Notes For Manual Review

- Keep post descriptions in your own voice.
- Treat description updates as content edits, even though they live in front matter.
- Before publishing any draft, confirm `feature.png` exists and the post renders cleanly.
