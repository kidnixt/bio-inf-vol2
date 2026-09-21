---
tags: [concepto, técnica, ingeniería-metabólica]
area: Técnicas
aliases: [ALE, adaptive laboratory evolution, evolución de laboratorio, evolutionary engineering, laboratory evolution]
---

# Evolución adaptativa de laboratorio

Estrategia experimental que consiste en **cultivar un organismo durante muchas generaciones bajo una presión selectiva** (por ejemplo, un medio donde el único azúcar es xilosa) y dejar que la selección natural haga el trabajo: las mutaciones que mejoran el desempeño se enriquecen solas.

## En la clase

Es una de las tres estrategias clásicas para que *[[Saccharomyces cerevisiae|S. cerevisiae]]* use [[Pentosas|pentosas]], junto con introducir [[Vías de asimilación de pentosas|vías heterólogas]] y la ingeniería de transportadores. Los trabajos citados:

- Garcia Sanchez et al. (2010) — *Improved xylose and arabinose utilization by an industrial recombinant S. cerevisiae strain using **evolutionary engineering***.
- Papapetridis et al. (2018) — ***Laboratory evolution** for forced glucose-xylose co-consumption enables identification of mutations that improve mixed-sugar fermentation by xylose-fermenting S. cerevisiae*.

El segundo es especialmente relevante: usa una cepa diseñada racionalmente (*pgi1Δ rpe1Δ*, que no puede crecer solo en glucosa) y después deja que la evolución encuentre las mutaciones que mejoran la fermentación de la mezcla.

## La relación con el diseño computacional

Son complementarios, no rivales:

| ALE | [[Diseño computacional de cepas]] |
|---|---|
| No requiere saber qué mutar | Requiere un modelo, pero propone blancos concretos |
| Encuentra soluciones que nadie hubiera propuesto | Encuentra soluciones que el modelo demuestra necesarias |
| Puede tardar meses y quedar en un óptimo local | Corre en 30 minutos, pero hay que validar experimentalmente |

Y comparten el mismo límite conceptual que señala la clase: **habilitar no es forzar**. Si la cepa evolucionada todavía puede crecer con un solo azúcar, va a tender a hacerlo.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
