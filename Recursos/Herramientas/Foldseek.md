---
tags: [herramienta, software, estructura, búsqueda]
area: Herramientas
aliases: [foldseek, búsqueda estructural rápida]
---

# Foldseek

Buscador de **estructuras** de proteínas que funciona comparando **texto** en vez de geometría (van Kempen et al., 2024, *Nature Biotechnology* 42:243–246). `search.foldseek.com`

## El problema que resuelve

Con [[AlphaFold DB]] (214 M de modelos) y el [[ESM Atlas]] (617 M), hay **cientos de millones de estructuras predichas**. Compararlas con alineadores estructurales clásicos (TM-align, Dali, CE) era el **cuello de botella**.

> **La idea:** si puedo **escribir la forma con letras**, puedo comparar estructuras con **algoritmos de secuencia**, optimizados por décadas.

Ese alfabeto es el [[Alfabeto 3Di|3Di]]: 10 rasgos geométricos por residuo, agrupados en **20 estados**, un símbolo por residuo → una "secuencia de forma".

## El resultado

| Comparación | Aceleración |
|---|---|
| vs. TM-align y Dali | **> 4.000×** |
| vs. CE | **> 21.000×** |
| En bases grandes | hasta **180.000×** |

Y **sin perder sensibilidad**: 86 % de Dali, 88 % de TM-align y **133 % de CE**.

> **Por qué es tan rápido:** no compara geometría, **compara texto**. Convierte un problema carísimo en uno que ya sabíamos resolver rápido.

## Su descendencia

- [[ProstT5]] **aprende** el alfabeto que Foldseek inventó, y predice el 3Di directo de la secuencia — sin calcular la estructura.
- [[Phold]] combina las dos piezas (ProstT5 para generar el 3Di, Foldseek para buscarlo) y anota genomas de fagos mejor que cualquier método de secuencia.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Bouras et al 2026 - Phold]] *(lectura)*
- [[Heinzinger et al 2024 - ProstT5]] *(lectura)*
- [[van Kempen et al 2024 - Foldseek]] *(lectura)*
