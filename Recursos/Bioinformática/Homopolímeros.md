---
tags: [bioinformática, secuencias, error]
area: Bioinformática
aliases: [homopolímero, homopolymer, STR, regiones de baja complejidad, short tandem repeats]
---

# Homopolímeros

Tramos de una misma base repetida (`AAAAAA`, `TTTTTTTT`). Son el caso difícil clásico de la [[Secuenciación con nanoporos|secuenciación con nanoporos]], y la razón principal de sus errores de tipo **indel**.

## Por qué fallan

La corriente del nanoporo responde al **[[K-mer|k-mer]]** presente en la región sensible. Dentro de un homopolímero, avanzar una base **no cambia el k-mer**, así que la corriente se mantiene plana: no hay transición que contar. El largo del tramo debe inferirse de **cuánto tiempo** dura ese nivel, y el tiempo depende de la velocidad de translocación, que fluctúa.

De ahí el error característico: acertar la base, errar cuántas veces está.

El mismo problema afecta a los **STR** (*short tandem repeats*) y a otras regiones de baja complejidad, aunque de forma más leve.

## Cómo se ataca

| Estrategia | Efecto |
|---|---|
| **Poro R10.4.1** con doble región sensible | Dos constricciones producen dos lecturas desfasadas del mismo tramo: mejora la resolución **especialmente en homopolímeros** |
| Modelos [[Basecalling\|basecaller]] SUP | Mejor modelado de la duración de los estados |
| [[Secuenciación dúplex\|Dúplex]] | Las dos hebras tienen contextos complementarios distintos |
| Cobertura y [[Pulido de secuencias\|pulido]] | Corrige el largo en la [[Secuencia consenso\|secuencia consenso]] |

La [[Sequencing by Expansion|SBX de Roche]] elimina el problema de raíz por otra vía: separa espacialmente los reporteros para que nunca haya dos bases idénticas contribuyendo a la misma señal.

## Por qué importa en microbiología

Un indel dentro de una región codificante produce un **corrimiento del marco de lectura**, y eso puede hacer que un gen de [[Resistencia antimicrobiana|resistencia]] real aparezca como pseudogén, o al revés. En genómica bacteriana el problema del homopolímero no es cosmético: cambia la anotación.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
