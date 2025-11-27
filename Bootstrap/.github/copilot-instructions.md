<!--
This file guides AI coding agents working on the small static Bootstrap example site
located at the repo root. Keep this file concise and focused on patterns that are
discoverable from the codebase (no aspirational rules).
-->

# Copilot / Agent Instructions

- **Purpose:** This repository contains standalone static HTML examples that demonstrate
  Bootstrap layouts and components (grid, nav, forms, cards). There is no build system.

- **Key files:**
  - `grid.html` — uses Bootstrap via CDN (`https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/...`) and contains inline example classes `.demo`, `.demo1`.
  - `style.css` — project-level CSS (contains `.btn-geetha`).
  - `style1.css` — additional CSS overriding layout classes (redefines `.col`).
  - Other HTML examples: `button.html`, `cards.html`, `forms.html`, `navigationbar.html`, `navlakshmi.html`, `modelexample.html`, `grid2.html`, `example of grid.html`.

- **Big picture / architecture:**
  - Single-folder static site (no package.json, build tools, or test harness).
  - Each HTML file is an independent example page. Styles are a mix of inline `<style>` blocks and two root CSS files (`style.css`, `style1.css`).
  - External dependency: Bootstrap is loaded from a CDN in pages such as `grid.html`.

- **Developer workflows (what agents need to know):**
  - There is no build step. To preview locally, run a simple HTTP server from the repo root:

    ```powershell
    cd 'c:\geetha\Bootstrap'
    python -m http.server 8000
    ```

    Then open `http://localhost:8000/grid.html` in a browser.

  - Filenames contain spaces (e.g. `example of grid.html`). When constructing URLs or file paths, URL-encode spaces (`example%20of%20grid.html`) or quote paths in PowerShell.

- **Project-specific patterns & conventions (observed):**
  - Multiple pages duplicate patterns (grid, nav, cards). Prefer editing the specific HTML file rather than attempting to generalize across files unless explicitly requested.
  - CSS is split: lightweight common styles in `style.css`, stronger overrides in `style1.css` that change `.col`. Edits to `.col` may impact multiple pages—be conservative.
  - Some pages use inline `<style>` (e.g., `grid.html` defines `.demo`/`.demo1` inline). If moving styles, prefer putting them into `style.css` and updating affected HTML files.
  - Bootstrap version used in `grid.html` is `5.3.8`. When modifying pages that rely on Bootstrap behaviors, keep the CDN version consistent across edits unless the change explicitly requires upgrading.

- **Integration points & external dependencies:**
  - Bootstrap via CDN (no local vendor files).
  - No backend APIs, build servers, or CI detected in repository files.

- **Safe-edit guidance for AI agents (concrete examples):**
  - To change the grid background in `grid.html`, prefer adding a rule to `style.css` and remove the inline `<style>` block only after verifying the page visually.
    Example: add `.demo { background-color: aqua; }` to `style.css` and remove the duplicate inline rule in `grid.html`.
  - Avoid global selectors that shadow Bootstrap core classes (e.g., avoid changing `.col` globally unless the intent is to change layout on all pages). `style1.css` already alters `.col` to blue; mirror that pattern when needed.
  - When updating CDN references, update every HTML file that references the CDN to keep behavior consistent.

- **What not to assume:**
  - There are no tests or CI; do not attempt to run non-existent build/test commands.
  - Do not assume naming conventions are consistent (file `example of grid.html` includes spaces).

If anything here is unclear or you want the agent to follow stricter conventions (for example, normalize filenames or centralize CSS), tell me which direction and I will update this file accordingly.
