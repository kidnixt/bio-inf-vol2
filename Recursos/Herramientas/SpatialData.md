---
tags: [herramienta, software, espacial, datos]
area: Herramientas
aliases: [SpatialData framework]
---

# SpatialData

Framework abierto (Python) para **guardar, alinear, consultar y visualizar** datos de ómicas espaciales de cualquier plataforma. Es la respuesta que muestra la clase al desafío *"Storage and Visualization!"* → [[Almacenamiento y visualización]].

## Qué ofrece (según la figura de la clase)

| Componente | Qué hace |
|---|---|
| **Formato de almacenamiento** | Un solo formato para **tablas, puntos, formas, etiquetas e imágenes**, sobre **OME-NGFF / Zarr** (almacenamiento por bloques, multiescala, compatible con la nube) |
| **Librería de Python** | Datasets **alineados espacialmente**; transformaciones (trasladar, escalar, rotar, encadenar); **consultas espaciales**; agregación de observaciones por región |
| **Lectores** | Importa datos de [[Xenium]], [[Visium]], [[CosMx SMI]], IMC, CyCIF… |
| **Anotación y visualización interactiva** | Dibujar regiones sobre la imagen y explorar |
| **Interfaz de [[Deep Learning]]** | Conexión con **PyTorch** |
| **Integración con el ecosistema** | Herramientas de imagen médica y de análisis single cell |

## Por qué hace falta

Un solo experimento espacial por imagen puede generar **de cientos de GB a TB** de imágenes. Los formatos por bloques permiten leer solo lo necesario sin cargar todo en memoria — pero comprimir o submuestrear con descuido puede borrar señales débiles de transcriptos poco abundantes ([[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou 2026]]).

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]] *(lectura)*
