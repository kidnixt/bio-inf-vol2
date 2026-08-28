---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [anotación celular, cell type annotation]
---

# Anotación de tipos celulares

El paso que convierte un cluster —una entidad estadística— en un [[Tipo celular]] con nombre biológico. La clase presenta dos familias de estrategias.

## Estrategias manuales

1. **[[Expresión diferencial]] entre clusters** → obtener los genes marcadores de cada grupo.
2. **Análisis en base a literatura** → contrastar esos marcadores con lo que se sabe del tejido (RBFOX3 → [[Neurona]]; TREM2 → [[Microglía]]).
3. **Anotación** → asignar el nombre.

Ventaja: control e interpretabilidad. Desventaja: lento, subjetivo, y limitado a lo que ya está descrito en la literatura.

## Estrategias automatizadas

- **Basadas en correlación con un set de datos previo**: se compara el perfil de cada célula (o cluster) con una referencia anotada y se transfiere la etiqueta más similar.
- **Basadas en [[Machine Learning]] con múltiples sets de datos previos**: se entrena un clasificador sobre muchos atlas anotados y se lo aplica a los datos nuevos.

Ventaja: rápido, reproducible, escalable. Desventaja: sólo puede reconocer lo que está en la referencia — **un tipo celular nuevo se anota como el más parecido conocido**, y así desaparece.

## El problema de fondo

Ambas familias dependen de que exista un consenso sobre qué tipos hay y cómo se llaman. Ese consenso es precisamente lo que los [[Atlas celulares]] intentan construir, y lo que el desafío de la [[Identidad celular]] señala como no resuelto.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
