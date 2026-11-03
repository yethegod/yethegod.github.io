# yethegod.github.io

Academic homepage + blog, built with Jekyll on GitHub Pages (design adapted from Jon Barron's).

## Common edits

| What | Where |
|---|---|
| Bio, links | `index.html` (top section) |
| Profile photo | add `images/profile.jpg` (square works best) |
| Research / projects | `_data/projects.yml` — one entry per row; `highlight: true` gives the yellow background |
| Email / GitHub / LinkedIn | `_config.yml` → `author` |

## Writing a blog post

Create `_posts/YYYY-MM-DD-some-title.md`:

```markdown
---
layout: post
title: "My Post Title"
description: "One-line summary shown on the blog index."
tags: [diffusion, notes]
math: true        # only if the post uses LaTeX
---

Content in Markdown. Inline math $x^2$, display math $$ ... $$.
```

Commit and push — GitHub Pages rebuilds in ~1 minute.

## Local preview (optional)

```bash
docker run --rm -it -p 4000:4000 -v "$PWD":/srv/jekyll -w /srv/jekyll ruby:3.3 \
  bash -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"
```

Then open http://localhost:4000.
