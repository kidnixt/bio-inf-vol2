---
tags: [técnica, secuenciación, plataforma-emergente]
area: Técnicas
aliases: [SBX, Xpandomer, AXELIOS, Roche SBX, secuenciación por expansión]
---

# Sequencing by Expansion (SBX)

Tecnología presentada por **Roche** en la plataforma **AXELIOS 1** (junio de 2026). Usa nanoporos, pero rompe con el supuesto central de la [[Secuenciación con nanoporos|secuenciación con nanoporos]] convencional.

## El giro conceptual

> **No introduce ADN nativo en el poro.**

En lugar de eso, la secuencia se **convierte en un polímero sintético expandido** llamado **Xpandomer**, en el que cada nucleótido original está representado por un reportero mucho más grande y químicamente distinguible. Ese polímero es el que atraviesa el nanoporo.

Al separar espacialmente los reporteros, se elimina el problema estructural de ONT —que la corriente responde a un [[K-mer|k-mer]] completo y no a una base— y con él buena parte del [[Perfil de error]] dependiente de contexto, [[Homopolímeros|homopolímeros]] incluidos.

## Especificaciones reportadas

| | |
|---|---|
| Rendimiento | **≥1,8 Tb** |
| Longitud | **Lecturas cortas** |
| Error | ~1:6000, aprox. **Q38** |

## Por qué es interesante

Invierte el mapa mental del campo: nanoporo dejó de ser sinónimo de lectura larga y ADN nativo. SBX usa el nanoporo como **detector de altísima sensibilidad** y renuncia deliberadamente a la longitud y a la [[Metilación del ADN|información epigenética]] a cambio de exactitud y throughput.

La línea de tiempo de la clase cierra justamente con esa incógnita: *¿Roche? ¿Illumina? ¿Quién sigue?*

Ver también [[Plataformas emergentes de nanoporos]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
