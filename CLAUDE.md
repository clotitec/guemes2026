# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is **not** a software project. It is a formal candidacy to the **Premio Pueblo de Cantabria 2026**, an institutional award granted by the Gobierno de Cantabria (Orden OBR/2/2017). The applicant is the **Junta Vecinal de Güemes** (parish council of a 301-inhabitant village in Bareyo, Cantabria, Spain).

All deliverables are static HTML documents. The repository holds the dossier that will be submitted to the jury plus supporting source materials.

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

## Repository layout (working convention)

```
01_Convocatoria/       READ-ONLY — official call PDF
02_Solicitud/          Application paperwork (checklist, cartas apoyo, acta, resumen)
03_Documentacion_Grafica/   Photos + GPX of circular route
04_Memoria_Economica/  MEMORIA_ECONOMICA.html — the 4-block breakdown
05_Certificaciones/    External certificates (Hacienda, SS, padrón) — pending
06_Memoria_Actuacion/  Core narrative HTMLs (dossier histórico, memoria actuación, itinerario jurado)
app/                   11 validated HTMLs — the version that is on Vercel
a mejorar/             Working layer — in-progress improvements + source documents
  candidatura/         NEW main landing (scroll-narrative index.html)
  mapa_hermanos/       Interactive world map of the 4 Güemes
```

**Iteration rule**: draft and experiment in `a mejorar/`. Promote to `app/` (or the numbered folders) only after stakeholder approval. Never modify `01_Convocatoria/` or `05_Certificaciones/` — those contain external official documents.

**Path caveat**: the absolute path contains dots and spaces (`D:/..... continua claude/Guemes_2026/`). Always quote paths in Bash commands.

## Tech stack (and absence of one)

- Pure HTML + inline CSS + vanilla JavaScript. No build, no `package.json`, no framework.
- Fonts via Google Fonts CDN — `app/` uses Inter, `a mejorar/candidatura/` uses Fraunces + Inter.
- Maps via Leaflet 1.9.4 (CDN) with CartoDB Dark Matter tiles.
- Deployment target: **Vercel** (static files). The `app/` folder is the deployed subset.

Open any `.html` by double-clicking — no dev server needed. There are no tests, linters, or commands to run.

## Narrative pillars — must be respected

Every document rests on three pillars. Each claim must be traceable to a source document in `a mejorar/`. **Do not invent, do not embellish.**

1. **900 years documented** (1084–2026) — sourced from `a mejorar/INFORME HISTORICO.pdf` by Luis de Escallada González (Centro de Estudios Montañeses, Sociedad Cántabra de Escritores, 15 June 2010). This document lists all key historical milestones, the artífices de Güemes (canteros, escultores, fundidores who built cathedrals in Segovia, Ciudad Rodrigo, Santiago, Oviedo, Pamplona), and the hospital de peregrinos lineage.

2. **"Abriendo caminos de amistad"** — the contemporary project. In **2009**, pilgrim **Bob** from Guemes Island (Washington, USA) arrived at the albergue. Cura **Ernesto Bustio** organized a real trip (Argentina → México → USA) with support from the Consejería de Cultura (libros donados). Four maquetas de acero corten are already installed in **El Portalillo de Güemes** under the project title "Abriendo caminos de amistad". Sourced from `a mejorar/HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES.pdf`.

3. **Hospitalidad peregrina continuous since s. XIV** — the medieval *Hospital de San Julián y Nª Sª de la Consolación* (closed 1800 by Real Cédula) is the antecedent of today's *Albergue La Cabaña del Abuelo Peuto* (founded 1999 by Ernesto Bustio, +50.000 peregrinos from +100 countries, best-rated on the Camino del Norte).

## Factual nuances that are easy to get wrong

The "4 Güemes del mundo" narrative has historical subtleties. Several earlier drafts contained errors — current drafts have been corrected. Keep these straight:

