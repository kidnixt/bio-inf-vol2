---
tags: [técnica, laboratorio, nanoporos]
area: Técnicas
aliases: [library prep, biblioteca de secuenciación, preparación de biblioteca, kits de secuenciación, adaptador de secuenciación]
---

# Preparación de bibliotecas de secuenciación

El conjunto de pasos de laboratorio que convierte una muestra de ácidos nucleicos en moléculas listas para entrar al secuenciador. En [[Secuenciación con nanoporos|ONT]] implica ligar un **adaptador de secuenciación** que lleva unida la **proteína motora**.

> La preparación de la biblioteca **impacta la calidad de la corrida y, por lo tanto, la generación de los datos**. No es un trámite previo: es una decisión analítica.

## Las estrategias de ONT

| Familia | Kit | Tiempo | Input | Longitud | PCR | [[Metilación del ADN\|Metilación]] | Para qué |
|---|---|---|---|---|---|---|---|
| **ADN nativo** | Ligation | 60 min | ~1 µg gDNA (100–200 fmol amplicones) | = largo del fragmento | No | ✓ | Mayor output |
| | Rapid | **10 min** | ~200 ng gDNA (50 ng amplicones) | Distribución aleatoria según el input | No | ✓ | Preparación más rápida |
| | Ultra-Long | 200 min + incubación O/N | 6M células | **N50 >50 kb** | No | ✓ | Lecturas ultra-largas |
| **ADN amplificado** | Rapid PCR Barcoding | 15 min + PCR | **1–5 ng** gDNA | ~2 kb | Sí | — | Bajo input |
| **Dirigido** | Microbial Amplicon Barcoding | 60 min + PCR | 10 ng gDNA | **16S completo + ITS** | Sí | — | Identificación de bacterias, arqueas y hongos ([[Secuenciación 16S]]) |
| **ARN** | cDNA-PCR | 2,25 h + PCR | 10 ng poly(A)+ o 500 ng ARN total | cDNA full-length | Sí | — | Identificar y cuantificar transcriptos completos |
| | **Direct RNA** | 135 min | 300 ng poly(A)+ o 1 µg ARN total | = largo del ARN | No | ✓ | Detectar bases modificadas "gratis" |

Todas admiten multiplexado.

## El compromiso de fondo

**La PCR abarata el input pero borra las modificaciones de base y acorta las lecturas.** El ADN nativo conserva la longitud y la capa epigenética, pero exige más material y ADN de alto peso molecular. Elegir kit es elegir qué información se está dispuesto a perder.

## Su lugar entre los factores de calidad

La biblioteca condiciona el **contexto molecular** que después el [[Basecalling|basecaller]] tiene que resolver, y determina si habrá o no [[Secuenciación dúplex|lecturas dúplex]] y modificaciones detectables. Ver [[Perfil de error]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
