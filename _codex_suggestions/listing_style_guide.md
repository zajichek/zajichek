# Listing Style Guide

Use this as a lightweight convention for Quarto listing pages on this site.

## Homepage Listing

The homepage should remain the broad chronological archive.

Recommended options:

```yaml
listing:
  contents: post
  sort: "date desc"
  type: default
  filter-ui: true
  sort-ui: true
  image-align: left
  image-placeholder: "icon.png"
  categories: true
  feed: true
```

## Topic Hub Listings

Topic hubs should use explicit post paths so each hub stays curated.

Recommended options:

```yaml
listing:
  contents:
    - ../post/example-post/index.qmd
  type: default
  sort: "date desc"
  image-align: left
  categories: true
```

## When Adding A New Post

- Decide whether the post belongs on `start-here.qmd`.
- Decide whether the post belongs in one or more topic hubs.
- Add one broad pillar category where appropriate.
- Keep existing specific categories useful for filtering.
- Confirm the homepage listing and topic hub listing both render as expected.

## Current Pillar Categories

- `Healthcare Analytics`
- `Statistical Thinking`
- `Reproducible Analytics`
- `R / Shiny`
- `AI for Analytics`
- `Data Science Infrastructure`
