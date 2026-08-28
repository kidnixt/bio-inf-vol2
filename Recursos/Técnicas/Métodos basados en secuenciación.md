---
tags: [técnica, espacial]
area: Técnicas
aliases: [sequencing-based, captura sobre oligos, NGS-based spatial]
---

# Métodos basados en secuenciación masiva

La segunda gran familia de la [[Transcriptómica espacial]]. En lugar de mirar el tejido, se **captura** el ARN sobre una superficie cuyas coordenadas están codificadas con [[Barcode espacial|barcodes espaciales]], y luego se secuencia todo junto.

## Principio

```
Corte de tejido sobre slide con barcodes posicionales
        ↓ permeabilización
ARN difunde y se captura sobre los oligos
        ↓ RT + secuenciación
Cada lectura lleva: transcripto + barcode = qué gen y dónde
```

La reconstrucción espacial es **computacional**: la posición se recupera decodificando el barcode, no mirando la imagen.

## Balance

| Ventajas | Desafíos |
|---|---|
| **Descubrimiento molecular**: se captura el [[Transcriptoma]] completo, sin panel predefinido | **Resolución** más gruesa: cada spot puede contener varias células |
| Compatible con el pipeline estándar de RNA-seq | [[Lateral diffusion]]: el ARN se corre antes de ser capturado |
| Alto throughput | Requiere deconvolución para asignar tipos celulares a spots |

## Historia y ejemplos

La clase sitúa el arranque de esta familia hacia 2008–2009. Ejemplos: [[Visium]] ([[10x Genomics]]), Stereo-seq ([[BGI]]) y, con la mejora de resolución vía sondas, [[Visium HD]].

## Contraparte

[[Métodos basados en sondas]] — el compromiso es exactamente el opuesto.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
