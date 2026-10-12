# Web_3D — Visualizador 3D de modelos anatómicos (MedicalBit)

Visor WebGL que corre en el navegador para inspeccionar los modelos anatómicos en 3D usados en el
entrenamiento quirúrgico simulado. Está hecho sobre **three.js** vendorizado: no necesita build ni
servidor de aplicaciones, se abre y funciona.

## Cómo se usa

Los `.stl` se cargan por ruta relativa, así que conviene servirlo con un servidor estático local
(abrir el archivo con `file://` falla por CORS):

```bash
python3 -m http.server 8000     # y abrir http://localhost:8000/index.html
```

| Archivo | Para qué |
| --- | --- |
| `index.html` | Visor del caso: carga las mallas `Klem-Ant.stl`, `Klem-Post.stl` y `tacoff-abdm-1-3.stl` |
| `visor-modelo-ICBA02.html`, `visor-modelo-ICBA03.html`, `visor-modelo-TAG2-ICBA.html`, `visor-modelo-Tagacoff-ICBA.html`, `visor-modelo-PatricioZ-ICBA.html` | Un visor por modelo/caso |
| `visor-modelos-STL.html` | Visor genérico de STL |
| `Ejemplo_playCanvas.html` | Prueba de concepto alternativa (three.js) |

## Cómo está hecho

- **three.js** en `build/` + `js/` (loaders, controles y utilidades vendorizadas: `STLLoader`,
  `OrbitControls`, `stats`, `dat.gui`, `draco`, `mmdparser`, `rhino3dm`, entre otras).
- `index.html` arma la escena: cámara en perspectiva, `MeshPhongMaterial`, `STLLoader` para STL
  binario, `OrbitControls` y un HUD de FPS con `stats.min.js`.
- `js/WebGL.js` — detección de soporte WebGL/WebGL2 con mensaje de error propio si el navegador no
  lo soporta.

## Estructura

```
index.html                 visor principal del caso
visor-modelo-*.html        visores por modelo / caso
models/stl/binary/*.stl    mallas anatómicas
models/stl/ascii/*.stl     mallas de ejemplo (PR2, disco ranurado)
build/three.js             librería three.js
js/loaders  js/controls    STLLoader, OrbitControls
js/libs                    utilidades de three.js
logomedicalbit-12.png      logo
```

## Contexto

Parte del toolkit de **MedicalBit** (startup de tecnología médica): simulador laparoscópico para
entrenamiento y modelos anatómicos impresos en 3D. Este visor es la pieza web que se usaba para
revisar cada modelo antes de imprimirlo.
