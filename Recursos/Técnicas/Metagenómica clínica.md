---
tags: [técnica, metagenómica, clínica, microbiología]
area: Técnicas
aliases: [metagenómica, mNGS, metagenómica respiratoria, secuenciación metagenómica]
---

# Metagenómica clínica

Secuenciación **sin selección previa** de todo el material genético presente en una muestra clínica, para identificar simultáneamente bacterias, hongos, virus ADN y ARN, y sus genes de [[Resistencia antimicrobiana|resistencia]] — sin necesidad de sospechar de antemano qué buscar.

Es lo que la clase llama **detección agnóstica**: un solo ensayo en lugar de una batería de tests dirigidos.

## El caso de referencia

La **NHS Respiratory Metagenomics Network** (`metagenomics.nhs.uk`) es la implementación más consolidada: metagenómica con [[Secuenciación con nanoporos|ONT]] dentro del sistema de salud británico para infecciones respiratorias, con resultado en **~6–24 h** e impacto terapéutico el mismo día. Hospitales participantes citados: Guy's & St Thomas', Great Ormond Street, Southampton, Newcastle.

## Qué aporta

| # | Aporte | Dato |
|---|---|---|
| 1 | Respuesta rápida | Resultados clínicamente útiles el mismo día (≥7–8 h) |
| 2 | Detección agnóstica | Bacterias, hongos y virus ADN/ARN en un solo ensayo |
| 3 | Más diagnósticos | **30%** de las muestras con detecciones adicionales |
| 4 | Tratamiento dirigido | **28%** cambios terapéuticos, **21%** desescalación |
| 5 | Resistencia | Genes de AMR para selección precoz de terapia |
| 6 | Control de infecciones | **14%** con implicancias para control de infecciones / salud pública |
| 7 | Más allá de la infección | **20%** contribuyó a decisiones de inmunomodulación |

Impacto en tres niveles: **paciente** (etiología rápida, terapia personalizada), **hospital** (brotes, AMR, control de infecciones) y **salud pública** ([[Vigilancia genómica hospitalaria|vigilancia genómica]] y patógenos emergentes).

> No solamente amplía el número de microorganismos que podemos detectar: **integra diagnóstico, resistencia y epidemiología dentro de una misma ventana temporal clínicamente útil**.

## El flujo bioinformático

| Etapa | Herramientas |
|---|---|
| Preparación | Lisis y **[[Depleción de ADN humano\|depleción de ADN humano]]** |
| Secuenciación | GridION / PromethION, [[Secuenciación en tiempo real\|tiempo real]] |
| [[Basecalling]] y QC | Guppy / MinKNOW, filtros Q ≥ 10 |
| Eliminación de humano | Alineamiento a **GRCh38** |
| [[Clasificación taxonómica]] | **Centrifuge** + base curada |
| **≈2 h → preliminar** | Patógenos (umbrales clínicos) + AMR (**Abricate + CARD + Scagaire**) |
| [[Ensamblaje de novo\|Ensamblaje]] / [[Secuencia consenso\|consenso]] | **minimap2**, **Medaka**, **bcftools** |
| Tipado y vigilancia | **Nextclade**, **SNP-sites**, MLST |
| **≈24 h → final** | Informe clínico integrado |

Cada etapa **introduce posibles sesgos**: el flujo es rápido, pero no neutro.

## Limitaciones

| # | Limitación | Detalle |
|---|---|---|
| 1 | Sensibilidad en baja carga | Pierde microorganismos poco abundantes, sobre todo **virus ARN**; peor límite de detección que la PCR |
| 2 | Preparación de la muestra | La depleción de ADN humano **también reduce material microbiano**; varía por tipo de muestra |
| 3 | Genoma incompleto | No siempre hay cobertura para ensamblar; limita AMR, tipado y vigilancia |
| 4 | Infección vs colonización | Detectar no es causar; requiere correlación clínica |
| 5 | Escalabilidad | Necesita automatización y throughput; flujo más complejo que el cultivo |
| 6 | Validación clínica | Faltan estudios multicéntricos y controlados; impacto en *outcomes* en evaluación |

> [!danger] Las tres desigualdades
> **detección ≠ infección** · **gen de AMR ≠ fenotipo** · **resultado rápido ≠ beneficio clínico demostrado**

El cuello de botella principal, según el cierre de la clase, es doble: la **baja proporción de ADN microbiano frente al humano** y la capacidad de analizar los datos de forma **reproducible**.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
