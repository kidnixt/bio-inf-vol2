---
tags: [técnica, single-cell, multiomica, proteomica]
area: Técnicas
aliases: [REAP-seq, cellular indexing of transcriptomes and epitopes by sequencing]
---

# CITE-seq

*Cellular Indexing of Transcriptomes and Epitopes by sequencing*. Mide en **la misma célula** el transcriptoma y la abundancia de **proteínas de superficie**, convirtiendo la información de proteína en **ADN secuenciable**. REAP-seq es un método equivalente.

## Cómo funciona

- Cada anticuerpo contra una proteína de superficie lleva conjugado un **barcode de ADN con cola poli-A**.
- En un experimento de [[scRNA-seq]] en gotas, los primers poly(dT) del bead capturan ese barcode **igual que a un ARNm**, y queda marcado con el mismo [[Barcode celular]].
- Al secuenciar, se cuentan los barcodes de anticuerpo → nivel de cada proteína por célula.

Ventaja frente a la [[Citometría de flujo]]: no hay límite por solapamiento de fluoróforos — el número de barcodes posibles es 4ᴺ — y escala a millones de células.

## Por qué importa

Hay subtipos celulares casi indistinguibles por ARN (por la [[Sparsity|escasez de detección]]) pero claros por proteína: el ejemplo típico son los **linfocitos T de memoria y regulatorios**. El análisis conjunto de ambas modalidades resuelve estados que ninguna resuelve sola → [[Integración de datos multiómicos]].

Límite: extenderlo a proteínas **intracelulares** es difícil, porque permeabilizar la célula degrada el ARN.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
