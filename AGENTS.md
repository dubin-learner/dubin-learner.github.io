# AGENTS.md

## Repo overview
- Static [docsify](https://docsify.js.org/) blog (Chinese content) published via GitHub Pages from `docs/`.
- No `package.json`, build step, lint, or tests. The only source of truth is the Markdown in `docs/`.
- `docs/.nojekyll` is required so GitHub Pages serves files starting with `_` (e.g. `_sidebar.md`). Do not delete it.

## Preview
- Run `docsify serve docs` from the repo root, then open http://localhost:3000.
- `docsify-cli` is installed globally here; on a fresh machine use `npm i -g docsify-cli`. Do not run `docsify init` (site is already initialized).
- Verification = preview the page and confirm new links/images resolve. There is nothing else to run.

## Structure and editing
- `docs/index.html`: docsify config and all CDN plugins (Prism, MathJax, mermaid, dark-mode switch).
- `docs/_sidebar.md`: top-level navigation only (5 sections). Section landing pages list their articles:
  - `docs/README.md` (home), `docs/works.md`, `docs/notes.md`, `docs/lifes.md`.
- To add an article: create `docs/<section>/<topic>/<name>.md`, then add a link on the matching landing page. Only touch `_sidebar.md` for a new top-level section.
- Internal links are root-absolute and omit the `.md` extension, e.g. `/notes/eda/EDA_LEC`. The one exception is `/course/最优化理论.md`.
- Notes are grouped by topic (`notes/cpp/...`, `notes/eda/...`, `course/...`, `tool/...`); EDA notes use `EDA_*.md`, series notes use `00.md`, `01.md`, etc.
- Images live in `docs/resources/<topic>/` (common) or in a sibling folder named after the article. Reference them relatively, e.g. `../resources/vim-use/foo.png` from `docs/tool/`.
- Keep titles/prose in Chinese; this is a personal Chinese-language blog.
- GitHub Pages paths are case-sensitive even though local macOS is not. Keep link and image path casing exact.

## Git gotchas
- Default branch is `master`; committed site files live in `docs/` (no generated output to commit).
- `.gitignore` contains `.DS_store` (wrong case), so `.DS_Store` is not ignored. Do not commit `.DS_Store` files.
- The `origin` URL embeds a GitHub token. Never print `git remote -v` or paste the URL into files, commits, or chat.
