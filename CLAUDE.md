# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not** a software project. It is a formal candidacy to the **Premio Pueblo de Cantabria 2026**, an institutional award granted by the Gobierno de Cantabria (Orden OBR/2/2017). The applicant is the **Junta Vecinal de Güemes** (parish council of a 315-inhabitant village in Bareyo, Cantabria, Spain).

All deliverables are static HTML documents. The repository holds the dossier submitted to the jury plus its source materials and the deployed public website.

- **Local path**: `F:\guemes2026\` (Windows; quote paths in Bash)
- **GitHub repo**: `clotitec/guemes2026` (public) — https://github.com/clotitec/guemes2026
- **Vercel target**: auto-deploy from `main` branch on push
- **Public URL**: https://guemes-pueblo-cantabria-2026.vercel.app/

### Deployment routing — important

Vercel auto-serves the `public/` folder when Framework Preset = "Other" and a `public/` directory exists. The Root Directory setting in Vercel shows `.` but Vercel behaves as if the root is `public/`.

Consequence: **`app/*` is NOT served via the public URL** — only `public/*` is. The `app/` directory is kept as a legacy reference to the earlier deployment that used a green+gold institutional palette; nothing in it is live.

**Editing rule**: to change what's published, edit `public/*`. Do not waste effort editing `app/*` — those changes never reach production.

Standard URL mapping (`vercel.json` has `cleanUrls: true`):
- `/` → `public/index.html`
- `/mapa/mapa_mundial_hermanos.html` → `public/mapa/mapa_mundial_hermanos.html`
- `/mapa/senda` → `public/mapa/senda/index.html`
- `/docs/memoria-economica` → `public/docs/memoria-economica.html`
- `/paneles` → `public/paneles/index.html`
- `/archivos/*.pdf` → `public/archivos/*.pdf`
- `/imagenes/...` → `public/imagenes/...`

### Deploy commands

```bash
# Default deploy: push to main → Vercel auto-deploys (~30-60 s)
git push

# Regenerate a PDF from a live URL (used to refresh archivos/*.pdf):
"/c/Program Files/Google/Chrome/Application/chrome.exe" \
  --headless=new --disable-gpu --no-sandbox --no-pdf-header-footer \
  --virtual-time-budget=20000 --run-all-compositor-stages-before-draw \
  --window-size=1100,1500 \
  --print-to-pdf="F:/guemes2026/public/archivos/FILENAME.pdf" \
  "https://guemes-pueblo-cantabria-2026.vercel.app/PATH"

# Local preview (required for iframe + relative PDF links to work):
cd public && python -m http.server 8000   # → http://localhost:8000
```

## Critical dates and budget

- **Submission deadline: 4 May 2026** (telematic presentation) — hard deadline.
- Junta Vecinal approval meeting: **13 April 2026** (passed — approved).
- Public info meeting: **19 April 2026** (passed).

Total prize budget: **160.000 €**, in 4 blocks. Every draft of the *memoria económica* must preserve the total and these 4 blocks:

| Block | Amount | Concept |
|---|---|---|
| A | 60.000 € | Senda de las Estatuas (4 acero corten sculptures + plazoletas urbanization, mobiliario, señalización, obra civil, proyecto técnico, plantación de árbol emblemático por plazoleta) |
| B | 45.000 € | Preservation works + 14 km of Camino de Santiago in Bareyo |
| C | 15.000 € | "Enróllate en Güemes" — rural arts festival (renamed from "Güemes en Bolas" on 21 Apr 2026 — never use the old name) |
| D | 40.000 € | Pádel court replacement, athletics fencing, **Centro de Interpretación Digital del Peregrino** in the Ermita de San Julián |

## Repository layout

```
public/                           ← DEPLOY HERE — single source of truth
  index.html                      Landing (12 narrative sections incl. ermita 24/7)
  mapa/
    mapa_mundial_hermanos.html    World map of the 4 Güemes
    senda/index.html              Senda map (MapLibre + Photo Sphere Viewer 360)
    streetview/{guemes,wemes}.json Google Street View pano IDs (~700 points)
  docs/                           Candidacy HTMLs (memorias, dossier, paneles, etc.)
  paneles/index.html              4 trilingual ES/EN/FR interpretive panels (A3)
  archivos/                       Generated PDFs and GPX (clean URLs)
  imagenes/                       Optimized photos (~1920px JPEG q82-86 + thumbs/)
    renders/                      8 day/night plazoleta renders
    iglesia/, ermita/             13 photos of the two temples (incl. AI totem render)
    antes/                        4 country reference images for antes/después comparison
  qr/                             3 QR variants (PNG color, PNG B&W, SVG)

ENTREGA_CANDIDATURA/              ← gitignored · regenerated on demand
                                  Final delivery folder for Google Drive (102 MB).
                                  Contains all official PDFs ordered by their
                                  upload destination on the Consejería platform.

app/                              LEGACY (older Vercel target) — do not edit
01_..06_*/                        OFFICIAL numbered folders (master copies)
"a mejorar/"                      Source PDFs/KML/originals (folder name has a space)
"fotos renders.../"               Source PNGs of renders (gitignored)
"fotos iglesia y ermita.../"      Source JPGs (gitignored)
*.jpg, *.png at root              Source images (gitignored — optimized copies live in public/imagenes/)
```

**Editing rule**: make changes in `public/`. The numbered folders (`06_Memoria_Actuacion/`, etc.) are the "official" archived versions kept untouched unless major content is finalized. **Do not modify** `01_Convocatoria/` (official call PDF) or `05_Certificaciones/`.

**Path caveat**: paths can contain spaces (`"a mejorar/"`, `"fotos renders.../"`). Always quote them in Bash.

## Tech stack (and absence of one)

- Pure HTML + inline CSS + vanilla JavaScript. No build, no `package.json`, no framework.
- Google Fonts CDN (Instrument Serif, Satoshi, Inter, Fraunces).
- World map: **Leaflet 1.9.4** (CartoDB Voyager tiles).
- Senda map: **MapLibre GL** (Esri satellite + OSM) + **Photo Sphere Viewer 5.13.3** for the 30 aerial 360° panoramas.
- Street View: Google Maps embed iframe (public format `embed?pb=!4v1!6m8!1m7!1s${pano}!2e10` — **no API key needed**).
- Image optimization: Python with **PIL/Pillow** (resize to max 1920px, JPEG q82-86, generate 720px thumbs).
- No tests, no lint, no CI beyond Vercel's auto-deploy.

## Two visual palettes coexist by design

- `public/docs/*` (early-generation docs) and `app/*` — **green + gold**.
- `public/index.html`, `public/mapa/*`, `public/paneles/*`, and the newer docs (`memoria-economica`, `documentacion-grafica`, `guia-visita-jurado`) — **corten steel + dark navy + cream**, with Instrument Serif italic for headers and Satoshi for body. CSS variables: `--bg-deep #0a1120`, `--bg-navy #101a30`, `--corten #c89450`, `--corten-br #f4c77b`, `--ok #7bc6f4`.

Do not unify the palettes without explicit instruction. The docs are functional; the landing/map/paneles are the "emotional hook".

## Narrative pillars — must be respected

Every document rests on three pillars. Each claim must be traceable to a source. **Do not invent, do not embellish.**

1. **942 years documented (1084–2026)** — sourced from `a mejorar/INFORME HISTORICO.pdf` by Luis de Escallada González (Centro de Estudios Montañeses, 15 June 2010). Republished at `public/archivos/informe-historico.pdf`.
2. **"Abriendo caminos de amistad"** — the contemporary project. In **2009**, pilgrim **Bob** from Guemes Island (Washington, USA) arrived at the albergue; cura **Ernesto Bustio** organized a trip (Argentina → México → USA) with support from the Consejería de Cultura. Four maquetas de acero corten are already installed in **El Portalillo**. Source: `a mejorar/HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES.pdf`.
3. **Hospitalidad peregrina continua desde s. XIV** — the medieval *Hospital de San Julián* (closed 1800 by Real Cédula) is the antecedent of today's *Albergue La Cabaña del Abuelo Peuto* (founded 1999 by Ernesto Bustio, +150.000 peregrinos, +80 países).

### Ermita de San Julián — narrative (corrected 29 abril)

The ermita has been **continuously open 24/7, gratuitous, without staff** for decades — fiel a su vocación histórica. The candidacy **does not "open" the ermita**; it adds two layers:

1. **Vigilance** — RGPD-compliant camera + aforo counter to protect accumulated patrimony (cientos de fotos del Padre Ernesto, exvotos).
2. **Data + ampliated information** — multilingual touch totem (ES · EN · FR · DE · IT) with full digital photo gallery (more than fits physically), online dashboard for the Junta Vecinal.

Never write copy that suggests the ermita "se va a abrir". The wording is *"proteger, medir y dar a conocer un patrimonio que ya funciona"*.

## Factual nuances easy to get wrong

The "4 Güemes del mundo" narrative has historical subtleties. Several earlier drafts contained errors — current drafts are corrected:

- **Juan Francisco de Güemes y Horcasitas** (1st Conde de Revillagigedo, virrey of Nueva España) was born in **Reinosa**, not in Güemes-Bareyo.
- **Martín Miguel de Güemes** (Argentine hero, 1785–1821) — his father Gabriel came from **Abionzo** (Cantabria), not Güemes-Bareyo.
- The bond between the 4 Güemes is **toponymic** (shared surname) + **contemporary** (the 2009 trip). Defensible story: *"cuna del apellido"* + *"abriendo caminos de amistad"*. NOT *"here was born the virrey"*.

### Emblematic trees per plazoleta (climate-validated for Bareyo, Cfb / USDA 9a-9b)

| Country | Tree | Scientific | Notes |
|---|---|---|---|
| 🇪🇸 España | Roble común | *Quercus robur* | Autóctono cantábrico — ideal |
| 🇦🇷 Argentina | **Ceibo** (NOT jacarandá — too cold-sensitive) | *Erythrina crista-galli* | Árbol nacional oficial argentino (1942), resists -7 °C |
| 🇲🇽 México | **Ciprés calvo** (NOT ahuehuete — slow growth in cool summers) | *Taxodium distichum* | Same genus as ahuehuete, fully hardy in northern Spain |
| 🇺🇸 EE.UU. | Abeto Douglas | *Pseudotsuga menziesii* | Washington state tree, planted commercially in Cantabria |

## Senda map (`public/mapa/senda/`) — current UI state

The map has been progressively cleaned. **Do not re-add** these without explicit instruction:

- ❌ "Mostrar puntos 360°" toggle button (removed)
- ❌ "Street View Google" toggle button + 700-pano JSON layer + modal (removed)
- ❌ Route toggle "Ambas / Completa / Jurado" (only one route exists)
- ❌ "Ruta del jurado · Wikiloc" sidebar entry (removed)
- ❌ "Patrimonio 3D / Tour Matterport Iglesia + Ermita" link (removed)
- ❌ Visible "Matterport" branding anywhere

What's allowed:
- ✅ Two buttons "Ver interior de la iglesia" / "Ver interior de la ermita" using the existing Matterport iframe modal — but **no visible "Matterport" text** in labels, eyebrows or descriptions.
- ✅ "Visor aéreo 360° · 30 vistas" button → opens Photo Sphere Viewer.
- ✅ Single circular route GPX.

## Paneles (`public/paneles/`) — current state

- 4 A3-portrait panels, trilingual (ES · EN · FR demonstrative; full ES · EN · FR · DE · IT online).
- Each has a schematic SVG world map (viewBox 360x180) with origin marker (Güemes) and destination dot + dashed arc. The realistic Wikipedia world map was tried and reverted — keep schematic.
- **No QR codes** — replaced with `panel-url-block` showing the public URL.

## Guía visita jurado (`public/docs/guia-visita-jurado.html`)

Final cleaned version has 4 sections only:
1. Visión general — Landing
2. Cartografía interactiva — Mapa mundial · Mapa Senda · Tour 360°
3. Memorias y documentos — Económica · Actuación · Histórico · Itinerario
4. Material visual y renders — Documentación gráfica completa

**Removed (do not re-add)**: paneles section, documentos complementarios (acta, cartas apoyo, resumen ejecutivo — go via separate channel), transparencia/GitHub.

## Delivery process — `ENTREGA_CANDIDATURA/`

The folder is **gitignored** and rebuilt on demand for Google Drive upload to the administrative team (ATYS) and the Junta Vecinal President (Begoña de la Fuente). Layout:

```
ENTREGA_CANDIDATURA/
├── 00_LEEME_PRIMERO/
│   ├── 00_INSTRUCCIONES_ADMINISTRACION.pdf  (step-by-step for ATYS)
│   ├── 01_GUIA_VISITA_JURADO.pdf            (deliverable for the jury)
│   ├── EMAIL_PARA_BEGONA.txt                (draft to send)
│   ├── VERIFICACION_LINKS.txt
│   ├── CHECKLIST.txt
│   └── README.txt
├── 01_OBLIGATORIOS_FIRMA/                   3 docs (solicitud, memoria económica, declaración responsable)
├── 02_OBLIGATORIOS_SIN_FIRMA/               documentación gráfica (31 MB)
├── 03_OPCIONALES_FIRMA/                     ATYS deposita certificación firmada del acta
├── 04_DOCUMENTOS_BASE_PRETENSION/           memoria actuación, dossier, biografías, paneles, candidatura completa
├── 05_MATERIAL_GRAFICO/                     renders, iglesia/, ermita/, fotos_pueblo/, aereas/
├── 06_RECURSOS_DIGITALES/                   ENLACES_WEB.txt + QRs
└── 99_REFERENCIA/                           convocatoria oficial BOC + GPX
```

When the user asks to "regenerate the delivery", the steps are: regenerate latest PDFs from live URLs → copy to the right subfolders → refresh README files → verify URLs return 200.

## Image optimization workflow

When raw images land at the project root or in source folders, optimize them before committing:

```python
from PIL import Image, ImageOps
img = ImageOps.exif_transpose(Image.open(src).convert("RGB"))
big = img.resize((1920, int(img.size[1] * 1920 / img.size[0])), Image.LANCZOS)
big.save(out_full, "JPEG", quality=84, optimize=True, progressive=True)
thumb = big.resize((720, ...), Image.LANCZOS)
thumb.save(out_thumb, "JPEG", quality=78, optimize=True, progressive=True)
```

Originals at root must be excluded via `.gitignore` (`/*.jpg`, `/*.png`). The single source of truth for the website is `public/imagenes/` (optimized).

## Conflict-of-interest posture

The candidacy is being drafted **pro bono** by Clotitec (info@clotitec.com). The candidacy text itself must NOT name Clotitec as a designated provider for any of the 160 k€ budget lines. Describe services generically (*"un proveedor digital especialista, adjudicado por la Junta Vecinal a través de su procedimiento ordinario de contratación"*). If the candidacy wins, Clotitec may compete openly on equal terms.

## Key stakeholders

| Role | Name | Contact |
|---|---|---|
| Presidenta Junta Vecinal de Güemes | Begoña de la Fuente Crespo | via Ayuntamiento Bareyo |
| Presidente Cooperativa Nª Sª de Consolación | Miguel Lavín | — |
| Cura / Fundador del albergue | Padre Ernesto Bustio Crespo | ernestobustio@yahoo.es |
| Ayuntamiento de Bareyo | — | aytobareyo.org |
| Asesoría administrativa | ATYS | (handles certificate + declaración responsable) |
| Candidacy lead (pro bono) | Clotitec | info@clotitec.com |

## Persistent memory

A Claude Code auto-memory system exists at `C:\Users\Usuario\.claude\projects\F--guemes2026\memory\` with notes on user preferences, feedback, project evolution, source-document summaries. Read `MEMORY.md` there at session start — it complements this file (CLAUDE.md = project facts; memory = how to collaborate).

## Source documents worth reading before generating new content

Available both at source locations and at `public/archivos/` with clean filenames:

- `a mejorar/INFORME HISTORICO.pdf` — 15 pages, academic, the historical backbone
- `a mejorar/HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES.pdf` — 11 pages with photos
- `a mejorar/ERNESTO BUSTIO CRESPO, HISTORIA DEL ALBERGUE Y DEL PERSONAJE.pdf`
- `ESTADO_PROYECTO.md` — live status tracker
- `CONVOCATORIA 2026 ORDEN OBR-002-20217.pdf` — official call (governs jury expectations)
