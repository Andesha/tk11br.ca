# New-post update checklist

When you add a post under `content/posts/*.md`, the post file is not the only
surface that may need to change. Some surfaces update themselves from front
matter; others are hand-curated and only change if you edit them. Work through
this list for every new post and decide **fits / does not fit** for each curated
surface — do not add a post everywhere by reflex.

## 1. Front matter (always)

Set these in the post's front matter (`archetypes/default.md` is the starting
template):

- `title`, `subtitle`, `description`, `date`, `tags`.
- **`description` is required.** The homepage build (`layouts/index.html`) fails
  with `Missing description in <path>` if any post lacks one.
- **`draft: true` hides the post everywhere.** Set `draft: false` to publish.
- **`tags` do real work** — see the automatic surfaces below.

## 2. Automatic surfaces (no edit needed — just get front matter right)

These regenerate from front matter. You do not touch them; you only confirm the
post shows up as expected.

- **Homepage "Latest post" and "Recent posts"** — newest posts by `date`.
- **Homepage "Recorded talks" and the Talks page list** — any post whose `tags`
  include `talk` is listed automatically (`layouts/index.html` and the
  `talks-list` shortcode). Tag a talk with `talk` rather than hand-adding it.
- **Tag landing pages** (`/tags/<tag>/`) — generated from `tags`. Keep tag
  spelling consistent with the vocabulary below.

### Tag vocabulary

Prefer established tags instead of creating near-duplicates:

- `talk` — recorded presentations only; drives the Talks surfaces.
- `python` — Python is a substantial topic.
- `hpc` — high-performance computing.
- `performance` — profiling or optimization.
- `scheduling` — cluster schedulers and job submission.
- `eeg` — EEG research or processing.
- `bids` — Brain Imaging Data Structure.
- `preprocessing` — data-cleaning and preprocessing pipelines.
- `workflow` — reproducible research workflows.

Named technologies and projects may be used when they are central to a post.
Use official capitalization, such as `Cython`, `PyLossless`, `EEGStudyFlow`,
and `ViewClust`; keep officially lowercase names such as `pandas` lowercase.
Avoid tags for incidental mentions. Add a new general-purpose tag only when it
would remain useful for grouping this post with current or likely future posts.

The post front matter is the authoritative tag inventory; this list documents
reusable general tags rather than every named project.

## 3. Curated surfaces (decide fits / does not fit, then edit if it fits)

These are hard-coded. A new post only belongs here if it genuinely fits.

- **Homepage "Highlighted projects"** (`layouts/index.html`) — three hand-picked
  project cards. Edit only if the post is a flagship project worth featuring.
- **Homepage "Quick links"** (`layouts/index.html`) — links to top-level
  resource pages, not posts. Edit only if you also added a new top-level
  resource page under `content/`.
- **Projects page** (`content/projects/_index.md`) — prose sections per project.
  Edit if the post represents or updates a project described here.
- **Talks page "Publications"** (`content/talks/_index.md`) — edit if the post is
  a publication (the recorded-talks list above is automatic).

## 4. Per-post review block (copy-paste into the PR/commit description)

```
New-post surfaces reviewed for <post-slug>:
- Front matter (description set, draft flipped, tags): updated
- Highlighted projects (homepage):        fits / does not fit — [updated | skipped]
- Quick links (homepage):                 fits / does not fit — [updated | skipped]
- Projects page (_index.md):              fits / does not fit — [updated | skipped]
- Talks page Publications (_index.md):    fits / does not fit — [updated | skipped]
- Talk tag applied (if a talk):           yes / n/a
```

## 5. Build check (always)

Run the build and confirm it passes and the affected pages look right:

```
hugo --minify
```

A missing `description` or a broken internal `ref`/`relref` will surface here.
