---
tags: [concepto, biología]
area: Biología molecular
aliases: [ARNm, mRNA]
---

# ARN mensajero

El **ARN mensajero (ARNm)** es la copia transitoria de un gen que se produce durante la transcripción y que sirve de molde para la [[Traducción]]. Es la molécula que realmente se mide en [[Bulk RNA-seq]] y [[scRNA-seq]].

## Características que condicionan la medición

- **Cola poli-A**: la mayoría de los protocolos de RNA-seq capturan ARNm mediante oligo-dT, que se aparea con la cola poli-A. Por eso los métodos estándar capturan preferentemente ARNm y no ARN ribosomal ni otros ARN no poliadenilados.
- **Vida media corta**: el ARNm es transitorio, lo que lo hace un buen reporte del estado *actual* de la célula ([[Estado celular]]) más que de su identidad permanente.
- **Muy poca cantidad por célula**: del orden de picogramos, lo que obliga a amplificar por PCR en [[scRNA-seq]] — y es la razón por la que se necesita el [[UMI]].

El conjunto de todos los ARN de una célula en un momento dado es su [[Transcriptoma]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
