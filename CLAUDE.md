# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not** a software project. It is a formal candidacy to the **Premio Pueblo de Cantabria 2026**, an institutional award granted by the Gobierno de Cantabria (Orden OBR/2/2017). The applicant is the **Junta Vecinal de Güemes** (parish council of a 301-inhabitant village in Bareyo, Cantabria, Spain).

All deliverables are static HTML documents. The repository holds the dossier submitted to the jury plus its source materials and the deployed public website.

**GitHub repo**: `clotitec/guemes2026` (public) — https://github.com/clotitec/guemes2026
**Vercel target**: auto-deploy from `main` branch, serving the `public/` folder
**Public URL**: https://guemes-pueblo-cantabria-2026.vercel.app/
**QR code**: generated at `public/qr/` in 3 variants (corten PNG, B&W PNG, scalable SVG)

⚠️ Known config issue as of first deploy: Vercel Root Directory was initially set wrong (serving `app/` instead of `public/`). Fix in Vercel dashboard → Settings → General → Root Directory = `public` → Redeploy. The new landing only shows after this fix.

## Critical dates and budget

- **Submission deadline: 4 May 2026** (telematic presentation) — hard deadline, do not miss
- Junta Vecinal approval meeting: 13 April 2026 (passed — approved)
- Public info meeting in the village: 19 April 2026 (passed — residents committed to voluntary weekend cleanups)

Total prize budget: **160.000 €**, distributed in 4 blocks. Every draft of the *memoria económica* must preserve the total and these 4 blocks:

| Block | Amount | Concept |
|---|---|---|
| A | 60.000 € | Senda de las Estatuas (4 acero corten sculptures + urbanization of plazoletas, mobiliario, señalización, obra civil, proyecto técnico) |
| B | 45.000 € | Preservation works + the 14 km of Camino de Santiago across the municipality of Bareyo |
| C | 15.000 € | "Enróllate en Güemes" — rural arts festival (renamed from "Güemes en Bolas" on 21 Apr 2026 — never use the old name) |
| D | 40.000 € | Pádel court replacement, athletics fencing, Ermita San Julián as Digital Interpretation Centre |

## Repository layout

### The three working layers

```
public/            ← DEPLOY HERE — single source of truth for the website
  index.html       The landing (10 scroll-narrative sections + documents hub)
  mapa/            Interactive world map of the 4 Güemes (+ 23 aerial photos)
  docs/            11 official candidacy HTMLs
  archivos/        PDFs and GPX renamed for clean URLs (convocatoria, informe histórico, etc.)

app/               ← LEGACY deployment (old Vercel target). Same content as public/docs/
01_..06_*/         ← OFFICIAL numbered folders. Original versions of the docs
a mejorar/         ← Source materials + working copies (PDFs, KML, original images, candidatura/ and mapa_hermanos/ drafts)
```

**Editing rule**: make changes in `public/`. When substantial changes are validated, reflect them in the relevant numbered folder (`06_Memoria_Actuacion/`, etc.) as the "official" version. The `app/` folder is legacy — do not edit unless asked.

**Do not modify** `01_Convocatoria/` (official call PDF) or `05_Certificaciones/` (external certificates).

**Path caveat**: the local absolute path contains dots and spaces (`D:/..... continua claude/Guemes_2026/`). Always quote paths in Bash commands. A rename attempt of `a mejorar/` failed due to a Windows file lock, so the folder keeps the space — but the deployed website in `public/` uses clean paths.

### Key files at the repo root

- `vercel.json` — Vercel config: `cleanUrls`, cache headers for `/mapa/imagenes/*` (immutable 7 days) and `/archivos/*` (1 day)
- `.gitignore` — excludes the 21 stray `aerea_*.jpg` duplicates at root, `.claude/settings.local.json`, OS junk
- `README.md` — public-facing project README (structure + how to deploy)
- `CLAUDE.md` — this file
- `ESTADO_PROYECTO.md` — live status tracker (dates, decisions, pending items)

## Commands

### Local preview of the deployable site

