# BuyerGuide India — Jekyll site

Honest product reviews for Indian buyers. Built with Jekyll + the [minima](https://github.com/jekyll/minima)
theme, deployed to GitHub Pages at **buyerguideindia.online**.

## Local development

```bash
cd website
bundle install
bundle exec jekyll serve --livereload
```

Visit `http://localhost:4000`.

## Content structure

Content lives in three collections instead of the default `_posts/`:

| Collection      | Folder            | URL pattern              | Layout      |
|------------------|--------------------|---------------------------|-------------|
| Product reviews  | `_reviews/`        | `/reviews/:slug/`         | `review`    |
| Comparisons      | `_comparisons/`    | `/comparisons/:slug/`     | `comparison`|
| Top 5 roundups   | `_roundups/`       | `/roundups/:slug/`        | `roundup`   |

The layout is applied automatically via `defaults` in `_config.yml`, so you
only need to fill in front matter fields, not set `layout:` yourself.

A `roundup` article does not have to use the structured `products:` front
matter array — see `_roundups/top-5-dashcams-for-cars-in-india-2026.md` for
an article written as plain Markdown body content (table + inline "Buy Now"
HTML buttons) with only `title`, `date`, `description`, and `category` set
in front matter.

### Affiliate links

Every review/comparison/roundup product entry sets an `asin` (and,
optionally, a per-product `affiliate_tag`). The `affiliate-button.html`
include builds the link as:

```
https://www.amazon.in/dp/{asin}?tag={affiliate_tag or site.affiliate_tag}
```

Set your real Amazon Associates tag in `_config.yml` (`affiliate_tag:`).

### Never fabricate data

If a price, rating, or spec is unavailable, leave the front matter field as
`null` — the layouts render "Price unavailable" / "Rating unavailable"
rather than inventing a number.

## Publishing to GitHub Pages (repo: buyerguideindia-site)

This `website/` folder is meant to become the **root** of its own GitHub
repository, `buyerguideindia-site` — not stay nested as a subfolder.

1. Create an empty GitHub repository named `buyerguideindia-site`.
2. Push the *contents* of this `website/` folder to that repo's root
   (so `_config.yml`, `Gemfile`, `CNAME`, and `.github/` all sit at the
   repo root there).
3. In the repo, go to **Settings → Pages → Build and deployment** and set
   **Source** to **GitHub Actions**. The included
   `.github/workflows/deploy.yml` will build and deploy on every push to
   `main`.
4. In **Settings → Pages → Custom domain**, enter `buyerguideindia.online`
   and enable **Enforce HTTPS** once the certificate is issued. GitHub
   reads the `CNAME` file automatically, but setting it in the UI as well
   ensures it isn't overwritten by a future build.

### DNS records for buyerguideindia.online

At your domain registrar, point the domain at GitHub Pages:

- `A` records for the apex domain (`buyerguideindia.online`) →
  `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- `CNAME` record for `www` → `<your-github-username>.github.io`

DNS propagation can take up to 24 hours; GitHub will show a checkmark on
the Pages settings page once it verifies the domain.

## SEO

- `jekyll-seo-tag` renders `<title>`, meta description, Open Graph, and
  Twitter Card tags from front matter / `_config.yml`.
- `jekyll-sitemap` generates `/sitemap.xml` automatically at build time.
- `/robots.txt` points crawlers at the sitemap.

## Customising the look

`assets/main.scss` imports the minima base stylesheet and layers site-specific
rules on top (cards, affiliate buttons, spec tables, star ratings). Edit
that file rather than minima's own Sass partials.
