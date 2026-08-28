---
tags: [herramienta, plataforma, empresa]
area: Plataformas
---

# 10x Genomics

Empresa cuya plataforma de [[Microfluídica|microgotas]] convirtió al [[scRNA-seq]] en una técnica de rutina. Es el ejemplo de workflow que usa la clase.

## Workflow (single cell)

```
suspensión celular  +  perlas (gel beads) con barcode  +  aceite
        ↓ chip microfluídico
GEMs (gotas): 1 célula + 1 perla
        ↓ lisis + retrotranscripción dentro de la gota
ADNc marcado con barcode celular + UMI
        ↓ romper emulsión, amplificar por PCR, secuenciar
```

Cada perla lleva millones de oligos con el **mismo** [[Barcode celular]] pero [[UMI|UMIs]] distintos, que es exactamente lo que se necesita para separar células y contar moléculas.

## 3' Assay vs 5' Assay

| | 3' Assay | 5' Assay |
|---|---|---|
| Extremo capturado | 3' del transcripto | 5' del transcripto |
| Uso típico | Cuantificación general de expresión | Igual, **más** perfilado de receptores inmunes (TCR/BCR) |
| Motivo | El oligo-dT captura la cola poli-A | Las regiones variables de TCR/BCR quedan del lado 5' |

## En transcriptómica espacial

10x Genomics también es actor central en [[Transcriptómica espacial]] con [[Visium]] (2019 en adelante) y [[Visium HD]], que aparecen en la línea de tiempo de la clase junto a [[Nanostring]], [[Vizgen]] y [[BGI]].

## Herramientas asociadas

El software oficial de procesamiento (Cell Ranger / Space Ranger) hace demultiplexado por barcode, alineamiento y construcción de la [[Matriz de conteo]]. Alternativas más livianas usan [[Pseudoalineamiento]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
