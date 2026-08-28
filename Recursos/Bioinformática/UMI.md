---
tags: [concepto, bioinformática, single-cell]
area: Bioinformática
aliases: [UMIs, unique molecular identifier, identificador molecular único]
---

# UMI (Unique Molecular Identifier)

Una **secuencia aleatoria corta** (típicamente 10–12 nucleótidos) que se añade a cada molécula de ADNc **antes** de la amplificación por PCR. Su función es identificar **moléculas individuales**.

## El problema que resuelve

Una célula contiene muy poco ARN, así que el [[scRNA-seq]] obliga a amplificar por PCR. Pero la PCR no amplifica todo por igual: fragmentos cortos, con GC favorable o simplemente afortunados en los primeros ciclos terminan sobrerrepresentados. Sin corrección, el conteo de lecturas mide **eficiencia de amplificación**, no abundancia original.

## Cómo lo resuelve

Cada molécula original recibe un UMI distinto antes de amplificar. Todas las copias de PCR de esa molécula heredan el **mismo** UMI.

```
3 moléculas originales del gen A  →  UMI: AACGT, TTGCA, GGATC
        ↓ PCR (10.000 copias)
10.000 lecturas, pero sólo 3 UMIs distintos
        ↓ contar UMIs únicos, no lecturas
conteo del gen A = 3   ✔
```

**Contar UMIs únicos ≈ contar moléculas originales.** Eso es lo que vuelve cuantitativo al método.

## No confundir con el barcode celular

Son dos etiquetas distintas que responden preguntas distintas:

| Etiqueta | Pregunta que responde | Compartida por |
|---|---|---|
| [[Barcode celular]] | ¿**De qué célula** viene esta lectura? | Todas las moléculas de la misma célula |
| **UMI** | ¿Es una **molécula nueva** o una copia de PCR? | Todas las copias de la misma molécula |

## En el resto del pipeline

- El **número de UMIs por célula** es una de las tres métricas centrales del [[Control de calidad en scRNA-seq]].
- Los conteos de la [[Matriz de conteo]] de una plataforma como [[10x Genomics]] son conteos de UMI, no de lecturas.
- No aplica a [[Proteómica de célula única]]: como no hay amplificación, no hay sesgo de PCR que corregir — y tampoco hay forma de compensar la escasez de material.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
