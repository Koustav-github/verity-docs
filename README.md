# Verity docs

The documentation site for [Verity](https://github.com/Koustav-github/Verity), an agentic
MLOps pipeline.

Static HTML and one stylesheet. No build step, no dependencies, no framework — which is
the whole point: a docs site whose own toolchain needs maintaining is a liability.

## Layout

```
index.html          Overview — what Verity is, the four agents, the design principle
quickstart.html     Requirements, configuration, first upload, first prediction
architecture.html   Pipeline internals, statuses, sandbox, serving, accepted limits
api.html            SDK reference and HTTP routes
assets/style.css    The shared stylesheet
.nojekyll           Stops GitHub Pages running the files through Jekyll
```

## Running it locally

Any static file server. There is nothing to compile:

```bash
python -m http.server 4000
# then open http://localhost:4000
```

Opening `index.html` directly from the filesystem also works, though the relative links
behave slightly differently in some browsers.

## Deploying to GitHub Pages

Push to a repository, then in **Settings → Pages** choose *Deploy from a branch*, pick the
branch, and set the folder to `/` (root). GitHub serves it as-is.

`.nojekyll` matters: without it, Pages runs the files through Jekyll, which ignores
directories beginning with an underscore and can rewrite things unexpectedly.

## Editing

Each page is self-contained. The masthead and nav are duplicated across all four files —
deliberately, since sharing them would mean introducing a build step or client-side
templating to save a dozen lines. If a fifth page appears and the duplication starts to
hurt, that is the moment to reconsider, not before.

Colours come from the CSS custom properties at the top of `assets/style.css` and match the
Verity app's own palette, so the docs and the product read as one thing.

## Keeping it honest

The content states what Verity does *and* what it does not: no authentication on any
route, single-replica serving, cold-sandbox resource numbers rather than production p99,
non-comparative promotion. If the product changes, those sections need changing with it —
they are the part of a docs site that rots most quietly.
