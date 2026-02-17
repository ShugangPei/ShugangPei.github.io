# Repository Guidelines

## Project Structure & Module Organization
This repository is a Hugo blog using the PaperMod theme.
- `hugo.toml`: site configuration, menus, theme, and output settings.
- `content/`: Markdown content. Put posts in `content/posts/` and standalone pages in `content/about.md`, `content/search.md`, etc.
- `static/`: static files served as-is (for example `static/img/avatar.png`).
- `archetypes/default.md`: template used by `hugo new`.
- `layouts/` and `assets/`: local theme overrides/extensions.
- `themes/PaperMod/`: git submodule; avoid direct edits unless intentionally updating the theme.
- `public/`: generated output from Hugo builds.

## Build, Test, and Development Commands
- `hugo server -D`: run local dev server including draft content.
- `hugo --minify`: production build (same build command used in CI).
- `hugo new content/posts/my-new-post.md`: create a new post from archetype.
- `git submodule update --init --recursive`: initialize/update PaperMod after clone.

## Coding Style & Naming Conventions
- Use Markdown for content and keep filenames in kebab-case (example: `open-source-notes.md`).
- Keep front matter complete: `title`, `date`, `draft`, and optional `tags`/`categories`.
- Prefer concise headings, short paragraphs, and language-tagged fenced code blocks.
- Keep Hugo config formatting consistent with existing files (2-space indentation for nested TOML blocks).

## Testing Guidelines
There is no unit test suite in this repo; validation is build- and preview-based.
- Run `hugo --minify` before opening a PR.
- Run `hugo server -D` and verify updated pages, navigation, tags, and search behavior.
- If you change layouts/assets, manually check desktop and mobile rendering.

## Commit & Pull Request Guidelines
Recent commits follow short, imperative, lowercase messages (for example: `add open-source projects post`, `update about page`).
- Keep commit subjects focused and under ~72 characters.
- PRs should include: purpose, changed paths, and verification steps.
- Link related issues when applicable.
- Include screenshots for visible UI/theme/layout changes.

## Security & Configuration Tips
- Do not commit secrets, tokens, or local machine paths.
- Treat `themes/PaperMod` as an upstream dependency; prefer overrides in root `layouts/` or `assets/`.