```bash
# Option 1 — double-click public/index.html (simplest, works for most things)

# Option 2 — local HTTP server (required for the iframe and PDF links to work)
cd public && python3 -m http.server 8000
# → http://localhost:8000
```

### Git + GitHub

```bash
# Status and commit
git status
git add .
git commit -m "…"
git push

# Fix "dubious ownership" warning on this drive (already done globally)
git config --global --add safe.directory 'D:/..... continua claude/Guemes_2026'

# User is authenticated as `clotitec` via gh CLI with `repo` scope
gh repo view clotitec/guemes2026
gh auth status
```

### Vercel deployment

Auto-deploy on push to `main`. Initial project setup on Vercel dashboard:

- **Root Directory**: `public`
- **Framework Preset**: Other (static)
- **Build / Install / Output commands**: all empty

Manual deploy (if Vercel MCP token is valid): use `mcp__claude_ai_Vercel__deploy_to_vercel`. If expired, ask the user to reconnect the Vercel MCP or trigger deploy from the Vercel dashboard.

### Bulk text edits across the candidacy HTMLs

```bash
# Safe bulk rename pattern — used for "Güemes en Bolas" → "Enróllate en Güemes"
for f in public/docs/*.html app/*.html 02_Solicitud/*.html 06_Memoria_Actuacion/*.html; do
  sed -i 's/old text/new text/g' "$f"
done
```

## Tech stack (and absence of one)

- Pure HTML + inline CSS + vanilla JavaScript. No build, no `package.json`, no framework.
- Google Fonts CDN — `public/index.html` uses Fraunces + Inter; `public/docs/*` use Inter only.
- Maps via Leaflet 1.9.4 (CDN) with CartoDB Dark Matter tiles. The world map at `public/mapa/mapa_mundial_hermanos.html` is embedded as an iframe from the landing.
- Street View embedded via Google Maps embed iframe (public, no API key needed).
- No tests, no lint, no CI beyond Vercel's auto-deploy.

## Narrative pillars — must be respected

Every document rests on three pillars. Each claim must be traceable to a source document. **Do not invent, do not embellish.**

1. **900 years documented** (1084–2026) — sourced from `a mejorar/INFORME HISTORICO.pdf` by Luis de Escallada González (Centro de Estudios Montañeses, 15 June 2010). Also published in `public/archivos/informe-historico.pdf`.
2. **"Abriendo caminos de amistad"** — the contemporary project. In **2009**, pilgrim **Bob** from Guemes Island (Washington, USA) arrived at the albergue; cura **Ernesto Bustio** organized a trip (Argentina → México → USA) with support from the Consejería de Cultura. Four maquetas de acero corten are already installed in **El Portalillo de Güemes** under this project title. Source: `a mejorar/HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES.pdf` (also at `public/archivos/historia-viaje-cuatro-guemes.pdf`).
3. **Hospitalidad peregrina continuous since s. XIV** — the medieval *Hospital de San Julián y Nª Sª de la Consolación* (closed 1800 by Real Cédula) is the antecedent of today's *Albergue La Cabaña del Abuelo Peuto* (founded 1999 by Ernesto Bustio, +50.000 peregrinos, +100 countries, best-rated on the Camino del Norte).

## Factual nuances easy to get wrong

The "4 Güemes del mundo" narrative has historical subtleties. Several earlier drafts contained errors — current drafts are corrected. Keep these straight:

- **Juan Francisco de Güemes y Horcasitas** (1st Conde de Revillagigedo, virrey of Nueva España) was born in **Reinosa**, not in Güemes-Bareyo.
- **Martín Miguel de Güemes** (Argentine hero, 1785–1821) — his father Gabriel came from **Abionzo** (Cantabria), not Güemes-Bareyo.
- The bond between the 4 Güemes (España, México, Argentina, EE.UU.) is **toponymic** (shared surname origin tracing to the village) + **contemporary** (the 2009 trip). It is NOT direct birthplace lineage to Güemes-Bareyo for any of the historical figures. The defensible story is *"cuna del apellido"* + *"abriendo caminos de amistad"*, not *"here was born the virrey"*.
- Sources cross-verified: Wikipedia ES/EN, Historia Hispánica (Real Academia de la Historia), Biografías y Vidas, PARES (Portal de Archivos Estatales).

