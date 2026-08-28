---
tags: [técnica, espacial, transcriptómica]
area: Técnicas
aliases: [Spatial transcriptomics, biología espacial, transcriptómica spatial, ómicas espaciales]
---

# Transcriptómica espacial

Medición de la [[Expresión génica]] **conservando la posición de cada medición dentro del tejido**. Es el tercer escalón de una progresión:

| Aproximación | Qué obtenemos |
|---|---|
| [[Bulk RNA-seq]] | **Promedios** |
| [[scRNA-seq]] | **Distribuciones** |
| Transcriptómica espacial | **Contexto** |

## El problema que resuelve

El flujo `Tejido → disociación → células → scRNA-seq → UMAP` **conserva** resolución celular, heterogeneidad, estados y perfiles individuales. Pero el paso de disociación destruye:

- **Posición**
- **Arquitectura**
- **Vecinos**
- **Estructura tisular**
- **Relaciones espaciales**

El [[UMAP]] es un espacio de similitud transcriptómica, **no un mapa del tejido**.

## Las dos familias de métodos

| | [[Métodos basados en sondas]] | [[Métodos basados en secuenciación]] |
|---|---|---|
| Principio | Hibridación e imagen *in situ* | Captura sobre [[Barcode espacial\|barcodes espaciales]] + secuenciación |
| Ventaja | **Resolución extrema** (subcelular) | **Descubrimiento molecular** (sin panel) |
| Desafío | Cantidad de sondas; visualización | Resolución más gruesa |

## El trade-off

> **Número de genes × Número de células × Resolución espacial × Throughput**

Ninguna plataforma optimiza las cuatro. Ver [[GeoMx DSP]], [[CosMx SMI]], [[Visium]] y [[Visium HD]].

## Desafíos bioinformáticos

[[Segmentación celular]], [[Lateral diffusion]], [[Optical crowding]], [[Photobleaching]], [[Autofluorescencia]], [[Stage drift]], [[Integración de datos single cell y spatial]] y [[Almacenamiento y visualización]].

## Qué se aprende con ella

[[Spatial domains]], [[Neighborhoods]], [[Spatial niches]] y [[Atlas celulares]] espaciales.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
