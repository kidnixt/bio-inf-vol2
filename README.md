# bio-inf-vol2

Vault de Obsidian del curso **Fronteras y Perspectivas en Bioinformática** — Universidad ORT, 2026.

Punto de entrada: [[Fronteras y Perspectivas en Bioinformática - MOC]]

## Estructura

| Carpeta | Contenido |
|---|---|
| `Clases/Módulo N - .../` | Resumen en Markdown de cada clase + el MOC del módulo |
| `Recursos/` | Notas de conceptos, enlazadas inline desde los resúmenes |
| `Recursos/Lecturas/` | Una nota por paper de lectura (ideas clave, qué aporta respecto de la clase) |
| `Módulo N - .../Clase N - <tema>/` | Material del curso: diapositivas, resumen y `Lecturas/` con los PDFs |

### Subcarpetas de Recursos

- `Biología/` — biología molecular y metabolismo de base
- `Células/` — tipos y estados celulares
- `Técnicas/` — métodos experimentales
- `Herramientas/` — plataformas comerciales, bases de datos y software
- `Bioinformática/` — análisis, algoritmos, desafíos y artefactos
- `Proyectos/` — consorcios y atlas
- `Personas/` — docentes e instituciones
- `Lecturas/` — papers asociados a las clases

## Convenciones

- Los resúmenes enlazan **inline** con wikilinks a las notas de `Recursos/`.
- Cada nota de recurso cierra con una sección **Aparece en** que apunta a las clases (y lecturas) donde se menciona.
- Los nombres de archivo son únicos en todo el vault, así que los links funcionan sin ruta.
- Las variantes de un mismo término se declaran en `aliases:` del frontmatter, no como notas separadas.
- El frontmatter de cada recurso tiene `tags`, `area` (= nombre de su subcarpeta) y `aliases`.
- Los resúmenes se nombran por el **título de la clase**; los PDFs de diapositivas, `Diapositivas - <título>.pdf`.
- En los resúmenes, lo dicho en clase que no está en las diapositivas va en recuadros `> [!quote] En la clase`.

## Agregar una clase nueva

1. Poner el material en `Módulo N - .../Clase N - <tema>/` (renombrar a `Diapositivas - ...`, `Resumen - ...` y `Lecturas/`).
2. Escribir el resumen en `Clases/Módulo N - .../<Título de la clase>.md` leyendo las diapositivas como imagen.
3. Crear las notas de `Recursos/` que falten (incluida una por lectura en `Recursos/Lecturas/`).
4. Actualizar el MOC del módulo, el MOC del curso y las secciones *Aparece en*.
