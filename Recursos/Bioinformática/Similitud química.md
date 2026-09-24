---
tags: [concepto, bioinformática, quimioinformática]
area: Bioinformática
aliases: [Tanimoto, coeficiente de Tanimoto, similitud molecular, fingerprint]
---

# Similitud química

La hipótesis fundacional del [[Diseño basado en ligandos|LBDD]]:

> **Moléculas parecidas tienden a compartir actividad.**

Y su contracara, que la clase enuncia en la misma diapositiva:

> **Riesgo:** un cambio pequeño puede producir un [[Activity cliff|*activity cliff*]].

## Cómo se mide

Se comparan **fingerprints**: vectores de bits donde cada posición indica la presencia de una subestructura (ver [[Representaciones moleculares]]). La métrica estándar es el **coeficiente de Tanimoto** (o Jaccard):

$$T_c = \frac{c}{a + b - c}$$

donde *a* y *b* son los bits encendidos en cada molécula y *c* los que comparten. Va de 0 a 1.

**El ejemplo de la clase:** dos moléculas que comparten un anillo fenólico y un grupo amino, pero A tiene además un ácido carboxílico.

```
A: 0 1 0 1 0 1     (a = 3)
B: 0 1 0 1 0 0     (b = 2)
     ^   ^         (c = 2)

Tc = 2 / (3 + 2 − 2) = 0,66
```

## Otras métricas

| Métrica | Rango |
|---|---|
| Tanimoto / Jaccard | 0 a 1 |
| Distancia euclídea | 0 a N |
| City-block / Manhattan / Hamming | 0 a N |
| Coeficiente de Dice | 0 a 1 |
| Similitud coseno | 0 a 1 |
| Russell–RAO, Forbes, distancia de Soergel | 0 a 1 |

La elección importa: métricas distintas ordenan distinto el mismo conjunto, y ninguna es "la correcta" fuera de un protocolo.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
