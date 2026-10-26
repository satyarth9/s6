# Transformation journal

Local-first, static Astro website. No Cloudflare connection, analytics, deployment hooks, or publishing credentials are configured.

## Development

- `npm install` installs dependencies.
- `npm run dev` starts the local development server (normally http://127.0.0.1:4321).
- `npm run build` validates compilation and writes the production website to `dist/` locally.
- `npm run preview` serves that local production build.

These commands do not publish anything. Fonts currently load from Google Fonts; social embeds contact their respective platforms when present.

## Records

`src/data/journey.json` holds public journey settings. `src/data/days/YYYY-MM-DD.json` holds each day's public record. An empty array means not logged, not zero intake or activity. Weight is nullable. Only mark a day complete after closeout. Summaries derive from records during the build. Do not publish drafts, credentials, or private motivations. All data imported into the public site must be treated as public even if the eventual source repository is private.

Use the ignored `private/` directory for local drafts only; do not import it into application code. Local files are durable records; chat history alone should not be the record of truth.

## Social content

Set profile links and add selected posts in `src/data/social.json`. A post has `platform` (`youtube` or `instagram`), `url`, and `title`. YouTube supports watch, Shorts, and youtu.be URLs. Instagram supports public post/reel URLs with embedding enabled. Embeds include source links for fallback. No API token is needed for selected embeds. Automated account synchronization is not implemented. No sample social posts or invented activity are included.

## Release policy

Work locally, run checks and build, then explicitly release. There is currently no Git remote or hosting connection. When hosting is configured, use a dedicated production branch (for example `production`) and disable automatic branch/PR preview deployments if Cloudflare should receive releases only. Daily closeout should produce one publication containing the finalized day and cumulative metrics. Feature development on local branches does not publish.

## Current scope

Responsive overview, weight-loss progress, daily journal, and social embed support. A time-series chart, nutrition estimates, record validation, analytics, and release integration remain future work. Starting data contains only the supplied measurement.

## No-install design preview

Open `preview.html` directly in your browser. It is a standalone, generated design preview with inline CSS and no remote fonts or scripts. Regenerate after data changes using `npm run preview:offline` (Node only; no installation required). `npm run dev:offline` serves the same preview on http://127.0.0.1:4321 when local port access is permitted.

The fallback preview uses a separate Node renderer and the same data/CSS; it is not verification of the Astro production build. It shows profile cards, not embedded posts. Production Astro embeds still need specific post/video URLs. Both profiles are now configured as @saptyogi. The environment used to create this preview blocked npm DNS resolution and binding local server ports, so the Astro build and browser appearance remain unverified.
