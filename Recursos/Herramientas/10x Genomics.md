---
tags: [herramienta, plataforma, empresa]
area: Herramientas
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

Cada perla lleva cientos de miles a millones de oligos con el **mismo** [[Barcode celular]] pero [[UMI|UMIs]] distintos, que es exactamente lo que se necesita para separar células y contar moléculas.

## 3' Assay vs 5' Assay

| | 3' Assay | 5' Assay |
|---|---|---|
| Extremo capturado | 3' del transcripto | 5' del transcripto |
| Uso típico | Cuantificación general de expresión | Igual, **más** perfilado de receptores inmunes (TCR/BCR) |
| Motivo | El oligo-dT captura la cola poli-A | Las regiones variables de TCR/BCR quedan del lado 5' |
| Oligo del bead | Read 1 + barcode + UMI + **poly(dT)VN** | Read 1 + barcode + UMI + **TSO** (*template switch oligo*) |
| Cómo se completa el ADNc | El TSO en solución agrega el extremo 5' por *template switching* | El poly(dT) está en solución; el TSO del bead hace el *template switching* |

El 3'-assay es el más usado. Frente a los protocolos de placa como [[Smart-seq]], 10x captura **muchas más células** (>10.000) pero solo un extremo del transcripto (1.000–4.000 genes/célula). En Uruguay, la plataforma está disponible en el [[Institut Pasteur de Montevideo]].

## En transcriptómica espacial

10x Genomics también es actor central en [[Transcriptómica espacial]] con [[Visium]] (2017 en la línea de tiempo de la clase), [[Visium HD]] y la plataforma de imagen [[Xenium]] (2022), junto a [[Nanostring]], [[Vizgen]] y [[BGI]].

## Herramientas asociadas

El software oficial de procesamiento (Cell Ranger / Space Ranger, ver [[Seurat y Scanpy]]) hace demultiplexado por barcode, alineamiento y construcción de la [[Matriz de conteo]]. Alternativas más livianas usan [[Pseudoalineamiento]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
