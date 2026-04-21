# Mapa Mundial de los 4 Güemes — "Abriendo Caminos de Amistad"

Animación interactiva bilingüe para la candidatura de Güemes (Bareyo, Cantabria) al Premio Pueblo de Cantabria 2026.

**Versión 3** — vista mundial + vista local + Street View + bilingüe + **visor aéreo con 23 fotos descargadas localmente**.

---

## Qué hace

### 🌍 Vista mundial (modo por defecto)
- Mapa oscuro cinematográfico centrado en el Atlántico
- 4 pines dorados pulsantes: Güemes (ES), General Güemes (AR), Güémez (MX), Guemes Island (USA)
- **Líneas arqueadas animadas** que se dibujan en secuencia desde Güemes hacia los 3 hermanos
- Panel lateral con **foto + ficha histórica** de cada lugar
- Se puede navegar manualmente clicando pines o leyenda

### 🏘️ Vista local (desde botón "Ver el pueblo")
- Zoom automático sobre Güemes-Bareyo
- 7 puntos de interés con etiquetas:
  - 4 estatuas de acero corten (España, Argentina, México, EE.UU.)
  - Iglesia de San Vicente Mártir
  - Ermita de San Julián
  - Albergue La Cabaña del Abuelo Peuto
- Cada punto abre su ficha con historia breve

### 🚶 Street View embebido
- Botón "Caminar por la ruta" abre un modal con la vista Street View de:
  - La ruta de la Iglesia + Hospital de Peregrinos
  - El Albergue
- Se cierra con ✕ o ESC

### 🌐 Bilingüe ES / EN
- Toggle arriba-derecha cambia toda la interfaz (títulos, fichas, leyenda)
- Versión inglesa pensada para Bob y la comunidad de Guemes Island, para que puedan leer el proyecto

### 📸 Visor aéreo (nuevo en v3)
- **23 fotografías aéreas de Güemes descargadas localmente** en `imagenes/aereas/`
- Botón **"Visor aéreo"** arriba-derecha (o desde la ficha de Güemes-España)
- Vista grid con thumbnails + click para abrir fullscreen
- Navegación con flechas ← → del teclado o botones laterales
- Funciona **offline** una vez descargada la carpeta
- Cierre con ✕ o ESC

---

## Cómo usarlo

### Abrir localmente
Doble clic en `mapa_mundial_hermanos.html`. Necesita conexión para cargar tiles de mapa y fuentes.

### Embeber en una web
Subir la carpeta entera y usar un iframe:

```html
<iframe
  src="/ruta/mapa_mundial_hermanos.html"
  style="width:100%; height:100vh; border:none;"
  title="Abriendo Caminos de Amistad">
</iframe>
```

---

## Datos verificados

### Los 4 Güemes del mundo

| País | Lugar | Desde | Población | Distancia | Fuente |
|---|---|---|---|---|---|
| 🇪🇸 España | Güemes (Bareyo, Cantabria) | 1084 | 301 | — | Informe L. Escallada 2010 |
| 🇦🇷 Argentina | General Güemes (Salta) | 1888 | 56.948 | 10.400 km | Wikipedia + INDEC 2022 |
| 🇲🇽 México | Güémez (Tamaulipas) | 1749 | 1.731 | 8.750 km | Wikipedia + INEGI 2020 |
| 🇺🇸 EE.UU. | Guemes Island (Washington) | 1791 | ~600 | 8.100 km | Wikipedia EN |

### Puntos de la vista local (Güemes-Bareyo)

| Punto | Coordenadas | Tipo |
|---|---|---|
| Estatua España | 43.4557, -3.6369 | Futura escultura |
| Estatua Argentina | 43.4540, -3.6400 | Futura escultura (provisional) |
| Estatua México | 43.4565, -3.6340 | Futura escultura (provisional) |
| Estatua EE.UU. | 43.4553, -3.6378 | Futura escultura (provisional) |
| Iglesia de San Vicente | 43.4555278, -3.6363889 | Patrimonio siglo XI–XVII |
| Ermita de San Julián | 43.4553692, -3.6371699 | Patrimonio siglo XII–XIII |
| Albergue La Cabaña del Abuelo Peuto | 43.4477667, -3.6446 | Fundado 1999 |

