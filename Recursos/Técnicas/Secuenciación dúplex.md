---
tags: [técnica, nanoporos, calidad]
area: Técnicas
aliases: [duplex, dúplex, simplex, modo de secuenciación, duplex basecalling]
---

# Secuenciación dúplex

Modo de lectura de [[Secuenciación con nanoporos|ONT]] en el que **las dos hebras complementarias de la misma molécula** atraviesan el poro una tras otra, y el [[Basecalling|basecaller]] combina ambas señales para producir una única lectura de consenso.

| Modo | Qué se lee | Calidad típica (Kit 14 + SUP) |
|---|---|---|
| **Simplex** | Una sola hebra | ~Q20–Q26 (99,75% con R10.4.1 + [[Dorado]] v5) |
| **Dúplex** | Ambas hebras de la misma molécula | **~Q30–Q31 (>99,9%)** |

## Por qué funciona

Los errores del nanoporo dependen del **contexto de secuencia** ([[K-mer|k-mers]], [[Homopolímeros|homopolímeros]]). Como las dos hebras presentan contextos complementarios y por lo tanto **distintos**, sus errores no coinciden: cruzarlas cancela buena parte del ruido específico de contexto.

Es el mismo razonamiento que hay detrás del [[Secuencia consenso|consenso]] por cobertura, pero aplicado dentro de **una sola molécula**, sin necesidad de secuenciar la región muchas veces.

## Su costo

No todas las moléculas producen un par dúplex: depende de la química y de la [[Preparación de bibliotecas de secuenciación|preparación de la biblioteca]], y el rendimiento en reads dúplex es una fracción del total. Se paga throughput a cambio de exactitud por lectura.

En la clase aparece como uno de los cuatro factores de plataforma que determinan la calidad de la **lectura individual**, junto con el poro y la química, el modelo de basecalling y la versión de [[Dorado]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
