---
tags: [bioinformática, nanoporos, análisis]
area: Bioinformática
aliases: [tiempo real, real time, streaming de datos, análisis en tiempo real, secuenciación dinámica]
---

# Secuenciación en tiempo real

Una propiedad estructural de la [[Secuenciación con nanoporos|secuenciación con nanoporos]]: **los datos se generan y analizan mientras la biblioteca está en el equipo**.

> Secuenciación como **proceso dinámico**, no como lote.

## Por qué es posible

Cada molécula produce su señal completa al atravesar el poro, de forma independiente de las demás. No hay ciclos sincronizados que haya que completar antes de tener una lectura utilizable — a diferencia de la secuenciación por síntesis, donde la lectura de un cluster solo existe cuando terminaron los 150 ciclos.

En términos prácticos: a los pocos minutos de empezar ya hay reads completas y basecalleadas.

## Qué habilita

| Consecuencia | Ejemplo |
|---|---|
| **Detener cuando alcanza** | En PromethION se puede parar la corrida cuando hay datos suficientes, lavar y reutilizar la flow cell |
| **Resultados escalonados** | En el flujo de [[Metagenómica clínica\|metagenómica clínica]]: resultado preliminar a **≈2 h** (patógenos + AMR) y resultado final a **≈24 h** (ensamblaje, tipado, informe) |
| **Impacto clínico el mismo día** | La red de metagenómica del NHS reporta resultados clínicamente útiles en ≥7–8 h |
| Selección adaptativa | El equipo puede decidir sobre la marcha qué moléculas seguir leyendo |

## Su costo bioinformático

El análisis deja de ser un pipeline que se corre al final y pasa a ser un **servicio que corre junto a la corrida**, con [[Basecalling|basecalling]] en GPU concurrente, filtros de calidad en línea y umbrales de reporte. La complejidad se muda del algoritmo a la infraestructura — que es exactamente el terreno del [[Módulo 4 - MOC|Módulo 4]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
