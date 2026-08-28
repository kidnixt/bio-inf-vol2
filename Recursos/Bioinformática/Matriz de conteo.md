---
tags: [concepto, bioinformática]
area: Bioinformática
aliases: [count matrix, matriz de expresión, matriz genes x células]
---

# Matriz de conteo

La estructura de datos central de toda la transcriptómica: una tabla de **genes × observaciones** donde cada celda es la abundancia estimada de un gen en una observación.

## El cambio de escala

| Tecnología | Filas × Columnas | Orden de magnitud |
|---|---|---|
| [[Bulk RNA-seq]] | genes × condiciones | ~10.000 × [6–10] |
| [[scRNA-seq]] | genes × **células** | ~20.000 × [10³–10⁶] |

```
Bulk                                scRNA-seq
        S1     S2     S3                    Cell 1  Cell 2  Cell 3
Gene A  1000   1200   950           Gene A    12      8      15
Gene B    20     50    15           Gene B     0      5       0
Gene C     0      2     1           Gene C     0      2       1
```

Pasar de decenas de columnas a millones cambia **todo**: los métodos estadísticos, las estructuras de datos (matrices dispersas en lugar de densas), la memoria necesaria y hasta qué preguntas tiene sentido hacer.

## Cómo se construye

Demultiplexado por [[Barcode celular]] → [[Alineamiento de secuencias|alineamiento]] o [[Pseudoalineamiento]] → conteo de [[UMI|UMIs]] únicos por gen y por célula.

## Sus propiedades incómodas

- **[[Sparsity]]**: la mayoría de las celdas son cero.
- **[[Alta dimensionalidad]]**: 20.000 dimensiones por célula.
- **Conteos, no medidas continuas**: requiere modelos de distribución de conteos (Poisson, binomial negativa), no gaussianos.
- **[[Batch effect]]**: matrices de experimentos distintos no son directamente comparables.

## En espacial

En [[Transcriptómica espacial]] la matriz gana una tabla asociada de **coordenadas** por observación (spot, bin o célula segmentada), y a menudo una imagen histológica alineada. Eso es parte del problema de [[Almacenamiento y visualización]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
