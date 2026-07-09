# Post Publication Checklist

Use this before publishing a new post or moving a draft out of draft status.

## Front Matter

- Confirm `title` is final.
- Confirm `description` is present and written in your voice.
- Confirm `author` does not need a post-specific override.
- Confirm `date` is the intended publication date.
- Confirm `draft` is removed or set to `false`.
- Confirm `image: "feature.png"` is present.
- Confirm `feature.png` exists in the post folder.
- Confirm categories include one broad pillar category where appropriate.
- Confirm categories include useful specific tags.

## Rendering

- Run `quarto render`.
- Check the post page in `_site/post/.../index.html`.
- Check the homepage listing card.
- Check the topic hub page if the post belongs in one.
- Check `index.xml` if the post should appear in the RSS feed.
- Check `_site/sitemap.xml` if the post should be public.

## Content Review

- Add any direct-answer introduction, related reading, FAQ, or description improvements manually.
- Keep these edits in your own voice.
- Avoid publishing if placeholder text such as `ADD TEXT ABOUT` remains in the post.