- **Juan Francisco de Güemes y Horcasitas** (1st Conde de Revillagigedo, virrey of Nueva España) was born in **Reinosa**, not in Güemes-Bareyo. Both are in Cantabria, ~80 km apart.
- **Martín Miguel de Güemes** (Argentine hero, 1785–1821) — his father Gabriel came from **Abionzo** (Cantabria), not Güemes-Bareyo.
- The bond between the 4 Güemes (España, México, Argentina, EE.UU.) is **toponymic** (shared surname origin — the apellido itself traces back to the village) + **contemporary** (the 2009 trip). It is NOT a direct birthplace lineage to Güemes-Bareyo for any of the named historical figures. Frame narratives accordingly — the defensible story is *"cuna del apellido"* + *"abriendo caminos de amistad"*, not *"here nació el virrey"*.
- Sources for these facts: Wikipedia ES/EN, Historia Hispánica (Real Academia de la Historia), Biografías y Vidas — all cross-verified.

## Key stakeholders

| Role | Name | Contact |
|---|---|---|
| Presidenta Junta Vecinal de Güemes | Begoña de la Fuente Crespo | via Ayuntamiento Bareyo |
| Presidente Cooperativa Nª Sª de Consolación | Miguel Lavín | — |
| Cura / Fundador del albergue | Padre Ernesto Bustio Crespo | ernestobustio@yahoo.es |
| Ayuntamiento de Bareyo | — | aytobareyo.org |
| Candidacy lead (pro bono) | Clotitec | info@clotitec.com |

## Conflict-of-interest posture

The candidacy is being drafted **pro bono** by Clotitec (info@clotitec.com). The text of the candidacy itself must NOT name Clotitec as a designated service provider for any of the 160 k€ budget lines. Describe services generically ("a specialist digital provider, awarded by the Junta Vecinal through its standard procurement"). If the candidacy wins, Clotitec may compete openly on equal terms — no prior commitment.

## The 4 sculpture locations (coordinates provisional)

| Sculpture | Location in the village | Approx. GPS |
|---|---|---|
| Güemes de España | Centro, junto a Iglesia de San Vicente | 43.4557, -3.6369 |
| Güemes de Argentina | Plazoleta grande, entrada por Galizano | 43.4540, -3.6400 |
| Güemes de México | Parque dirección Meruelo | 43.4565, -3.6340 |
| Güemes de EE.UU. | El Quejigal, cerca de la Ermita San Julián | 43.4553, -3.6378 |

Exact coordinates live in `a mejorar/Estatuas.kml` (a Google My Maps NetworkLink). The provisional values above match the user's location descriptions and should be refined once the KML is resolved.

## Persistent personal memory

A Claude Code auto-memory system is active at `~/.claude/projects/D--------continua-claude-Guemes-2026/memory/` with notes on the user, feedback, project evolution, stakeholder preferences, and source-document summaries. Read `MEMORY.md` there at session start — it complements this `CLAUDE.md` (this one = project facts; memory = how to collaborate).

## Known housekeeping items

- `aerea_*.jpg` files exist in the repo root (21 files, ~4 MB). They are duplicates of the canonical copies in `a mejorar/mapa_hermanos/imagenes/aereas/`. Left over from a failed parallel download. Safe to delete after confirming duplicates (`find ... -name 'aerea_*.jpg'`).
- `Estatuas.kml` only contains a NetworkLink — the actual coordinates live on Google My Maps and need to be exported with "Keep data updated" checked.
- The `app/` HTMLs use a green + gold palette. The new `a mejorar/candidatura/` landing uses a corten-steel + dark navy palette. Both are intentional — the first is the "validated current deployment", the second is the "potent new presentation". Do not harmonize without explicit guidance from the user.

## Source documents worth reading

When generating any new narrative content, read these first:

- `a mejorar/INFORME HISTORICO.pdf` — 15 pages, academic, the historical backbone
- `a mejorar/HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES.pdf` — 11 pages with photos, the contemporary story
- `a mejorar/ERNESTO BUSTIO CRESPO, HISTORIA DEL ALBERGUE Y DEL PERSONAJE.pdf` — context on the central figure
- `ESTADO_PROYECTO.md` — live project status tracker (dates, decisions, pending items)
- `CONVOCATORIA 2026 ORDEN OBR-002-20217.pdf` — the official call (governs what the jury expects)
