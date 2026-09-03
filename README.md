explain-git-with-d3
===================

Use D3 to visualize simple git branching operations.

This simple project is designed to help people understand some basic git concepts visually.

This is my first attempt at using both SVG and D3. I hope it is helpful to you.

The page can be accessed via: https://dvx76.github.io/explain-git-with-d3/

This site is a fork of the original
[explain-git-with-d3](https://github.com/onlywei/explain-git-with-d3) project by
[Wei Wang (onlywei)](https://github.com/onlywei), which is still available at
https://onlywei.github.io/explain-git-with-d3/.

## Running Locally

This is a static site with no build step and no dependencies to install.
However, opening `index.html` directly via the `file://` protocol will **not**
work: the page loads its JavaScript modules with RequireJS, which fetches them
via XHR, and browsers block that on local files.

Serve the repository root with any static file server, e.g.:

```sh
python3 -m http.server 8000
```

then open http://localhost:8000/ in your browser. (With Node.js installed,
`npx serve .` works too.)

Note that the page loads D3, RequireJS, and some CSS from the cdnjs CDN, so an
internet connection is required for full functionality.

The development-only memory leak test page lives at
http://localhost:8000/memtest.html.
