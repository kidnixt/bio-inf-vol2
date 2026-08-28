---
tags: [concepto, bioinformática, desafío]
area: Bioinformática
aliases: [efecto de lote, batch effects, ruido técnico]
---

# Batch effect

> **Ruido + batch effect: variabilidad técnica y biológica + diferentes experimentos/plataformas.**

Segundo de los cinco desafíos bioinformáticos de la clase. Un *batch effect* es una diferencia sistemática entre datos que se origina en **cómo se generaron**, no en la biología: distinto día de procesamiento, distinto operador, distinto lote de reactivos, distinta plataforma, distinto donante.

## Por qué es tan grave en single cell

Con miles de células por muestra, incluso un sesgo técnico pequeño se vuelve **estadísticamente arrollador**. El síntoma clásico: al hacer [[Reducción dimensional]] y [[Clustering]], las células se agrupan **por muestra** en lugar de por [[Tipo celular]]. El [[UMAP]] muestra islas separadas que corresponden a experimentos, no a biología.

## El dilema de la corrección

Corregir el batch effect es necesario, pero peligroso:

- Corregir **de menos** → los clusters reflejan lotes, no tipos celulares.
- Corregir **de más** → se borran diferencias biológicas reales, sobre todo si el diseño experimental está confundido (por ejemplo, si todos los controles se procesaron un día y todos los tratados otro).

La regla práctica es de diseño, no de software: **nunca alinear el batch con la variable de interés**. Si eso ya ocurrió, ningún método puede separarlos.

## Relación con la integración

Los métodos de corrección de batch son los mismos que se usan para [[Integración de datos multiómicos]] y para combinar atlas de laboratorios distintos ([[Atlas celulares]]).

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
