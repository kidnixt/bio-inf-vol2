---
tags: [concepto, bioinformática, desafío]
area: Bioinformática
aliases: [integración de datos, multiómica, multi-omics integration]
---

# Integración de datos multiómicos

> **scATAC-seq + scRNA-seq + scRibo-seq + scProteomics**

El quinto desafío bioinformático de la clase. Cada ómica mide un nivel distinto del [[Dogma central de la biología molecular]], y ninguna alcanza por sí sola.

## Los dos escenarios

| Escenario | Descripción | Dificultad |
|---|---|---|
| **Multiómica pareada** | Varias modalidades medidas **en las mismas células** | Técnicamente difícil, computacionalmente más simple |
| **Integración no pareada** | Modalidades medidas en células distintas del mismo tejido | Técnicamente accesible, computacionalmente difícil |

En el segundo caso no hay correspondencia célula a célula: hay que **inferir** qué célula de un dataset corresponde a cuál del otro, alineando los espacios latentes de ambas modalidades.

## Por qué es difícil

- Las modalidades tienen **estadísticas incompatibles**: conteos de [[UMI]] en [[scRNA-seq]], señal casi binaria en [[scATAC-seq]], intensidades continuas en [[Proteómica de célula única]].
- Los **features no son los mismos**: genes vs picos de accesibilidad vs proteínas. Traducirlos requiere supuestos (por ejemplo, asignar un pico al gen más cercano).
- Distintos niveles de [[Sparsity]] y de [[Batch effect]].
- Escalas de datos muy distintas: 20.000 genes vs 100.000+ picos vs unos cientos de proteínas.

## La apuesta

> Aproximaciones de [[Machine Learning]], [[Deep Learning]] y [[Inteligencia Artificial]] pueden aportar soluciones.

Es la frase con la que la clase cierra la sección de desafíos, y la conexión explícita con el [[Módulo 3 - MOC|Módulo 3]].

## Caso espacial

[[Integración de datos single cell y spatial]] — el mismo problema, con la posición como modalidad adicional.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
