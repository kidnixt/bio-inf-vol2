---
tags: [concepto, bioinformática]
area: Bioinformática
aliases: [sequencing depth, cobertura, profundidad]
---

# Profundidad de secuenciación

Cuántas lecturas se dedican a una muestra o a una célula. Es una de las cuatro cosas que la clase señala como mediadoras entre "expresión" y lo que efectivamente medimos, junto con el sampleo, el ruido y la distribución de conteos.

## El presupuesto de lecturas

Secuenciar tiene un costo fijo por lectura, así que siempre hay que repartir un presupuesto:

| | [[Bulk RNA-seq]] | [[scRNA-seq]] |
|---|---|---|
| Unidad | Por muestra | Por célula |
| Típico | 20–30 M lecturas | 20k–50k lecturas |
| Total del experimento | ~150 M (6 muestras) | **200–500 M** (10k células) |

## El compromiso central

> **Más células × menos profundidad**, o **menos células × más profundidad**.

- Muchas células con poca profundidad → buena descripción de la **composición** del tejido, pero mucha [[Sparsity]] y mala detección de genes de bajo [[Rango dinámico]].
- Pocas células con mucha profundidad → mejor detección por célula (útil para isoformas o genes raros), pero peor cobertura de poblaciones minoritarias.

La elección depende de la pregunta: buscar un [[Tipo celular]] raro pide muchas células; caracterizar en detalle un tipo conocido pide profundidad.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
