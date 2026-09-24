---
tags: [concepto, bioinformática, quimioinformática, modelado]
area: Bioinformática
aliases: [QSAR 2D, QSAR-2D, 3D-QSAR, QSAR-3D, relación estructura-actividad, SAR]
---

# QSAR

**Relación cuantitativa entre estructura y actividad** (*Quantitative Structure–Activity Relationship*): un modelo supervisado que predice la actividad de una molécula a partir de descriptores numéricos de su estructura.

```
estructura química → descriptores (X) → modelo ŷ = f(X) → actividad predicha
```

## El ejemplo de la clase

Cinco moléculas con actividad experimental (7,2; 6,5; 5,9; 7,8; 6,1), descritas por **MW, LogP, HBD, HBA y TPSA**. Se parte en entrenamiento (70 %) y prueba (30 %), se ajusta el modelo, se evalúa con **R², Q² y RMSE** (gráfico predicho vs. observado) y se aplica a una molécula nueva: **pIC₅₀ = 6,8**.

## Variantes

| Variante | Qué usa |
|---|---|
| **QSAR-2D** | Descriptores calculados de la estructura plana: propiedades fisicoquímicas, conteos, fingerprints |
| **QSAR-3D** | Campos moleculares en el espacio (estérico, electrostático), que requieren alinear las moléculas en 3D. Suele ajustarse con **PLS** |

## El descriptor no tiene que ser un fingerprint

En el trabajo de [[Andrés Ballesteros]] sobre *p*-quinonas, los descriptores salen de **cálculos de química cuántica** (DFT): ΔG de formación de semiquinona e hidroquinona, energías HOMO, LUMO y SUMO. Es decir, el QSAR puede apoyarse en la **física del mecanismo** —en ese caso el ciclo redox de la quinona— y no solo en la topología de la molécula.

## Con deep learning

El contraste que plantea la clase: el **QSAR tradicional** usa descriptores **definidos previamente** y produce un modelo interpretable por una persona; el [[Deep Learning|deep learning]] aprende **representaciones** desde SMILES, grafos, confórmeros o ensambles, y produce un **espacio de [[Embedding|embeddings]]**. Es la misma jugada que los [[Modelo de lenguaje de proteínas|PLMs]] hacen del lado de las proteínas.

Su límite compartido con todo el [[Diseño basado en ligandos|LBDD]]: los [[Activity cliff|activity cliffs]], y la extrapolación fuera del dominio de entrenamiento.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
