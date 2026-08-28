---
tags: [técnica, espacial]
area: Técnicas
aliases: [hibridación de sondas, imaging-based, métodos de imagen, in situ hybridization]
---

# Métodos basados en sondas (hibridación)

Una de las dos grandes familias de la [[Transcriptómica espacial]]. Los transcriptos se detectan **directamente sobre el tejido intacto**, mediante sondas fluorescentes complementarias a secuencias conocidas, y se leen por microscopía en rondas sucesivas de hibridación.

## Principio

```
Tejido intacto  ──►  hibridación de sondas  ──►  imagen  ──►  desmontaje  ──►  siguiente ronda
```

Cada gen recibe un **código de colores a lo largo de las rondas**. Con N rondas y C colores se pueden distinguir muchos más genes que colores hay disponibles (codificación combinatoria). Es la lógica de MERFISH ([[Vizgen]]) y del [[CosMx SMI]].

## Balance

| Ventajas | Desafíos |
|---|---|
| **Resolución extrema** — se ve el transcripto individual, con posición subcelular | Limitado a la **cantidad de sondas** diseñadas: es un panel dirigido, no descubrimiento |
| No requiere disociar ni capturar | **Visualización** y manejo de los datos de imagen |
| Sensibilidad alta por transcripto | [[Optical crowding]], [[Photobleaching]], [[Autofluorescencia]], [[Stage drift]] |

## La limitación de fondo

Sólo se detecta **lo que se buscó**. Si un gen no está en el panel, no existe para el experimento. Por eso estos métodos son la elección cuando ya se sabe qué se busca, y los [[Métodos basados en secuenciación]] lo son cuando hay que descubrirlo.

## Historia

Es la familia más antigua: la clase la traza desde ~1980, mucho antes que la secuenciación masiva.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
