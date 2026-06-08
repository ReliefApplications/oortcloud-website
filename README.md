# Oort Technology — Website

Marketing website for **Oort Cloud Technology S.L.**, served at
[www.oortcloud.tech](https://www.oortcloud.tech).

The site is a small set of static, dependency-free HTML pages. There is no build
step, framework, or bundler — every page is hand-written HTML with inline CSS and
loads instantly.

## Pages

| File                  | URL                  | Purpose                                          |
| --------------------- | -------------------- | ------------------------------------------------ |
| `index.html`          | `/`                  | Landing page (services, approach, clients, contact) |
| `privacy-policy.html` | `/privacy-policy.html` | Privacy & cookie policy                        |
| `404.html`            | served on any unknown path | Custom "page not found" page               |

Supporting files:

- `CNAME` — the custom domain (`www.oortcloud.tech`) GitHub Pages serves the site on.

## Local development

There's no toolchain to install. Either open a file directly:

```bash
open index.html
```

…or serve the folder so that root-relative links (`/`, `/privacy-policy.html`)
behave exactly as they do in production:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

To preview the 404 page locally, navigate to any non-existent path while using a
server that falls back to `404.html`, or just open `404.html` directly.

## Deployment (GitHub Pages)

The site is deployed with **GitHub Pages**, served straight from this repository —
there is no CI/CD workflow or build artifact.

**How it works:**

1. GitHub Pages is configured to deploy from the `main` branch, root (`/`) folder.
   (Repository → **Settings → Pages → Build and deployment → Deploy from a branch**.)
2. Any push to `main` publishes automatically within a minute or two.
3. The `CNAME` file binds the site to the custom domain `www.oortcloud.tech`.
   DNS for that domain points at GitHub Pages. Keep this file in the repo — Pages
   re-reads it on every deploy, and deleting it unsets the custom domain.
4. `404.html` is GitHub Pages' built-in convention: it is automatically served
   (with an HTTP 404 status) for any request that doesn't match a real file.

**To publish a change:**

```bash
git add .
git commit -m "Describe your change"
git push origin main
```

Then watch the deployment under the repo's **Actions** tab (GitHub runs an internal
"pages build and deployment" job). Once it's green, the live site reflects the change.

## Conventions

- **No dependencies, no build.** Keep each page self-contained. Styles live in a
  `<style>` block in each page's `<head>`; fonts load from Google Fonts.
- **Shared design tokens.** Colours and spacing are defined as CSS custom
  properties under `:root` (e.g. `--accent`, `--ink`, `--paper`). Reuse them so
  pages stay visually consistent.
- **Root-relative links.** Link between pages with paths like `/` and
  `/privacy-policy.html` so they resolve correctly on the custom domain.
