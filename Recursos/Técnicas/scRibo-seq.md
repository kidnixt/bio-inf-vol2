---
tags: [técnica, single-cell, traductómica]
area: Técnicas
aliases: [Ribo-seq, ribosome profiling, Ribo-STAMP, single cell Ribo-seq]
---

# scRibo-seq (ribosome profiling)

Mide **eventos traduccionales**: qué ARNs están siendo efectivamente leídos por ribosomas en un momento dado. Ver [[Traducción]].

## Cómo funciona

Se digiere con nucleasa todo el ARN que **no** está protegido por un ribosoma. Lo que sobrevive son los *ribosome footprints* — fragmentos de ~28-30 nt correspondientes exactamente a la posición del ribosoma sobre el transcripto. Se secuencian esos fragmentos.

El resultado es un mapa de **qué se traduce, dónde sobre el ARNm y cuánto**, con resolución de codón.

## Por qué no basta con el transcriptoma

La correlación entre abundancia de ARNm y abundancia de proteína es baja. Un transcripto presente puede estar reprimido o secuestrado sin traducirse. El [[Transcriptoma]] no distingue esos casos; el Ribo-seq sí.

## El desafío en célula única

Es una de las ómicas single-cell más difíciles: la clase destaca la necesidad de trabajar en **micro volúmenes (~50 nL)** para no diluir el escasísimo material de una sola célula.

**Ribo-STAMP** es la alternativa que menciona la clase: en lugar de digerir y secuenciar footprints, fusiona una enzima editora de ARN (APOBEC) a una proteína ribosomal; los ARNs que pasan por el ribosoma quedan **marcados por edición de base**, y esa marca se lee en un [[scRNA-seq]] convencional. Evita el paso bioquímico delicado a costa de resolución.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
