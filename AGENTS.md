# AGENTS.md

Static, client-only educational website that visualizes git branching concepts
(commit, branch, switch, merge, rebase, fetch/pull/push, reset, revert, tag)
with D3 commit graphs and an interactive fake terminal per playground. Fork of
[onlywei/explain-git-with-d3](https://github.com/onlywei/explain-git-with-d3);
2015-era upstream code, no CI.

## No build system

There is no `package.json`, bundler, tests, or linter. All files are plain
HTML/CSS/JS served as-is. Edit a file, refresh the browser.

## Architecture

- **ES5-era vanilla JS with RequireJS AMD modules** (`define(...)`) — not ES
  modules. Keep that style; don't modernize without asking.
- **D3 v3.5.12 and all third-party CSS come from the cdnjs CDN** (require.js via
  `<script>` in `index.html`, d3 via `require.config` in `js/main.js`), so a
  network connection is needed at runtime.
- Every playground's scenario data (`commitData`, `originData`,
  `initialMessage`) is defined **inline in `index.html`** in a `require([...])`
  block, keyed by hash (`#commit`, `#merge`, `#zen`, ...).

## File map

| Path | Role |
|---|---|
| `index.html` | Main page: all playground containers, inline scenario data, hash router, SVG arrow markers. |
| `js/main.js` | RequireJS config (CDN path + shim for d3) and ES5 polyfills. Entry point (`data-main`). |
| `js/explaingit.js` | Public API: `explainGit.open/reset`; creates a `HistoryView` (+ optional origin view) and a `ControlBox` per playground. |
| `js/historyview.js` | D3 rendering of the commit graph (circles, edges, tags, transitions). |
| `js/controlbox.js` | Fake git terminal: parses simulated commands, command history, drives the view. |
| `css/explaingit.css` | Only local stylesheet. |
| `memtest.html` | Dev-only page that repeatedly opens/destroys playgrounds to test for memory leaks. |
| `images/prompt.gif` | Terminal prompt icon. |

## Run locally

`file://` will NOT work (RequireJS loads modules via XHR). Serve the repo root:

```sh
python3 -m http.server 8000
# → http://localhost:8000/
# (or, with Node: npx serve .)
```

`memtest.html` is at http://localhost:8000/memtest.html.
