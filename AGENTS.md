# Repository Guidelines

## Project Structure & Module Organization
The site is a Jekyll project. `_pages` holds static pages, `_posts` contains dated blog entries following `YYYY-MM-DD-title.md`, `_includes` and `_layouts` gather Liquid partials and templates, `_sass` centralizes theme variables and mixins, and `assets/` stores images, scripts, and compiled CSS. `_site/` is generated output—never edit or commit it manually. Site-specific overrides (favicon, feeds, analytics) sit at the repo root, while `docker-compose.yml` lets you spin up a containerized dev stack.

## Build, Test, and Development Commands
`bundle install` resolves Ruby gems declared in `Gemfile`. `bundle exec jekyll serve --livereload` runs the local dev server on port 4000 in watch mode; `docker compose up` provides the same workflow inside the official Jekyll image. `JEKYLL_ENV=production bundle exec jekyll build` emits optimized assets into `_site`. Run `bundle exec jekyll doctor` after structural changes to catch config mistakes.

## Coding Style & Naming Conventions
Use two spaces for YAML front matter and Liquid blocks, and Markdown headings that mirror article titles. Blog posts are named `YYYY-MM-DD-slug.md` with descriptive slugs matching the `permalink`. Favor semantic HTML, `include` partials, and front-matter toggles instead of inline JavaScript. Global SCSS belongs in `_sass` and should be imported through `assets/css/styles.scss`; group variables by feature and annotate non-obvious overrides with short comments.

## Testing & QA Guidelines
Automated tests are not provided, so every change must at least pass `bundle exec jekyll build --trace`. Inspect the generated `_site` (or `http://localhost:4000`) to verify navigation, code blocks, and Umami analytics snippets. When editing `_posts`, check for broken images or relative links via the browser console, then rebuild to confirm no Markdown or Liquid warnings surface.

## Commit & Pull Request Guidelines
Commits follow the existing `type: concise summary (#issue)` pattern (`fix: Removed environment check for analytics (#14)` is the reference). Scope each commit to one logical change and include before/after screenshots whenever layouts shift. Pull requests must describe the motivation, list affected URLs or components, mention required `_config.yml` updates, and link to issues. Request a review before merging and wait for any CI build to finish.

## Security & Configuration Tips
Secrets and analytics keys live in `_config.yml`; do not commit real credentials—prefer `_config.dev.yml` overrides ignored by Git. Run production builds with `JEKYLL_ENV=production bundle exec jekyll build` so third-party scripts use production IDs. Clean `_site` before packaging (`rm -rf _site && bundle exec jekyll build`) to avoid shipping stale files.
