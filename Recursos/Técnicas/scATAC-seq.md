---
tags: [técnica, single-cell, epigenómica]
area: Técnicas
aliases: [ATAC-seq, single cell ATAC-seq]
---

# scATAC-seq

**Assay for Transposase-Accessible Chromatin sequencing** a nivel de célula única. Mide la **conformación de la [[Cromatina]]**: qué regiones del genoma están físicamente accesibles y, por lo tanto, disponibles para la transcripción.

## Cómo funciona

Una transposasa Tn5 hiperactiva se inserta preferentemente en el ADN **abierto** y, al hacerlo, deja adaptadores de secuenciación en el sitio de inserción. Sólo las regiones accesibles quedan marcadas; las regiones compactadas (heterocromatina) quedan protegidas.

```
Cromatina abierta  ──Tn5──►  fragmentos con adaptadores  ──►  se secuencian
Cromatina cerrada  ──Tn5──►  (sin inserción)
```

## Qué aporta sobre el scRNA-seq

Mide el nivel regulatorio **anterior** a la transcripción:

| | [[scRNA-seq]] | scATAC-seq |
|---|---|---|
| Mide | Qué se está expresando | Qué **puede** expresarse |
| Señal | Conteos de [[ARN mensajero]] | Picos de accesibilidad |
| Revela | Estado transcripcional actual | Elementos regulatorios activos, enhancers, sitios de unión de factores de transcripción |

Permite detectar genes "preparados" (accesibles pero aún silenciosos), típicos de células en transición — ver [[Pseudotiempo]].

## Desafíos propios

Es aún **más escaso** que el scRNA-seq: cada locus tiene sólo 2 copias por célula diploide, así que la matriz resultante es casi binaria y la [[Sparsity]] es extrema. Combinarlo con expresión en las mismas células es uno de los objetivos de la [[Integración de datos multiómicos]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
