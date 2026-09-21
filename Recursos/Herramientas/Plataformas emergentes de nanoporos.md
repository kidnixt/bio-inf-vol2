---
tags: [herramienta, plataforma, nanoporos, emergente]
area: Herramientas
aliases: [QitanTech, QNome, CycloneSEQ, MGI, PolyseqOne, AxiLona, Axbio, Gseq-500, Geneus, QNome-3841]
---

# Plataformas emergentes de nanoporos

Durante más de una década [[Oxford Nanopore Technologies|ONT]] fue el único actor con nanoporos comerciales. Eso terminó: hay al menos cinco competidores con producto, y uno de ellos es Roche.

> [!warning] Todas las especificaciones de esta nota son **declaradas por el fabricante** y **requieren validación independiente**.

## El panorama

| Plataforma | Origen | Principio | Rendimiento | Exactitud | Observaciones |
|---|---|---|---|---|---|
| **QitanTech** — QNome-3841, QCell-384 | China | Nanoporo | Menor que ONT | 99% reportada | Algunas herramientas creadas para ONT aceptan su [[FASTQ]]; distribución limitada principalmente a China |
| **MGI CycloneSEQ** — G100 | China | Nanoporo | **>50 Gb por celda** en evaluaciones iniciales independientes | Algo inferior a la química ONT R10.4.1 | Un benchmark cross-platform reporta errores de sustitución asociados a metilación |
| **PolyseqOne** | China | Nanoporo | >50 Gb por celda | **>99%** | Requiere validaciones independientes; usada para identificar un nuevo alelo HLA-DPA1 |
| **Axbio AxiLona AXP-100** | — | *Nanopore sequencing by synthesis* (NSBS / EL-NGS) | — | **>99% tras consenso circular** | Longitud ≥10 kb hasta 100 kb; sensores sobre arrays CMOS |
| **Geneus Gseq-500** | China | NSBS | 15 Gb en 10 h | 93,25% | ADN y ARN; [[Basecalling\|basecalling]] en tiempo real |
| **Roche AXELIOS 1** | — | [[Sequencing by Expansion\|SBX]] | **≥1,8 Tb** | Error ~1:6000 (**Q38**) | No introduce ADN nativo en el poro; **lecturas cortas** |

## Dos familias conceptuales

1. **Réplicas del enfoque ONT** (QitanTech, CycloneSEQ, PolyseqOne): ADN nativo atravesando el poro, con las mismas propiedades y los mismos problemas. Su ventaja buscada es de costo y de acceso regional.
2. **Nanoporo como detector, no como lector** (Axbio, Geneus, Roche): el poro detecta señales generadas por una reacción de síntesis o por un polímero sintético. Sacrifican la lectura larga y el ADN nativo —y con ellos la [[Metilación del ADN|información epigenética]]— a cambio de exactitud y throughput.

## La línea de tiempo del campo

Las químicas se suceden **R6 → R7 → R7.3 → R9 → R9.4 → R9.5 → R10 → R10.3 → R10.4 → R10.4.1**, con los equipos apareciendo en paralelo: MinION (2014), primer genoma humano con MinION (2016), PromethION (2018), Flongle y primer secuenciador chino QNome-9604 (2020), PromethION 2 / QNome-3841hex / Gseq-500 (2022, el año en que *Nature Methods* eligió la secuenciación de lecturas largas como método del año), PolyseqOne y CycloneSEQ (2024)… y al final, un signo de interrogación: **¿Roche? ¿Illumina? ¿Quién sigue?**

*Zhang T., et al. (2024). https://doi.org/10.1016/j.jgg.2024.09.007*

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
