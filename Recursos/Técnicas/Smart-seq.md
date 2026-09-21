---
tags: [técnica, single-cell, transcriptomica]
area: Técnicas
aliases: [Smart-seq2, SMART-seq, SMART-seq2, Smart-Seq]
---

# Smart-seq

Familia de protocolos de [[scRNA-seq]] **basados en placas**: cada célula se deposita (normalmente por [[Citometría de flujo|FACS]]) en un pocillo y se procesa por separado, obteniendo el **transcripto completo** (*full-length*) en lugar de solo un extremo.

## 10x Genomics vs Smart-seq

La comparación que se discutió en la clase (resumen del curso):

| | [[10x Genomics]] (gotas) | **Smart-seq** (placas) |
|---|---|---|
| Nº de células | **> 10.000** | **< 1.000** |
| Cobertura del transcripto | Solo el extremo 3' (o 5') | **Completa** |
| Genes detectados por célula | 1.000–4.000 | **> 5.000** |
| Requisitos | Equipo y chip de microfluídica | Solo *cell sorting* |

La lógica general: los métodos de gotas ganan **células** a costa de **profundidad**, lo que suele identificar mejor la heterogeneidad de un tejido; Smart-seq gana profundidad y detecta genes poco expresados, isoformas y variantes ([[Shafer 2019 - Cross-species analysis of scRNAseq data|Shafer 2019]]). En la tabla de [[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija (2019)]], Smart-seq2 figura con un throughput de **100–300 células** por experimento.

En la línea de tiempo de la clase, SMART-seq aparece en 2012 y SMART-seq2 en 2013–2014.

## En Uruguay

Según la clase, hay capacidad instalada para Smart-seq (solo requiere *cell sorting*, disponible por ejemplo en el [[IIBCE]]) y para 10x Genomics (en el [[Institut Pasteur de Montevideo]]).

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Shafer 2019 - Cross-species analysis of scRNAseq data]] *(lectura)*
