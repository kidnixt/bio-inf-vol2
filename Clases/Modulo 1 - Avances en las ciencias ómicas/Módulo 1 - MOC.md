---
tags: [MOC, modulo-1]
---

# Módulo 1 — Avances en las ciencias ómicas

Índice del módulo. Curso **Fronteras y Perspectivas en Bioinformática** — Universidad ORT, 2026.

## Clases

| # | Clase | Docente |
|---|---|---|
| 1 | [[Aproximaciones ómicas con resolución de célula única]] | [[Guillermo Eastman]] |
| 2 | [[Biología espacial - mapeando la expresión génica a su entorno]] | [[Guillermo Eastman]] |
| 3 | [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]] | [[Cecilia Salazar]] |

## El hilo conductor del módulo

Las dos primeras clases recorren una sola progresión, en tres escalones:

| Aproximación | Qué obtenemos | Qué se pierde |
|---|---|---|
| [[Bulk RNA-seq]] | **Promedios** | Todo lo que hay debajo del promedio |
| [[scRNA-seq]] | **Distribuciones** | La posición en el tejido |
| [[Transcriptómica espacial]] | **Contexto** | Profundidad o cobertura, según la plataforma |

La tercera clase baja un nivel y mira **la tecnología que produce los datos**: cómo se generan las secuencias, qué cambia cuando las lecturas son largas y la molécula se lee nativa, y qué pasa cuando eso se aplica a microbiología clínica.

| Aproximación | Qué obtenemos | Qué se pierde |
|---|---|---|
| [[Secuenciación de segunda generación\|Lectura corta]] | **Exactitud por base** | Repeticiones, [[Plásmido\|plásmidos]], [[Variantes estructurales\|estructura]] |
| [[Secuenciación con nanoporos\|Nanoporos]] | **Longitud, molécula nativa, [[Metilación del ADN\|epigenética]] y [[Secuenciación en tiempo real\|tiempo real]]** | Exactitud por lectura individual |

Y un diagnóstico común de cierre en las tres clases: el cuello de botella ya no es generar datos, sino **almacenarlos, visualizarlos, integrarlos e interpretarlos responsablemente** para convertirlos en conocimiento.

## Mapa de conceptos del módulo

### Biología de base

[[Expresión génica]] · [[Dogma central de la biología molecular]] · [[Transcriptoma]] · [[ARN mensajero]] · [[Traducción]] · [[Cromatina]] · [[Rango dinámico]] · [[Heterogeneidad celular]] · [[Metilación del ADN]] · [[Plásmido]] · [[Resistencia antimicrobiana]]

### Células

[[Tipo celular]] · [[Estado celular]] · [[Identidad celular]] · [[Tejido cerebral]] · [[Neurona]] · [[Macroglía]] · [[Astrocito]] · [[Oligodendrocito]] · [[Microglía]] · [[Célula endotelial]]

### Técnicas — célula única y espacial

[[Bulk RNA-seq]] · [[scRNA-seq]] · [[scATAC-seq]] · [[scRibo-seq]] · [[Proteómica de célula única]] · [[Transcriptómica espacial]] · [[Aislamiento de células individuales]] · [[Dilución al límite]] · [[Micromanipulación]] · [[Microdisección por captura láser]] · [[Citometría de flujo]] · [[Microfluídica]] · [[Métodos basados en sondas]] · [[Métodos basados en secuenciación]]

### Técnicas — secuenciación

[[Secuenciación Sanger]] · [[Secuenciación de segunda generación]] · [[Secuenciación de tercera generación]] · [[Secuenciación con nanoporos]] · [[Preparación de bibliotecas de secuenciación]] · [[Secuenciación dúplex]] · [[Sequencing by Expansion]] · [[Secuenciación de proteínas con nanoporos]]

### Técnicas — microbiología clínica

[[Secuenciación 16S]] · [[Metagenómica clínica]] · [[Depleción de ADN humano]] · [[Vigilancia genómica hospitalaria]] · [[Uso clínico y marco regulatorio]]

### Plataformas y herramientas

[[10x Genomics]] · [[GeoMx DSP]] · [[CosMx SMI]] · [[Visium]] · [[Visium HD]] · [[Nanostring]] · [[Vizgen]] · [[BGI]] · [[Oxford Nanopore Technologies]] · [[Plataformas de secuenciación ONT]] · [[Illumina]] · [[PacBio]] · [[Plataformas emergentes de nanoporos]] · [[Dorado]] · [[Porefile]] · [[Nanodisco]]

### Bioinformática — datos y procesamiento

[[Barcode celular]] · [[UMI]] · [[Barcode espacial]] · [[Matriz de conteo]] · [[Profundidad de secuenciación]] · [[Alineamiento de secuencias]] · [[Pseudoalineamiento]] · [[Multimapping]] · [[Squiggle]] · [[K-mer]] · [[POD5]] · [[FASTQ]] · [[Basecalling]]

### Bioinformática — calidad y ensamblaje

[[Calidad Phred]] · [[Perfil de error]] · [[Homopolímeros]] · [[Secuencia consenso]] · [[Pulido de secuencias]] · [[Ensamblaje de novo]] · [[Variantes estructurales]] · [[Clasificación taxonómica]] · [[Secuenciación en tiempo real]]

### Bioinformática — análisis de célula única

[[Control de calidad en scRNA-seq]] · [[Genes mitocondriales]] · [[Reducción dimensional]] · [[PCA]] · [[UMAP]] · [[Clustering]] · [[Anotación de tipos celulares]] · [[Expresión diferencial]] · [[Gene Ontology]] · [[Pseudobulk]] · [[Pseudotiempo]]

### Desafíos

[[Sparsity]] · [[Batch effect]] · [[Alta dimensionalidad]] · [[Identidad celular]] · [[Integración de datos multiómicos]] · [[Segmentación celular]] · [[Integración de datos single cell y spatial]] · [[Almacenamiento y visualización]]

### Artefactos de la biología espacial

[[Lateral diffusion]] · [[Optical crowding]] · [[Photobleaching]] · [[Autofluorescencia]] · [[Stage drift]]

### Análisis espacial

[[ROI]] · [[Spatial domains]] · [[Neighborhoods]] · [[Spatial niches]]

### Proyectos

[[Atlas celulares]] · [[Human Cell Atlas]] · [[BRAIN Initiative]] · [[BICCN]] · [[Malaria Cell Atlas]]

### IA

[[Machine Learning]] · [[Deep Learning]] · [[Inteligencia Artificial]]

### Personas e instituciones

[[Guillermo Eastman]] · [[IIBCE]] · [[Cecilia Salazar]] · [[Institut Pasteur de Montevideo]] · [[David Deamer]]

## Navegación

- Curso completo → [[Fronteras y Perspectivas en Bioinformática - MOC]]
- Siguiente módulo → [[Módulo 2 - MOC]]
