---
tags: [concepto, biología]
area: Biología molecular
aliases: [transcriptomas, transcriptómica]
---

# Transcriptoma

> **La colección completa de todas las moléculas de ARN presentes en una célula o tejido en un momento dado.**

Medir un transcriptoma responde dos preguntas:

1. **¿Qué genes se están expresando?**
2. **¿En qué nivel?**

A diferencia del genoma, que es esencialmente el mismo en todas las células de un organismo, el transcriptoma es **dinámico**: cambia con el tipo celular, el [[Estado celular]], el momento del desarrollo, la hora del día y cualquier estímulo.

## El rango dinámico

Un punto crítico y muchas veces subestimado: la abundancia de transcriptos abarca varios órdenes de magnitud dentro de la misma célula. Ver [[Rango dinámico]].

| Gen | Orden de abundancia | Tipo |
|---|---|---|
| GAPDH | ~10⁵ | housekeeping |
| ACTB | ~10⁴ | housekeeping |
| MAP2 | ~10³ | estructural neuronal |
| RBFOX3 | ~10² | marcador neuronal (NeuN) |
| TREM2 | ~10¹ | marcador de [[Microglía]] |
| NANOG | ~10⁰ | factor de transcripción |

Los genes **más informativos biológicamente** (marcadores, factores de transcripción) suelen estar en la parte baja de esa escala. Esto explica por qué la [[Profundidad de secuenciación]] y la [[Sparsity]] importan tanto en [[scRNA-seq]].

## Cómo se mide

- A nivel de muestra: [[Bulk RNA-seq]] → [[Matriz de conteo]] de genes × condiciones
- A nivel de célula: [[scRNA-seq]] → matriz de genes × células
- A nivel de célula **y posición**: [[Transcriptómica espacial]]

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
