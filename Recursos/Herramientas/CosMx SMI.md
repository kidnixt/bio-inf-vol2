---
tags: [herramienta, plataforma, espacial]
area: Plataformas
aliases: [CosMx, Spatial Molecular Imager]
---

# CosMx SMI (Spatial Molecular Imager)

Plataforma de [[Transcriptómica espacial]] de [[Nanostring]] basada en imagen, dentro de la familia de [[Métodos basados en sondas]]. Alcanza resolución de **célula única y subcelular**: localiza transcriptos individuales y permite decir si un ARN está en el núcleo o en el citoplasma.

## Cómo funciona

Rondas sucesivas de hibridación de sondas fluorescentes sobre el tejido intacto, con codificación combinatoria: cada gen tiene una firma única de colores a lo largo de las rondas. La imagen se toma en cada ciclo y la decodificación reconstruye la identidad de cada punto de señal.

## Su lugar en el trade-off

| # Genes | Resolución espacial | Throughput |
|---|---|---|
| Alto a completo | **Célula única y subcelular** | **Moderado – bajo** |

Se paga la resolución con throughput: el área de tejido que se puede procesar por corrida es mucho menor que en [[GeoMx DSP]] o [[Visium HD]].

## Desafíos propios

Al ser un método de imagen, hereda todos los problemas ópticos: [[Optical crowding]], [[Photobleaching]], [[Autofluorescencia]] y [[Stage drift]]. Y como devuelve transcriptos con coordenadas pero sin fronteras celulares, requiere [[Segmentación celular]] — el paso más crítico del pipeline.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
