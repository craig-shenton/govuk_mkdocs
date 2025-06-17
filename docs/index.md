# GOVUK mkdocs example site

The site is built using [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme, styled with GOV.UK design language.

📍 **Live site**: [https://craig-shenton.github.io/govuk_mkdocs/](https://craig-shenton.github.io/govuk_mkdocs/)

---

## 🚀 How to Build Locally

To preview and develop the site locally:

### 1. Install Python and dependencies

```bash
pip install mkdocs mkdocs-material "mkdocstrings[python]" mkdocs-autorefs
```

> Use quotes for `mkdocstrings[python]` in zsh to avoid shell errors.

### 2. Start the local development server

```bash
mkdocs serve
```

Then open `http://localhost:8000` in your browser.

---

## 🌍 How to Deploy

### ⚙️ Deployment is automated via GitHub Actions

On every push to `main`, the site is built and deployed to the `gh-pages` branch using this workflow:

```
.github/workflows/deploy.yml
```

### 🛠️ Manual Deploy (fallback)

```bash
mkdocs build
cd site
git init
git checkout -b gh-pages
git remote add origin https://github.com/craig-shenton/govuk_mkdocs.git
touch .nojekyll
git add .
git commit -m "Manual deploy"
git push -f origin gh-pages
```

Then enable Pages in **Settings → Pages → Source: `gh-pages` / root**.

---

## ✍️ How to Edit Content

All documentation lives in the `docs/` folder.

- Markdown content → `docs/*.md`
- Navigation → `mkdocs.yml` under `nav:`
- Custom styles → `docs/assets/stylesheets/extra.css`
- HTML overrides → `overrides/main.html`

To update:

- Make your edits
- Rebuild with `mkdocs build` (if deploying manually)
- Push to `main` (if using GitHub Actions)

---

## 🧠 Features

- ✅ GOV.UK styling and branding
- ✅ Auto API reference with `mkdocstrings`
- ✅ GitHub Pages auto-deploy
- ✅ PDF download option (via template)
- ✅ `.nojekyll` for directory support
- ✅ GitHub Actions integration

---

## 📋 TODO: UExtensions & Plugins

### 🧩 Markdown Extensions to Enable

```yaml
markdown_extensions:
  - github-callouts
  - pymdownx.highlight
  - pymdownx.inlinehilite
  - pymdownx.snippets
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.tabbed:
      alternate_style: true
      slugify: !!python/object/apply:pymdownx.slugs.slugify
        kwds:
          case: lower
```

Steps:

- [ ] Install: `pip install pymdown-extensions`
- [ ] Add the above to your `mkdocs.yml`
- [ ] Create sample Markdown files that use:
  - !!! note / warning callouts (`github-callouts`)
  - `mermaid` diagrams using ```mermaid
  - `=== Tabs ===` blocks

---

### ⚙️ MkDocs Plugins to Add

```yaml
plugins:
  - material/search
  #- search  # fallback
  - awesome-nav
  - redirects:
      redirect_maps:
        'index.md': 'api-design-guidelines/index.md'
  - git-revision-date-localized:
      enabled: !ENV [MKDOCS_GIT_PROVENANCE_ENABLED, false]
      type: timeago
      enable_creation_date: true
  - git-committers:
      enabled: !ENV [MKDOCS_GIT_PROVENANCE_ENABLED, false]
      repository: ukhsa-collaboration/api-guidelines
      token: !ENV [GITHUB_TOKEN]
      branch: main
```

Steps:

- [ ] Install missing plugins:
  ```bash
  pip install mkdocs-awesome-pages-plugin mkdocs-redirects-plugin \
              mkdocs-git-revision-date-localized-plugin mkdocs-git-committers-plugin-2
  ```
- [ ] Add the plugin block above to `mkdocs.yml`
- [ ] Set environment variables in GitHub Actions:
  - `MKDOCS_GIT_PROVENANCE_ENABLED=true`
  - `GITHUB_TOKEN` (add via GitHub repo secrets)
- [ ] Create `api-design-guidelines/index.md` as the new homepage target
- [ ] Structure your file hierarchy to benefit from `awesome-nav`

---

## 📝 License

All content is available under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/), except where otherwise stated.
