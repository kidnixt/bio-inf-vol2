---
tags: [técnica, transcriptómica]
area: Técnicas
aliases: [transcriptómica bulk, RNA-seq bulk]
---

# Bulk RNA-seq

Secuenciación del ARN de **una muestra completa**: se homogeneiza el tejido, se extrae todo el ARN junto y se secuencia. Fue el estándar de la transcriptómica durante más de una década y sigue siendo la opción correcta para muchas preguntas.

## Qué se obtiene

Una [[Matriz de conteo]] de dimensiones modestas — **~10.000 genes × [6–10] condiciones**:

```
          Sample 1   Sample 2   Sample 3
Gene A      1000       1200        950
Gene B        20         50         15
Gene C         0          2          1
```

Sobre ella se hacen los análisis clásicos: clustering de muestras (PCA), [[Expresión diferencial|DEGs]], enriquecimiento por [[Gene Ontology]] y detección de genes co-regulados.

## La advertencia conceptual

> **No estamos midiendo expresión directamente. Estamos cuantificando la abundancia de las moléculas de ARN muestreadas.**

Todo pasa por: sampleo, [[Profundidad de secuenciación]], ruido y distribución de conteos.

## La limitación

Un tejido es heterogéneo (ver [[Heterogeneidad celular]]), así que el bulk devuelve **promedios ponderados** por la abundancia de cada población. Se pierden:

- [[Tipo celular|Tipos celulares]]
- [[Estado celular|Estadíos celulares]]
- Subpoblaciones
- **Células raras**

Un cambio real confinado a una subpoblación del 2% es invisible en el promedio.

## Cuándo sigue siendo la mejor opción

Cuando la pregunta es sobre la muestra como un todo, cuando el tejido es razonablemente homogéneo, cuando se necesitan muchas réplicas biológicas, o cuando el presupuesto manda: el bulk es órdenes de magnitud más barato que el [[scRNA-seq]]. De hecho, la estrategia de [[Pseudobulk]] consiste en volver deliberadamente al marco estadístico del bulk partiendo de datos single cell.

## Se contrapone a

- [[scRNA-seq]] (promedios → distribuciones)
- [[Transcriptómica espacial]] (→ contexto)

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
