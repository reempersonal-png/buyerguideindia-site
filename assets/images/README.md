# Article Images

Hero/header images (and any other visuals) used in review, comparison,
and roundup articles live in this folder.

## Naming convention

    <publish-date>-<article-slug>-<descriptor>.<ext>

- `publish-date` — the article's front matter `date`, as `YYYY-MM-DD`
- `article-slug` — a short, hyphenated version of the article's topic
- `descriptor` — what the image is: `hero`, `thumb`, `detail`, etc.
- `ext` — `jpg`, `jpeg`, `png`, or `webp`

Example: the hero image for the 2026-07-15 dashcam roundup would be

    2026-07-15-dashcams-hero.jpg

## Using an image in an article

Set the `image` field in the article's front matter to a site-root-relative
path:

```yaml
---
title: "Top 5 Best Dashcams for Cars in India 2026"
date: 2026-07-15
image: /assets/images/2026-07-15-dashcams-hero.jpg
---
```

When `image` is set:
- The review/comparison/roundup layout displays it as a hero image at the
  top of the article.
- The homepage shows it as the article card's thumbnail.
- `jekyll-seo-tag` uses it as the `og:image` / Twitter Card image for
  social sharing previews.

If `image` is left unset, all three are skipped automatically — no broken
image tags are rendered on the page.

## Guidelines

- Keep images under ~200KB where possible; this is a text-first content
  site, not an image gallery.
- Use a 16:9 or wider aspect ratio so the same image crops well both as a
  full-width hero and as a homepage card thumbnail.
- Never use a manufacturer's or Amazon's product photography without
  checking the applicable image-use terms.
