---
tags: [herramienta, software, pipeline, metagenómica]
area: Herramientas
aliases: [porefile, microgenlab/porefile]
---

# Porefile

Pipeline en **Nextflow** para perfilado de **[[Secuenciación 16S|16S de largo completo]]** con lecturas de [[Secuenciación con nanoporos|nanoporos]], desarrollado en el laboratorio de microbiología y genómica de Montevideo.

`https://github.com/microgenlab/porefile` · Nextflow 22.10.2

## El flujo

| Paso | Herramienta |
|---|---|
| Lecturas 16S crudas | — |
| Filtrado | **Nanofilt** v2.8.0 |
| Control de calidad | **NanoPlot** v1.41.0 → QC summary |
| Mapeo contra base de referencia | **Minimap2** v2.24 contra **SILVA** |
| [[Clasificación taxonómica]] | **MEGAN6 LCA** v6.24.20 (vía `rma2sam`) |
| Salida | Tablas de conteo y taxonomía |
| Estimación final | Abundancia relativa (con opción de reducir la base de datos) |

El uso de **LCA** (*lowest common ancestor*) es la decisión de diseño característica: en lugar de forzar una asignación a especie que la lectura no sostiene, asigna cada read al taxón más específico que sea compatible con todos sus buenos alineamientos.

## Aplicaciones

- **Identificación de aislamientos bacterianos.**
- **Caracterización de comunidades procariotas y eucariotas** — no solo bacterias, lo que lo distingue de los pipelines 16S clásicos.

Que esté escrito en Nextflow no es un detalle menor: la **reproducibilidad** del análisis es, según el cierre de la clase, uno de los dos cuellos de botella de la [[Metagenómica clínica|metagenómica clínica]]. Conecta con los temas del [[Módulo 4 - MOC|Módulo 4]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
