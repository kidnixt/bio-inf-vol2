---
tags: [herramienta, software, basecalling, nanoporos]
area: Herramientas
aliases: [dorado, Remora, basecaller de ONT]
---

# Dorado

El **[[Basecalling|basecaller]] actual y oficial** de [[Oxford Nanopore Technologies|ONT]] (2023–actualidad; versión citada en la clase: **v2.1.2**). Convierte la señal eléctrica cruda almacenada en [[POD5]] a secuencia en [[FASTQ]] / BAM / CRAM.

Está integrado en MinKNOW, corre en GPU, y soporta ADN y ARN, modo simplex y [[Secuenciación dúplex|dúplex]], y bases modificadas.

## Cómo funciona por dentro

| # | Etapa | Detalle |
|---|---|---|
| 1 | Señal cruda ([[POD5]]) | Corriente iónica medida por el nanoporo |
| 2 | Preprocesamiento | Escalado, normalización, recorte, división en *chunks* con solapamiento (cada chunk se procesa de forma independiente) |
| 3 | **Inferencia neuronal** | **CNN** (capas convolucionales 1D para extraer características locales) + **Transformer** (dependencias de largo alcance en la señal) |
| 4 | Representación estructurada | **CRF** — campo aleatorio condicional que modela transiciones entre contextos de [[K-mer\|k-mers]]. Ej.: estado de largo 5 → 4⁵ = **1024 contextos posibles** |
| 5 | Decodificación | ***Beam search***: se consideran múltiples hipótesis y se selecciona la mejor trayectoria |
| 6 | Secuencia y calidad | Salida con [[Calidad Phred\|Q-scores]] |

## Modelos: FAST, HAC y SUP

Tres modelos neuronales optimizados para distintos compromisos entre **velocidad de inferencia y exactitud**:

| Modelo | Perfil |
|---|---|
| **FAST** | Máxima velocidad, mayor error |
| **HAC** (*high accuracy*) | Punto intermedio, el más usado en producción |
| **SUP** (*super accuracy*) | Máxima exactitud, mucho más cómputo |

**SUP > HAC >> FAST** en calidad. Como la señal se conserva, el mismo POD5 puede **rebasecallearse** más tarde con un modelo mejor o una versión más nueva de Dorado y ganar exactitud sin volver al laboratorio — por eso la clase insiste en registrar la **versión del basecaller y el modelo** como metadato trazable.

## Bases modificadas y Remora

Dorado puede realizar **conjuntamente** el basecalling y la inferencia de determinadas [[Metilación del ADN|modificaciones]], mediante modelos específicos preentrenados:

| Molde | Modificaciones |
|---|---|
| ADN | A → **6mA** · C → **4mC**, **5mC**, **5hmC** |
| ARN | A → m6A · C → m5C · U → pseudouridina · inosina · 2'-O-metilaciones (Am/Cm/Gm/Um) |

Las probabilidades se emiten como *tags* **MM/ML** en el BAM, y alimentan el análisis posterior: Modkit, visualización en IGV, identificación de motivos, metiloma y epitranscriptoma.

**Remora** es el proyecto hermano de ONT que separa el *calling* de bases modificadas del basecalling propiamente dicho.

## Su linaje

Metrichor (2014–2017, nube) → Albacore (2017–2018, local) → Guppy (2018–2024, GPU, *legacy*) → **Dorado**. En paralelo, **Bonito** es la rama de investigación de código abierto (2019–actualidad), usada para entrenar y evaluar modelos, no para producción.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