> ⚠️ **Las coordenadas de las 4 estatuas son PROVISIONALES** hasta que se extraiga el KML definitivo desde Google My Maps. Para ajustarlas, editar el objeto `LOCAL_POI` en el bloque `<script>` del HTML.

---

## Tecnología

- HTML5 + CSS3 + JavaScript vanilla — **un solo archivo**, sin build, sin dependencias Node
- [Leaflet 1.9.4](https://leafletjs.com/) — mapa interactivo
- [CartoDB Dark Matter](https://carto.com/attributions) — tiles oscuros libres
- Google Fonts: [Fraunces](https://fonts.google.com/specimen/Fraunces) + [Inter](https://fonts.google.com/specimen/Inter)
- Google Maps Embed API — Street View

---

## Archivos

```
mapa_hermanos/
├── mapa_mundial_hermanos.html    ← archivo principal (1025 líneas)
├── README.md                      ← este archivo
└── imagenes/
    ├── ESPANA.jpeg                (plazoleta junto a Iglesia San Vicente)
    ├── ARGENTINA.jpeg             (plazoleta de entrada por Galizano)
    ├── MEXICO.jpeg                (plazoleta dirección Meruelo)
    ├── EEUU.jpeg                  (camino junto a la Ermita)
    └── aereas/
        ├── aerea_01.jpg … aerea_23.jpg   (23 vistas aéreas del pueblo y entorno)
```

Tamaño total de la carpeta: ~24 MB (incluye las 23 fotos aéreas descargadas localmente para que la galería funcione incluso sin conexión a Google).

---

## Cambios fáciles para iteraciones futuras

### Editar textos (ES o EN)
Buscar el objeto `PUEBLOS` o `LOCAL_POI` dentro del `<script>`. Cada entrada tiene bloques `es:` y `en:` con los textos editables.

### Cambiar coordenadas de las 4 estatuas
Editar `LOCAL_POI.estatua_*.coords` con las coordenadas definitivas del KML.

### Ajustar velocidad de la narrativa
Editar los `setTimeout` dentro de `startNarrative()`. Actualmente: 1.8s → 3.8s → 7.2s → 10.6s → 14.8s.

### Añadir más Street Views
Ampliar el objeto `STREETVIEW` con nuevas entradas `{ pano, coords, heading, pitch, titleKey }`.

### Añadir más idiomas
Duplicar el bloque `es:` dentro de cada entrada de `PUEBLOS` y `LOCAL_POI`, añadir la clave (`fr`, `de`, `it`) al objeto `I18N` con las traducciones, y ampliar `toggleLang()` para ciclar.

### Embeber fotos aéreas específicas
Cuando el usuario seleccione 4-6 imágenes aéreas, colocarlas en `imagenes/aereas/` y reemplazar el botón "Galería aérea" por una galería modal integrada.

---

## Fuentes documentales

- **INFORME HISTÓRICO** firmado por Luis de Escallada González (Centro de Estudios Montañeses, Sociedad Cántabra de Escritores), 15 junio 2010
- **HISTORIA DEL VIAJE POR LOS CUATRO GÜEMES** — crónica del viaje 2009 de Ernesto Bustio a Argentina, México y Estados Unidos con apoyo de la Consejería de Cultura del Gobierno de Cantabria
- **El Tribuno de Salta** — artículo "Travesía para llegar al origen del apellido Güemes"
- **Casa de Cantabria en Ciudad de México** — encuentro con directivos (ver fotografías del viaje)
- **Wikipedia ES/EN, Biografías y Vidas, Historia Hispánica (RAH)** — datos biográficos de los Güemes históricos

---

## Para aprobar

Enviar esta carpeta (comprimida en zip o subida a Google Drive/OneDrive) a:
- Junta Vecinal de Güemes (Begoña de la Fuente Crespo)
- Cooperativa Nª Sª de Consolación (Miguel Lavín)
- Padre Ernesto Bustio (albergue)
- Ayuntamiento de Bareyo

El receptor solo necesita abrir `mapa_mundial_hermanos.html` con doble clic. No requiere instalación.
