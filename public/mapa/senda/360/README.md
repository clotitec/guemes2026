# Tour 360° — Senda de las Estatuas

Esta carpeta contiene las fotografías equirectangulares (360°) que alimentan el visor inmersivo del mapa de la Senda.

## Cómo añadir nuevas escenas

1. **Coloca el archivo .jpg aquí** (ej: `iglesia.jpg`).
   - Formato: equirectangular 2:1, idealmente 6000×3000 a 8000×4000 px.
   - Compresión recomendada: JPG calidad 80, AVIF/WebP también soportados.
   - Si el archivo trae metadatos XMP `ProjectionType=equirectangular` (Insta360, Theta, DJI), Photo Sphere Viewer los detecta automáticamente.

2. **Edita `TOUR_SCENES` en `../index.html`** (busca el bloque `// TOUR 360°`).

   Mínimo viable:
   ```js
   {
     id: 'iglesia',
     poi: 'mon:iglesia',                  // vincula al POI del mapa
     panorama: '360/iglesia.jpg',
     name: 'Iglesia de San Vicente Mártir',
     caption: 'Inicio de la Senda',
     links: [{ nodeId: 'portalillo' }]    // escenas vecinas
   }
   ```

3. **Vínculos `poi`** — formato `kind:id` donde:
   - `statue:es | ar | us | mx`
   - `mon:iglesia | palacio | ermita | albergue`
   - O `null` si la escena no está atada a un POI existente

4. **Posicionamiento de las flechas entre escenas** (`links[].position`):
   ```js
   links: [
     { nodeId: 'portalillo', position: { yaw: '90deg', pitch: 0 } }
   ]
   ```
   Si lo dejas vacío, PSV las calcula automáticamente desde las coordenadas GPS.

## Ejemplo completo (4 escenas conectadas)

```js
const TOUR_SCENES = [
  {
    id: 'iglesia',
    poi: 'mon:iglesia',
    panorama: '360/iglesia.jpg',
    name: 'Iglesia de San Vicente Mártir',
    caption: 'Inicio de la Senda',
    links: [{ nodeId: 'portalillo' }]
  },
  {
    id: 'portalillo',
    panorama: '360/portalillo.jpg',
    name: 'El Portalillo',
    caption: 'Las 4 maquetas históricas',
    links: [{ nodeId: 'iglesia' }, { nodeId: 'ermita' }],
    gps: [-3.6378, 43.4553]
  },
  {
    id: 'ermita',
    poi: 'mon:ermita',
    panorama: '360/ermita.jpg',
    name: 'Ermita de San Julián',
    caption: 'Hospital medieval de peregrinos',
    links: [{ nodeId: 'portalillo' }, { nodeId: 'albergue' }]
  },
  {
    id: 'albergue',
    poi: 'mon:albergue',
    panorama: '360/albergue.jpg',
    name: 'Albergue La Cabaña del Abuelo Peuto',
    caption: 'Origen del proyecto, 2009',
    links: [{ nodeId: 'ermita' }]
  }
];
```

## Convenciones de nombres recomendadas

| Archivo                    | POI vinculado    |
|----------------------------|------------------|
| `iglesia.jpg`              | `mon:iglesia`    |
| `ermita.jpg`               | `mon:ermita`     |
| `palacio.jpg`              | `mon:palacio`    |
| `albergue.jpg`             | `mon:albergue`   |
| `portalillo.jpg`           | (sin POI)        |
| `plazoleta-espana.jpg`     | `statue:es`      |
| `plazoleta-argentina.jpg`  | `statue:ar`      |
| `plazoleta-eeuu.jpg`       | `statue:us`      |
| `plazoleta-mexico.jpg`     | `statue:mx`      |

## Optimización antes de subir

```bash
# Reducir a 6000px de ancho (manteniendo 2:1)
ffmpeg -i input.jpg -vf scale=6000:3000 -q:v 4 output.jpg

# O con ImageMagick
magick input.jpg -resize 6000x3000 -quality 80 output.jpg
```
