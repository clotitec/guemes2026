# Güemes 2026 — Candidatura al Premio Pueblo de Cantabria

Sitio web oficial de la candidatura de Güemes (Bareyo, Cantabria) al **Premio Pueblo de Cantabria 2026** (Orden OBR/2/2017 del Gobierno de Cantabria).

🌐 **URL pública**: (pendiente de desplegar en Vercel)

---

## Qué hay aquí

Este repositorio contiene el sitio web de la candidatura + la documentación oficial + los materiales de fuente utilizados para redactarla.

### `public/` — lo que se sirve en la web

```
public/
├── index.html                  Landing narrativa (10 secciones + hub de documentos)
├── mapa/                       Mapa mundial interactivo de los 4 Güemes
│   ├── mapa_mundial_hermanos.html
│   └── imagenes/               Fotos de ubicaciones + 23 vistas aéreas
├── docs/                       11 documentos oficiales de la candidatura
│   ├── resumen-ejecutivo.html
│   ├── memoria-actuacion.html
│   ├── memoria-economica.html
│   ├── dossier-historico.html
│   ├── estrategia-puntuacion.html
│   ├── itinerario-jurado.html
│   ├── guemes-en-bolas.html       ← Propuesta "Enróllate en Güemes"
│   ├── cartas-apoyo.html
│   ├── acta-junta.html
│   ├── checklist.html
│   └── index.html                 ← antigua landing (secundaria)
└── archivos/                   PDFs y fuentes documentales
    ├── historia-viaje-cuatro-guemes.pdf
    ├── informe-historico.pdf
    ├── albergue-ernesto-bustio.pdf
    ├── convocatoria-oficial.pdf
    └── ruta-circular-guemes.gpx
```

### Resto del repositorio — materiales de trabajo

```
01_Convocatoria/ ... 06_Memoria_Actuacion/   Versiones originales numeradas por bloque
app/                                          Versión desplegada anterior (11 HTMLs)
propuesta/  (antes "a mejorar")               Carpeta de trabajo en curso — NO se despliega
CLAUDE.md                                     Guía para instancias futuras de Claude Code
ESTADO_PROYECTO.md                            Tracker de estado del proyecto
```

---

## Cómo ejecutar en local

Sin build, sin dependencias. Abre cualquier HTML con doble clic:

```bash
# Homepage
open public/index.html

# O levanta un servidor rápido (recomendado para que funcione el iframe)
cd public && python3 -m http.server 8000
# → http://localhost:8000
```

---

## Cómo desplegar en Vercel

Este repo está configurado para deploy automático con Vercel:

1. Importar el repositorio en [vercel.com/new](https://vercel.com/new)
2. **Root Directory**: `public`
3. **Framework preset**: Other (static)
4. **Build command**: (vacío)
5. Deploy

La configuración en `vercel.json` incluye `cleanUrls`, headers de seguridad y cache optimizado para las imágenes y PDFs.

Cada push a `main` dispara un redeploy automático.

---

## Datos del proyecto

| Campo | Valor |
|---|---|
| Solicitante | Junta Vecinal de Güemes (Bareyo, Cantabria) |
| Habitantes | 301 (INE 2024) |
| Presupuesto candidatura | 160.000 € |
| Plazo presentación | 4 de mayo de 2026 |
| Junta Vecinal aprobatoria | 13 de abril de 2026 |
| Reunión pública | 19 de abril de 2026 |

### Los 4 bloques del presupuesto

- **A — 60.000 €** · Senda de las Estatuas (4 esculturas acero corten)
- **B — 45.000 €** · Preservación del pueblo + 14 km del Camino de Santiago
- **C — 15.000 €** · "Enróllate en Güemes" (festival de arte rural)
- **D — 40.000 €** · Pádel, atletismo, Centro de Interpretación Digital en Ermita San Julián

---

## Contactos

- **Junta Vecinal**: Begoña de la Fuente Crespo (presidenta)
- **Albergue La Cabaña del Abuelo Peuto**: Padre Ernesto Bustio — ernestobustio@yahoo.es
- **Ayuntamiento de Bareyo**: aytobareyo.org
- **Redacción candidatura (pro bono)**: Clotitec · info@clotitec.com

---

## Fuentes documentales

Todos los datos históricos proceden de fuentes verificables:

- **INFORME HISTÓRICO** · Luis de Escallada González · Centro de Estudios Montañeses · 15 junio 2010
- **HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES** · Albergue de Güemes · Crónica del viaje 2009
- **Wikipedia, Biografías y Vidas, Historia Hispánica (RAH)** · Biografías cruzadas

---

*"Güemes no se inventa una historia para el premio. Güemes cuenta una historia que ya lleva 900 años ocurriendo."*
