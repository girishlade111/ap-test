# ap-test

An interactive canvas **particle-text animation** demo — particles assemble into a logo/text shape on screen and scatter away from the cursor (or touch), then drift back together. A playful visual experiment generated with [v0](https://v0.app) and rebuilt as a lightweight Next.js page.

> This project started as a v0.app playground experiment ("ap-test") and is kept here as a standalone demo of canvas-based particle animation with React.

## Demo

- Thousands of canvas particles form a filled text/logo shape.
- Move your mouse (or drag on touch devices) — particles near the cursor scatter in white and then fall back into the letterforms.
- Responsive: the canvas resizes with the window; layout adapts under 768px.

## Tech stack

- **Next.js 15.2.4** (App Router, client component)
- **React 19**
- **Tailwind CSS 3.4** + tailwindcss-animate
- **shadcn/ui** component set (Radix primitives, cva, clsx, tailwind-merge)
- Plain **Canvas 2D API** for the particle engine — no WebGL dependencies
- TypeScript throughout

## Quick start

Requires Node.js 18+ and pnpm (npm works too).

```bash
pnpm install        # or: npm install
pnpm dev            # or: npm run dev
```

Open [http://localhost:3000](http://localhost:3000). The animation runs immediately — move your cursor over the text.

## Build & static export

The page is fully client-side (no API routes, no server actions), so it can be exported as static HTML:

```bash
pnpm build          # builds with output: 'export' into ./out
```

Then serve `./out` with any static host (Cloudflare Pages, Netlify, GitHub Pages, nginx, `npx serve out`).

## Project structure

```
ap-test/
├── app/
│   ├── layout.tsx        # Root layout (Geist fonts, Vercel Analytics, metadata)
│   ├── page.tsx          # Thin wrapper rendering the particle component
│   └── globals.css       # Global styles
├── components/
│   └── theme-provider.tsx
├── components.json       # shadcn/ui config
├── lib/
│   └── utils.ts          # cn() helper (clsx + tailwind-merge)
├── public/               # Placeholder images (not used by the demo page)
├── styles/
│   └── globals.css       # Duplicate global styles (legacy from v0 scaffold)
├── vercel-logo-particles.tsx  # The particle engine + canvas rendering
├── next.config.mjs       # images.unoptimized, output: 'export'
├── tailwind.config.ts
└── postcss.config.mjs
```

## How the animation works

`vercel-logo-particles.tsx` renders text to an offscreen measurement of the canvas, samples pixel data to build a particle for each "filled" pixel, and runs a `requestAnimationFrame` loop where each particle has a spring back to its base position plus a radial repulsion force from the pointer. Colors shift to white while scattered and fade back as they settle.

## Environment variables

None required. No backend, no API keys.

## Deployment

- Any static host works (see "Build & static export" above). The repo ships with `output: 'export'` in `next.config.mjs`, so `pnpm build` writes directly to `./out`.
- Previously also auto-synced with v0.app deployments.

## Notes

- `styles/globals.css` is a leftover duplicate of `app/globals.css` from the v0 scaffold; the App Router uses `app/globals.css`.
- Placeholder images under `public/` are not referenced by the demo page.

---

Built by Girish Lade — [ladestack.in](https://ladestack.in)
