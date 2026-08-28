---
tags: [herramienta, plataforma, espacial]
area: Plataformas
---

# Visium HD

Generación de alta definición de [[Visium]] ([[10x Genomics]]). La clase la contrasta explícitamente con la versión clásica:

> **Visium (secuenciación) vs Visium HD (sondas)**

## Qué cambia

| | [[Visium]] | Visium HD |
|---|---|---|
| Superficie de captura | Spots discretos separados | **Grilla continua** de cuadrados de 2 µm |
| Química | Captura por poli-A + secuenciación | **Sondas** contra el transcriptoma |
| Resolución | Varias células por spot | Cerca de **célula única** |
| Cobertura | Transcriptoma completo | Transcriptoma completo (vía panel de sondas de genoma entero) |

## Su lugar en el trade-off

| # Genes | Resolución espacial | Throughput |
|---|---|---|
| **Completo** | Alta, cerca de célula única | **Alto** |

Es la combinación más equilibrada de las tres plataformas que compara la clase, y por eso lleva asterisco en la tabla: se acerca a tener todo a la vez, aunque con salvedades.

## Sus desafíos

- **[[Lateral diffusion]]**: al capturarse el ARN sobre oligos en superficie, la molécula difunde lateralmente antes de anclarse. La señal se "corre" respecto de su origen real y difumina los bordes entre estructuras. Es el problema característico de esta arquitectura.
- **[[Segmentación celular]]**: la grilla de 2 µm no respeta fronteras celulares; hay que agrupar bins en células, normalmente apoyándose en la imagen histológica.
- **[[Almacenamiento y visualización]]**: la resolución fina multiplica el volumen de datos.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