## Key stakeholders

| Role | Name | Contact |
|---|---|---|
| Presidenta Junta Vecinal de Güemes | Begoña de la Fuente Crespo | via Ayuntamiento Bareyo |
| Presidente Cooperativa Nª Sª de Consolación | Miguel Lavín | — |
| Cura / Fundador del albergue | Padre Ernesto Bustio Crespo | ernestobustio@yahoo.es |
| Ayuntamiento de Bareyo | — | aytobareyo.org |
| Candidacy lead (pro bono) | Clotitec | info@clotitec.com |

## Conflict-of-interest posture

The candidacy is being drafted **pro bono** by Clotitec (info@clotitec.com). The candidacy text itself must NOT name Clotitec as a designated service provider for any of the 160 k€ budget lines. Describe services generically ("a specialist digital provider, awarded by the Junta Vecinal through its standard procurement"). If the candidacy wins, Clotitec may compete openly on equal terms — no prior commitment.

## The 4 sculpture locations (coordinates provisional)

| Sculpture | Location in the village | Approx. GPS |
|---|---|---|
| Güemes de España | Centro, junto a Iglesia de San Vicente | 43.4557, -3.6369 |
| Güemes de Argentina | Plazoleta grande, entrada por Galizano | 43.4540, -3.6400 |
| Güemes de México | Parque dirección Meruelo | 43.4565, -3.6340 |
| Güemes de EE.UU. | El Quejigal, cerca de la Ermita San Julián | 43.4553, -3.6378 |

Exact coordinates live in `a mejorar/Estatuas.kml` (a Google My Maps NetworkLink). Coordinates in `public/mapa/mapa_mundial_hermanos.html` (see `LOCAL_POI` object in the JS) should be refined once the KML is resolved.

## Two palettes coexist by design

- `public/docs/*` and `app/*` — **green + gold** (original institutional palette, validated)
- `public/index.html` and `public/mapa/*` — **corten steel + dark navy + cream** (new premium editorial palette, inspired by the sculpture material)

Do not unify them without explicit user instruction. They serve different purposes: the docs are functional, the landing and map are the "emotional hook" that sells the candidacy.

## Persistent personal memory

A Claude Code auto-memory system is active at `~/.claude/projects/D--------continua-claude-Guemes-2026/memory/` with notes on the user, feedback, project evolution, stakeholder preferences, and source-document summaries. Read `MEMORY.md` there at session start — it complements this `CLAUDE.md` (this one = project facts; memory = how to collaborate).

## Source documents worth reading

When generating any new narrative content, read these first (available both at source locations and at `public/archivos/` with cleaner filenames):

- `a mejorar/INFORME HISTORICO.pdf` — 15 pages, academic, the historical backbone
- `a mejorar/HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES.pdf` — 11 pages with photos, the contemporary story
- `a mejorar/ERNESTO BUSTIO CRESPO, HISTORIA DEL ALBERGUE Y DEL PERSONAJE.pdf` — context on the central figure
- `ESTADO_PROYECTO.md` — live status tracker
- `CONVOCATORIA 2026 ORDEN OBR-002-20217.pdf` — the official call (governs what the jury expects)

## Current state (as of 21 Apr 2026)

- Bulk rename "Güemes en Bolas" → "Enróllate en Güemes" completed across 14 files (0 remaining occurrences in HTML content; file slug `guemes-en-bolas.html` kept for URL stability).
- Landing page built at `public/index.html` with 10 narrative sections including a "Documentos oficiales" hub that links to the 11 docs and to the interactive map.
- World map at `public/mapa/mapa_mundial_hermanos.html` with 4 animated arcs, local village mode, Street View embed, bilingual ES/EN toggle, and a visor aéreo of 23 locally-hosted photos.
- Git repo initialized, first commit pushed to GitHub `clotitec/guemes2026`. Vercel deployment pending a dashboard import or MCP reconnect.
- Pending: exact KML coordinates for the 4 sculptures, real QR code linking to the public URL once Vercel assigns it.
