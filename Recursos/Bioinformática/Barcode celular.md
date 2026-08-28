---
tags: [concepto, bioinformática, single-cell]
area: Bioinformática
aliases: [barcodes, barcode, código de barras celular, cell barcode]
---

# Barcode celular

Secuencia de ADN conocida que identifica **la célula** de la que proviene una lectura. Es la solución al primer desafío del [[scRNA-seq]]:

> ¿Cómo hacemos para saber de qué célula proviene cada molécula de ARN secuenciada?

## Cómo se asigna

En plataformas de [[Microfluídica]] como [[10x Genomics]], cada perla que entra en una gota lleva millones de oligos que comparten **el mismo barcode celular**, pero con [[UMI|UMIs]] distintos. Todo el ADNc generado dentro de esa gota — es decir, todo el ARN de esa célula — queda marcado con ese barcode. Después se puede romper la emulsión y secuenciar todo junto: la asignación célula-lectura ya está escrita en la secuencia.

## Estructura de una lectura

| Elemento | Función |
|---|---|
| Adaptador | Anclaje para secuenciar |
| **Barcode celular** | Identifica **la célula** |
| [[UMI]] | Identifica **moléculas individuales** |
| ADNc | Identifica el **transcripto / secuencia** |

## En el análisis

El demultiplexado por barcode es el primer paso del procesamiento, y es lo que convierte un archivo de cientos de millones de lecturas en las columnas de la [[Matriz de conteo]]. Los barcodes también son parte de la "metadata técnica" que hace explotar el volumen de datos respecto del [[Bulk RNA-seq]].

Un problema práctico: distinguir barcodes de células reales de barcodes de **gotas vacías** que capturaron ARN ambiental. Ése es uno de los objetivos del [[Control de calidad en scRNA-seq]].

## Análogo espacial

[[Barcode espacial]] — misma idea, pero la etiqueta codifica una posición en vez de una célula.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
