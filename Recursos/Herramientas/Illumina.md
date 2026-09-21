---
tags: [herramienta, plataforma, secuenciación]
area: Herramientas
aliases: [Solexa, SBS, sequencing by synthesis, MiSeq]
---

# Illumina

La plataforma dominante de [[Secuenciación de segunda generación|secuenciación de lectura corta]], y la referencia contra la que se compara toda tecnología nueva.

## Cómo genera la secuencia

*Sequencing by synthesis* (SBS): el ADN con adaptadores se amplifica sobre una flow cell por **bridge amplification**, formando clusters de copias idénticas. En cada ciclo se incorpora un nucleótido marcado y se toma una imagen; la lectura es la **intensidad y el patrón de fluorescencia de cada cluster en cada ciclo**.

> Illumina = imágenes cíclicas de fluorescencia.

## Prestaciones

| | |
|---|---|
| Longitud | Típicamente 150–300 pb |
| Calidad | **Q30 como benchmark**; mayoría de bases ≥Q30 (~99,9%) |
| Error equivalente | ≤0,1% — 1 error cada 1.000 bases |
| Perfil de error | Predominan **sustituciones** |

## En la clase

Aparece como el punto de comparación en dos lugares:

- En la tabla de [[Perfil de error]], donde marca el estándar de exactitud por base.
- En el estudio suizo de [[Secuenciación 16S|16S]] de baja biomasa (Geers et al., 2026), donde la concordancia con ONT fue del **93,5%**, con sensibilidad ligeramente mayor de Illumina a concentraciones bacterianas muy bajas, pero **~50 h más de tiempo** y **155 vs 35 CHF** por muestra.

La conclusión de ese estudio resume bien la relación entre ambas tecnologías hoy: no es que una reemplace a la otra, sino que **ONT se volvió una alternativa viable y costo-efectiva** en escenarios donde el tiempo importa.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
