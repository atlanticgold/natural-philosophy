# Natural Philosophy

*The study of things as they are.*

A static philosophical journal built with Jekyll and hosted on GitHub Pages. Essays are Markdown files with a small YAML front matter block — no HTML editing, no database, no CMS.

## Publishing a New Essay

1. Add a file to `_posts/` named `YYYY-MM-DD-your-title.md`.
2. Give it this front matter:

   ```yaml
   ---
   layout: post
   title: "Your Essay Title"
   date: 2026-09-14
   description: "One sentence, shown wherever the essay is listed."
   ---
   ```

3. Write the essay in Markdown below it.
4. Commit and push to `main`.

That's it. The homepage, the archive, and the essay's own page are all generated automatically — there's nothing else to update.

For images, math, or linking to other essays, see **Writing an Essay** below.

## What This Is

A minimal, text-first publishing setup: write an essay in Markdown, push, it's live. No JavaScript framework, no build step you need to think about beyond Jekyll itself. Three example essays ship with the project to show the format working end to end (including one that links to the other two) — delete or replace them whenever you like.

## Project Structure

```
_config.yml              Site title, tagline, and deployment settings
_posts/                  One Markdown file per essay — this is what you edit
about.md                 The About page (same format as an essay)
index.html               Homepage
archive.html             Full archive, grouped by year
categories.html          All essays grouped by category
tags.html                All essays grouped by tag
search.html              Search page
search.json              Search index, generated from site.posts — not hand-edited
feed.xml                 RSS feed, generated from site.posts — not hand-edited
_layouts/                Page templates (see "Layouts and Includes" below)
_includes/               Shared template snippets
assets/css/style.css     All site styling
assets/images/           Images referenced from essays
.github/workflows/       The GitHub Actions deployment workflow
```

## Writing an Essay

**Standard Markdown** works throughout: headings, paragraphs, lists, `> ` blockquotes, `[links](url)`, and fenced code blocks.

**Images** — place the file under `assets/images/` and reference it without a leading slash:

```markdown
![Alt text](assets/images/your-image.svg)
```

**Math** — wrap LaTeX in double dollar signs. On its own line, it's a displayed equation; inline in a sentence, it's inline math:

```markdown
An inline example: $$x^2 + y^2 = z^2$$ in the middle of a sentence.

$$
x^2 + y^2 = z^2
$$
```

**Linking to another essay** — an essay can mark itself as a **Response** to another essay (challenges or disagrees with it) and/or an **Addition** to another essay (builds on it). Add either to the front matter as a list of the target essay's filename, without `.md`:

```yaml
responses:
  - "2026-09-11-on-first-principles"
additions:
  - "2026-09-12-kinds-and-their-boundaries"
```

The linked essay's real title and URL are looked up automatically — you never type them by hand. If a field is empty or omitted, nothing extra is shown.

**Footnotes, citations, and a bibliography** — this is plain Markdown, nothing new to configure:

```markdown
Perception may be direct pickup rather than inference (Gibson 1979).[^1]

[^1]: A longer aside or the full citation detail goes here.

## References
{: .essay-bibliography}

- Gibson, J.J. *The Ecological Approach to Visual Perception*. Houghton Mifflin, 1979.
- ["Kinds and Their Boundaries"]({% post_url 2026-09-12-kinds-and-their-boundaries %}), *Natural Philosophy*.
```

A `[^1]` marker and matching `[^1]: text` definition (they can go anywhere in the file, not just at the bottom) render as a numbered, linked note at the end of the essay automatically — this is core Markdown, not a plugin. An inline citation like `(Gibson 1979)` is just prose; make it a link only if you want it clickable. The one thing to remember for a References section specifically is the `{: .essay-bibliography}` line directly under its heading — that's what gives it its own visual separation from the essay above it, the same way footnotes get theirs automatically. Reference another essay in your bibliography the same `post_url` way shown above for Response/Addition, or with a plain link if you'd rather.

**Categories and tags** — mark an essay's broad area with `categories` (usually just one) and its more specific concepts, subjects, thinkers, or methods with `tags` (usually several):

```yaml
categories:
  - Epistemology
tags:
  - Recognition
  - Reality
  - Gibson
```

Every value you use automatically appears on the `/categories/` or `/tags/` page, grouped with every other essay that shares it, and each essay links to those pages. There's no separate list to update — just be consistent about spelling and capitalization, since `Epistemology` and `epistemology` would be treated as two different categories.

## Search

The `/search/` page lets readers search by title, description, category, tag, author, or body text — all handled in the browser against `search.json`, a plain-text index rebuilt from `site.posts` on every deploy. There's nothing to maintain here either; it's generated the same way the archive and category pages are.

One thing to set once: `author` in `_config.yml` is currently a placeholder (`"Your Name"`) — change it to whatever byline you want to appear in essays and search results. It's a single site-wide value rather than something you set per essay, since there's currently one author for the whole journal; a per-post override could be added later if that ever changes.

## RSS Feed

The feed lives at **`/feed.xml`** — for this repo, that's `https://atlanticgold.github.io/natural-philosophy/feed.xml`. It's an RSS 2.0 feed generated from `site.posts` on every build, so a new essay appears in it automatically; there's no separate feed content to write or update. Each entry carries the essay's title, publish date, description, absolute URL, author, and its categories/tags as feed categories. Every page also links to it via a `<link rel="alternate">` tag in the page head, so browsers and feed readers can discover it automatically without needing the URL typed in by hand.

## Previewing Locally

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

Search specifically needs this — opening a built HTML file directly in a browser (rather than through `jekyll serve` or the live site) can't fetch `search.json`, since browsers block that for local files.

## Publishing Changes

Any change — a new essay, an edit to `about.md`, a CSS tweak — is published the same way: commit and push to `main`. There's no separate deploy step to run yourself.

## How GitHub Pages Deploys the Site

Pushing to `main` triggers the workflow in `.github/workflows/pages.yml`, which builds the site with Jekyll and publishes it — usually within a minute or two. You can watch it run under the repo's **Actions** tab.

`_config.yml` is already set for this repo (`atlanticgold/natural-philosophy`, deployed at `https://atlanticgold.github.io/natural-philosophy/`). If you ever fork or rename this repo, update `url`/`baseurl` there to match — the live deployment auto-detects the correct path on its own regardless, but `_config.yml` is what a local `bundle exec jekyll serve` uses to match it.

## Where the CSS Lives

Everything is in the single file `assets/css/style.css`. There's no preprocessor or build step for styles — edit it directly and refresh.

## Where the Layouts Live

`_layouts/` holds the three page templates:

- `default.html` — the outer HTML shell every page shares (used by the other two layouts)
- `page.html` — used by `about.md` and `archive.html`
- `post.html` — used by every essay

`_includes/` holds smaller pieces reused across pages: `header.html` (site title and nav), `footer.html`, `essay-relations.html` (the Response/Addition sections on an essay page), and `essay-list-item.html` (one essay entry — shared by the homepage, archive, categories, and tags pages so they can't drift out of sync with each other).
