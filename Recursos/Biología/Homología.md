---
tags: [concepto, biología, evolución]
area: Biología
aliases: [homólogos, homólogo, ortólogos, parálogos, divergencia]
---

# Homología

Dos secuencias son **homólogas** cuando descienden de un ancestro común. No es una medida de parecido: es una afirmación **histórica**. Dos proteínas pueden ser muy parecidas sin ser homólogas (convergencia) o muy distintas y sí serlo ([[Homología remota]]).

## En la tabla de "ediciones al texto"

La clase 9 la presenta como una de las **tres ediciones** que puede sufrir la secuencia de una proteína, y subraya que no son equivalentes:

| Edición | Ejemplo | Qué significa |
|---|---|---|
| **Mutación puntual** | `MKVLAG` → `MKVFAG` | Cambia una letra: el "error tipográfico". Puede ser silencioso **o destruir la función** |
| **[[Permutación circular]]** | `MKVAG` → `AGMKV` | Se corta y se reordena: las mismas letras, otro orden |
| **Homología** | humano `MKVLAG` / ratón `MKILSG` | **No es un error: es divergencia** desde un ancestro común. **El texto cambió y la función se conservó** |

> **Por qué importa para un modelo de lenguaje:** los tres casos producen secuencias parecidas pero **significan cosas distintas**. Un modelo que solo cuente letras no los distingue; uno que aprenda **contexto**, sí.

## Su papel doble en la clase

La homología es a la vez **la señal** y **el límite** de la bioinformática clásica:

- **La señal:** un [[Alineamiento múltiple de secuencias|MSA]] de homólogos es de donde salía toda la información evolutiva — conservación, covariación, [[Mapa de contactos|contactos]]. [[AlphaFold]] 2 y el [[Modelado por homología]] se apoyan en ella.
- **El límite:** cuando no hay homólogos detectables (proteínas metagenómicas del [[ESM Atlas]], proteínas de [[Bacteriófago|fagos]]), el método clásico no tiene de dónde agarrarse. Ahí es donde los [[Modelo de lenguaje de proteínas|PLMs]] aportan algo nuevo: traen lo que aprendieron **del resto del universo de proteínas**.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
