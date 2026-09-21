---
tags: [concepto, bioinformática, single-cell, trayectorias]
area: Bioinformática
aliases: [velocidad de ARN, RNA velocities, Velocyto]
---

# RNA velocity

Estimación de la **dirección y velocidad de cambio** del transcriptoma de cada célula a partir de un dato que el [[scRNA-seq]] captura "gratis": la proporción de transcriptos **sin empalmar** (con intrones) frente a los **empalmados**.

## La idea

Un transcripto recién sintetizado todavía tiene intrones; al procesarse, los pierde. Entonces:

| Situación del gen | Relación sin empalmar / empalmado |
|---|---|
| **Encendiéndose** (inducción) | Exceso de ARN sin empalmar |
| **Apagándose** (represión) | Déficit de ARN sin empalmar |
| Estado estacionario | Proporción constante |

Con eso se estima el **estado futuro** de cada célula y se dibujan flechas sobre el [[UMAP]]. Fue propuesto por La Manno et al. (herramienta **Velocyto**, que aparece en la figura de la clase dentro de los métodos de *trayectoria*).

## Para qué sirve

- Agregar **direccionalidad** a un [[Pseudotiempo]] inferido: resuelve problemas clásicos como dónde empieza la trayectoria (*rooting*), las ramificaciones y los ciclos ([[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija 2019]]).
- En el esquema del pipeline de la clase aparece como análisis *downstream*, junto a pseudotiempo y marcadores de poblaciones.

Incluso con química de extremo 3' se captura suficiente información de intrones como para estimarla.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] *(lectura)*
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
