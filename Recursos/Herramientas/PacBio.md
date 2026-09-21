---
tags: [herramienta, plataforma, secuenciación, lecturas-largas]
area: Herramientas
aliases: [Pacific Biosciences, HiFi, PacBio HiFi, Revio, SMRT, ZMW]
---

# PacBio

La otra plataforma de [[Secuenciación de tercera generación|tercera generación]], junto con [[Secuenciación con nanoporos|Oxford Nanopore]]. Secuenciación de **molécula única en tiempo real** (SMRT).

## Cómo genera la secuencia

Una polimerasa fijada al fondo de un pozo de escala zeptolitro (**ZMW**, *zero-mode waveguide*) sintetiza la hebra complementaria incorporando nucleótidos marcados. La señal son **pulsos de fluorescencia en tiempo real asociados a cada incorporación de nucleótido**.

> PacBio = fluorescencia de molécula única en tiempo real.

## HiFi

La molécula se circulariza y la polimerasa **da varias vueltas sobre el mismo molde**. El consenso de esas pasadas repetidas produce las lecturas **HiFi**: largas y con exactitud comparable a la de lectura corta.

| | |
|---|---|
| Longitud | Hasta 25 kb (típicas ~15 kb) |
| Exactitud | 99,9% oficial; hasta 99,95% (**Q33**) |
| Error equivalente | ~0,1% a 0,05% — 1 error cada 1.000–2.000 bases |
| Sistema actual | **Revio** |

## Frente a ONT

| | PacBio HiFi | ONT |
|---|---|---|
| Exactitud por lectura | Mayor (Q30–Q33) | Q26 simplex, Q30+ [[Secuenciación dúplex\|dúplex]] |
| Longitud máxima | ~25 kb | Ultra-long: >50 kb N50, reads >4 Mb |
| Portabilidad | Equipo de laboratorio | Desde 130 g |
| Datos crudos | — | Señal conservada y **rebasecalleable** ([[POD5]]) |

La estrategia de consenso circular de HiFi reaparece en algunas [[Plataformas emergentes de nanoporos|plataformas emergentes]] de nanoporos, como AxiLona.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
