---
tags: [herramienta, software, epigenética, metagenómica]
area: Herramientas
aliases: [nanodisco, fanglab/nanodisco]
---

# Nanodisco

Herramienta para descubrir **[[Metilación del ADN|metilación del ADN bacteriano]]** *de novo* a partir de datos de [[Secuenciación con nanoporos|nanoporos]], tanto en bacterias individuales como en microbiomas completos.

`https://github.com/fanglab/nanodisco`

Desarrollada junto con el trabajo de **Tourancheau et al.** (*Nature Methods*), *Discovering multiple types of DNA methylation from bacteria and microbiome using nanopore sequencing*.

## Qué resuelve

Detecta los **tres tipos principales de metilación bacteriana** —**6mA, 4mC y 5mC**— directamente de la señal, sin conversión con bisulfito y **sin conocer de antemano los motivos** a buscar. Compara la corriente observada contra la de una muestra amplificada por PCR (sin modificaciones) para aislar la desviación atribuible a la modificación.

## Para qué se usa

Su aplicación principal en metagenómica no es epigenética en sentido clásico, sino de **asignación**:

> Las metilaciones se utilizan principalmente como **huellas epigenéticas naturales para identificar y relacionar componentes del metagenoma**.

Cada especie bacteriana tiene su propio repertorio de metiltransferasas y por lo tanto su propia firma de motivos metilados. Esa firma permite decidir a qué genoma pertenece un contig o un [[Plásmido|plásmido]] — un problema de *binning* que con composición y cobertura solas suele quedar ambiguo.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
