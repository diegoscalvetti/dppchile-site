# DPP Madera website

A static website for the DPP Madera proof of concept. Plain HTML and CSS with relative links,
so it works on any static host and offline (download the folder, open `index.html`).
All data is invented (building ESM-01, seed 4411).

| Path | What it is |
|---|---|
| `index.html` | Landing page: the idea, the four records (DPP, EPM, DBL, DTw), routes per audience |
| `poc.html` | Proof of concept results: architecture, tests T1–T11, assembly state, example questions |
| `mockups/` | Five standalone mockups (A walkthrough, B scan app, C poster, D twin replay, E BPMN) |
| `twin/` | Static snapshot of the PoC's live assembly-state view, with each part's joined record as JSON |
| `figures/` | Figures from `docs/figures/` |

## Updating

This repository is a published copy. The source lives in the (private) PoC repository under `site/`;
`twin/` and `figures/` are regenerated there with `make site`, then copied here.

The mockups are built outside this repository; replace the files in `mockups/` to update them,
then re-add the fixed "DPP Madera home" link (`class="dppm-home"`) right after `<body>`.

## Publish

`.github/workflows/pages.yml` publishes the repository root to GitHub Pages on every push to `main`.
One-time setup: **Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Custom domain: dppchile.com

The site's domain is `dppchile.com` (also recorded in the `CNAME` file; with the GitHub Actions
source the Pages setting below is what counts, the file is a record of it).

1. In this repo: **Settings → Pages → Custom domain**, enter `dppchile.com`, save.
   (With the GitHub Actions source no `CNAME` file is needed; the setting is enough.) (Optional but recommended first: verify the domain under
   your GitHub account **Settings → Pages → Add a domain**, so nobody else can claim it.)
2. At the domain registrar's DNS settings, add:

   | Type | Name | Value |
   |---|---|---|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | AAAA | `@` | `2606:50c0:8000::153` |
   | AAAA | `@` | `2606:50c0:8001::153` |
   | AAAA | `@` | `2606:50c0:8002::153` |
   | AAAA | `@` | `2606:50c0:8003::153` |
   | CNAME | `www` | `diegoscalvetti.github.io` |

   Remove any other A, AAAA or CNAME records on `@` and `www` (registrars often add a parking page).
3. Wait for DNS (minutes to a few hours), then tick **Enforce HTTPS** in Settings → Pages.
4. Check: `dig dppchile.com +short` should list the four `185.199.x.153` addresses.

Other static hosts (Netlify, Vercel, Cloudflare Pages) also work: upload this folder as is.
