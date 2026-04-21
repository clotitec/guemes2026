# Güemes · Candidatura Pueblo de Cantabria 2026

Página única de presentación de la candidatura — diseñada como **landing narrativa tipo editorial** para que el jurado entienda en un solo scroll los 900 años de Güemes, el proyecto "Abriendo Caminos de Amistad" y el plan de actuación de 160.000 €.

---

## Qué contiene (11 secciones)

1. **Hero** — Título cinematográfico con fondo aéreo rotativo (4 fotos alternándose)
2. **El pueblo** — 4 contadores: 301 hab. · 942 años · 50.000 peregrinos · 4 Güemes en el mundo
3. **Origen** — Timeline vertical con 10 hitos de 1084 a 2026
4. **Los artífices** — 6 canteros y fundidores de Güemes que levantaron catedrales (Segovia, Ciudad Rodrigo, Pamplona, Santiago, Oviedo)
5. **El Camino** — Hospital medieval de San Julián → Albergue La Cabaña del Abuelo Peuto
6. **Abriendo caminos de amistad** — El encuentro Ernesto + Bob en 2009 y el viaje a los 4 Güemes
7. **Los 4 Güemes del mundo** — **Mapa interactivo embebido** (iframe del `mapa_hermanos/`)
8. **La Senda propuesta** — 4 cards de las ubicaciones reales con fotos actuales
9. **Plan de actuación** — Los 4 bloques de presupuesto (60k + 45k + 15k + 40k)
10. **Implicación vecinal** — La reunión del 19 abril 2026, vecinos voluntarios limpiando el pueblo
11. **Cierre** — Quién lidera + Contactos + Plazo

---

## Cómo abrirlo

**Doble clic en `index.html`**. Se abre en cualquier navegador (Chrome, Edge, Firefox, Safari).

Requiere conexión a internet para cargar:
- Las fuentes de Google Fonts (Fraunces + Inter)
- Los tiles del mapa mundial embebido

Las **23 fotografías aéreas y las 4 fotos de ubicaciones ya están descargadas localmente** en `../mapa_hermanos/imagenes/`.

---

## Estructura de archivos

```
a mejorar/
├── candidatura/
│   ├── index.html          ← ESTE archivo (página principal)
│   └── README.md           ← este README
└── mapa_hermanos/          ← el mapa mundial interactivo (embebido vía iframe en candidatura)
    ├── mapa_mundial_hermanos.html
    └── imagenes/
        ├── ESPANA.jpeg  ARGENTINA.jpeg  MEXICO.jpeg  EEUU.jpeg
        └── aereas/
            └── aerea_01.jpg ... aerea_23.jpg
```

⚠️ **Importante**: la página `candidatura/index.html` referencia imágenes del directorio hermano `mapa_hermanos/`. No mover `candidatura/` fuera del directorio padre sin mover también `mapa_hermanos/`, o la galería y el mapa se romperán.

---

## Para enviar al jurado

### Opción A — Carpeta comprimida
1. Seleccionar ambas carpetas (`candidatura/` + `mapa_hermanos/`) → comprimir en ZIP
2. Enviar por email o Google Drive
3. El receptor descomprime y abre `candidatura/index.html`

### Opción B — Publicación web
1. Subir `a mejorar/` entero a un subdominio (por ejemplo: `guemes2026.aytobareyo.org` o `clotitec.github.io/bareyo2026`)
2. Apuntar la URL principal a `/candidatura/index.html`
3. Generar **QR** de esa URL para imprimir en el dossier físico

### Opción C — Vercel / Cloudflare Pages (gratis, 5 minutos)
1. Crear repo en GitHub con la carpeta `a mejorar/`
2. Conectar Vercel/Cloudflare Pages al repo
3. Obtener URL pública `nombre.vercel.app` o similar

---

## Editar contenido

Todo el contenido está en **HTML plano** dentro del `<body>` del `index.html`. No hay backend, no hay CMS. Para cambios pequeños:

### Editar texto
Buscar el texto a cambiar en el HTML y reemplazarlo. Los textos están claramente separados por secciones con comentarios `<!-- SECCIÓN -->`.

### Cambiar fotos del hero
Buscar el array `heroImages` en el `<script>` al final del archivo y reemplazar las rutas.

### Cambiar colores
Buscar `:root { ... }` al inicio del `<style>`. Ahí están las variables:
- `--corten-br` → dorado brillante (acentos)
- `--bg-deep` → azul oscuro (fondo principal)
- `--text` → color de texto principal

### Añadir/eliminar stats, hitos, bloques
Cada uno es un bloque HTML replicable (`<div class="stat">`, `<div class="tl-item">`, `<div class="bloque">`). Copiar uno existente y modificar los valores.

### Cambiar presupuesto
Los 4 bloques están en la sección `#plan`. Editar los valores directamente.

---

## Tecnología

- HTML5 + CSS3 + JavaScript vanilla — **un solo archivo**, sin build, sin dependencias npm
- [Fraunces](https://fonts.google.com/specimen/Fraunces) (tipografía editorial serif) + [Inter](https://fonts.google.com/specimen/Inter) (tipografía sans)
- IntersectionObserver nativo para animaciones scroll-revelado
- `<iframe>` embebiendo el mapa mundial ya construido
- Paleta cromática inspirada en el acero corten de las esculturas

**Peso total**: ~35 KB de HTML/CSS/JS + las imágenes referenciadas (~24 MB en `mapa_hermanos/imagenes/`).

---

## Diseño

Inspirado en landings editoriales tipo **The New York Times long-form** y **Apple product pages**:

- **Contraste oscuro** para seriedad y foco
- **Tipografía italic grande** en títulos para transmitir emoción
- **Scroll narrativo** — cada sección es un capítulo
- **Números grandes** en los stats, como se hace en reportajes periodísticos
- **Fotos inmersivas** de las ubicaciones reales del pueblo (no stock)
- **Pull quotes** en momentos emocionales para pausar al lector

---

## Próximas mejoras sugeridas

- [ ] Botón de descarga del dossier PDF oficial de la candidatura
- [ ] Versión inglesa completa (ya existe toggle ES/EN en el mapa embebido)
- [ ] Reproductor de vídeo aéreo en el hero (cuando se grabe con dron)
- [ ] Galería adicional con fotos históricas de los artífices (si las aporta el Centro de Estudios Montañeses)
- [ ] Sección "Dónde dormir / cómo llegar" para peregrinos y visitantes tras el premio

---

## Fuentes documentales

- **INFORME HISTÓRICO** firmado por Luis de Escallada González (Centro de Estudios Montañeses, Sociedad Cántabra de Escritores), 15 junio 2010 — *localizado en la carpeta `a mejorar/`*
- **HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES** — crónica del viaje 2009 organizado por Ernesto Bustio con apoyo de la Consejería de Cultura del Gobierno de Cantabria — *localizado en la carpeta `a mejorar/`*
- **Wikipedia ES/EN, Biografías y Vidas, Historia Hispánica (Real Academia de la Historia)** — datos biográficos y de los pueblos hermanos
- **El Tribuno de Salta** — cobertura del viaje: "Travesía para llegar al origen del apellido Güemes"
- **Catastro del Marqués de la Ensenada (1753)** — 115 vecinos, 22 maestros canteros

---

*Generado como propuesta de landing principal para la candidatura. Revisar y validar con la Junta Vecinal y el Ayuntamiento de Bareyo antes de publicación pública.*
