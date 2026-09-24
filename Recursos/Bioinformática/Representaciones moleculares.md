---
tags: [concepto, bioinformática, quimioinformática]
area: Bioinformática
aliases: [SMILES, fingerprint, fingerprints, MACCS, grafo molecular, confórmero, descriptores moleculares]
---

# Representaciones moleculares

Las distintas formas de escribir una molécula para que un modelo la procese. La tesis de la clase:

> **La representación decide qué diferencias puede aprender el modelo.**

| Representación | Qué es | Ejemplo | Ventaja |
|---|---|---|---|
| **Propiedades fisicoquímicas** | Texto/numérico | logP, peso molecular | Ligero |
| **SMILES** | Texto químico | `O=C(O)c1ccccc1O` (ácido salicílico) | Ligero y **secuencial** |
| **Fingerprint** | Vector de bits de subestructuras | MACCS (166 bits) | Rápido para [[Similitud química\|similitud]] |
| **Grafo molecular** | Átomos (nodos) y enlaces (aristas) | — | Aprendizaje **local** |
| **Confórmero 3D** | Geometría | Varios confórmeros de la misma molécula | Interacciones **espaciales** |

La diapositiva lo muestra con una sola molécula —el **ácido salicílico**— escrita de cuatro maneras: SMILES, fingerprint MACCS, grafo numerado y tres confórmeros 3D.

## Por qué importa la elección

- Un modelo sobre **fingerprints** solo puede distinguir moléculas que difieran en las subestructuras codificadas. Un [[Activity cliff|activity cliff]] causado por un choque estérico en 3D le es invisible.
- Un modelo sobre **SMILES** ve una secuencia de caracteres — y por eso las arquitecturas de lenguaje (incluido el [[Transformer]]) se le aplican directamente.
- Un modelo sobre **grafos** (GNN) aprende relaciones locales entre átomos vecinos.
- Un modelo sobre **3D** puede capturar lo que ninguno de los anteriores ve, a costa de tener que elegir *qué* confórmero.

El aporte de la [[Inteligencia Artificial|IA]] en esta etapa es reemplazar descriptores **definidos previamente** por **representaciones aprendidas**. Del lado de las proteínas, la jugada equivalente son los [[Embedding|embeddings]] de los [[Modelo de lenguaje de proteínas|PLMs]].

Ver también [[Reglas de drug-likeness]] (el uso de propiedades fisicoquímicas como filtro).

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
