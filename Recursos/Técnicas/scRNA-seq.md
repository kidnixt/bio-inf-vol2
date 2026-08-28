---
tags: [técnica, transcriptómica, single-cell]
area: Técnicas
aliases: [single cell RNA-seq, RNA-seq de célula única, scRNAseq]
---

# scRNA-seq (single cell RNA-seq)

Secuenciación del [[Transcriptoma]] de **células individuales**. La clase la llama "la revolución", y el cambio conceptual se resume en una oposición:

> **Promedios → Distribuciones**

En lugar de un valor por gen por muestra ([[Bulk RNA-seq]]), se obtiene una distribución de valores por gen a lo largo de miles o millones de células.

## Los tres desafíos de la técnica

### 1. Matchear secuencias con células únicas

*¿Cómo saber de qué célula proviene cada molécula de ARN secuenciada?*

| Frente | Solución |
|---|---|
| Protocolos / tecnología | [[Aislamiento de células individuales]] |
| Biología molecular | [[Barcode celular]] + [[UMI]] |

El objetivo: **realizar reacciones de biología molecular en células individuales**. Ejemplo de workflow: [[10x Genomics]] (3' Assay y 5' Assay).

### 2. La cantidad de ARN

Una célula contiene del orden de picogramos de ARN. Hay que **amplificar el ADNc por PCR**, lo que introduce sesgo de amplificación — precisamente lo que corrige el [[UMI]].

### 3. El alineamiento

Explosión de datos respecto del bulk:

| | [[Bulk RNA-seq]] | scRNA-seq |
|---|---|---|
| Diseño | 3 vs 3 (6 muestras) | 10k células |
| Lecturas | 20–30 M por muestra | 20k–50k por célula → **200–500 M** |
| Metadata técnica | — | [[Barcode celular\|barcodes]] + [[UMI\|UMIs]] |

Las [[Alineamiento de secuencias|herramientas clásicas]] sufren con sitios exón–exón, RAM y [[Multimapping|multimappings]]. La solución es el [[Pseudoalineamiento]].

## Qué se obtiene

1. **Secuencias (raw data)**
2. **[[Matriz de conteo]]**: ~20.000 genes × [10³–10⁶] células

```
          Cell 1   Cell 2   Cell 3
Gene A      12        8       15
Gene B       0        5        0
Gene C       0        2        1
```

Los ceros abundantes son [[Sparsity]].

## Pipeline de análisis

[[Control de calidad en scRNA-seq]] → [[Reducción dimensional]] → [[Clustering]] → [[Anotación de tipos celulares]] → downstream ([[Expresión diferencial]], [[Pseudobulk]], [[Pseudotiempo]]).

## Su límite

Requiere **disociar el tejido**, y eso destruye la posición, la arquitectura y los vecinos. Esa pérdida es el punto de partida de la [[Transcriptómica espacial]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
