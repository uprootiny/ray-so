<p align="center">
  <a href="https://ray.so" target="_blank" rel="noopener noreferrer">
    <img width="1024" src="app/assets/og-image.png" alt="ray.so">
  </a>
</p>

<h1 align="center">ray.so -- standalone local build</h1>

<p align="center">
  A fork of <a href="https://github.com/raycast/ray-so">Raycast's ray.so</a> that builds the app as a <strong>standalone local application</strong>, not just a hosted website.
</p>

<p align="center">
  <a href="https://github.com/uprootiny/ray-so/actions/workflows/build.yml">
    <img src="https://github.com/uprootiny/ray-so/actions/workflows/build.yml/badge.svg" alt="Build & Deploy">
  </a>
</p>

## About

[ray.so](https://ray.so) by [Raycast](https://raycast.com) is a suite of developer tools for creating beautiful code snippet images, browsing AI prompts, creating Raycast extension icons, and more.

This fork packages ray.so as a **standalone local app** you can download and run on your own machine. CI produces a downloadable artifact containing a Node.js server and all static assets -- no internet connection required after download.

The build pipeline also attempts a static export for GitHub Pages deployment.

## Quick start

1. Go to the [Actions tab](https://github.com/uprootiny/ray-so/actions/workflows/build.yml) and open the latest successful run.
2. Download the **ray-so-standalone** artifact (a zip containing a Node.js server + static assets).
3. Unzip and run:

```bash
unzip ray-so-standalone.zip -d ray-so
cd ray-so
./run.sh            # starts on http://localhost:3000
./run.sh 8080       # ...or pick a different port
```

**Requires Node.js 18+.**

## Build from source

```bash
npm ci
npm run build
```

The standalone server output lands in `.next/standalone/`. For development with hot-reload:

```bash
npm ci
npm run dev
```

Then open <http://localhost:3000>.

## CI / artifacts

The GitHub Actions workflow (`.github/workflows/build.yml`) runs on every push to `main`:

1. `npm ci && npm run build` -- produces a **standalone** Next.js server.
2. Packages the server, static assets, `public/` directory, and a `run.sh` helper into the **ray-so-standalone** artifact (retained for 30 days).
3. Attempts a **static export** (`output: "export"`) and deploys to GitHub Pages if it succeeds.

The static export may fail for routes that use dynamic server features in upstream. When that happens the standalone artifact is still produced and usable -- only the Pages deployment is skipped.

## GitHub Pages

If the static export step succeeds, the site is deployed automatically:

> <https://uprootiny.github.io/ray-so/>

## Upstream

Based on [raycast/ray-so](https://github.com/raycast/ray-so). Upstream features include:

- **Code Images** -- create beautiful images of your code
- **Icon Maker** -- create icons for Raycast extensions
- **Prompt Explorer** -- browse AI prompts
- **Preset Explorer** -- browse AI presets
- **Quicklink Explorer** -- browse and import quicklinks
- **Snippet Explorer** -- browse and import snippets
- **Theme Explorer** -- browse and import themes

## License

See upstream [raycast/ray-so](https://github.com/raycast/ray-so) for license terms.
