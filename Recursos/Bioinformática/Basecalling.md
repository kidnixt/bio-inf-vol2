---
tags: [bioinformática, nanoporos, señal, deep-learning]
area: Bioinformática
aliases: [asignación de bases, basecaller, basecallers, base calling]
---

# Basecalling

El proceso computacional donde la **señal eléctrica es convertida al formato de secuencia nucleotídica** (ADN o ARN). Es el paso que traduce física en biología, y en [[Secuenciación con nanoporos|nanoporos]] es un problema de aprendizaje automático, no una conversión determinista.

## Por qué no es una tabla de conversión

> **ONT no detecta cada nucleótido de forma aislada.**
> La corriente está determinada por un grupo corto de nucleótidos —un **[[K-mer|k-mer]]**— situado simultáneamente en la región sensible del nanoporo.

Cada nivel de corriente corresponde a un **contexto de varias bases**, no a un carácter. Decodificar la secuencia es entonces encontrar la trayectoria de contextos más probable que explique la traza observada — y ahí es donde entran las redes neuronales.

Ese hecho estructural explica también buena parte del [[Perfil de error]]: los [[Homopolímeros|homopolímeros]] son difíciles porque desplazar la molécula una base no cambia el k-mer, y por lo tanto no cambia la corriente.

## El flujo de datos

```
señal eléctrica → POD5 → basecaller → FASTQ / BAM
   (squiggle)                          (+ Q-scores, tags MM/ML)
```

- La señal cruda se guarda en [[POD5]] (antes FAST5); la traza se llama [[Squiggle|squiggle]].
- El basecaller actual y oficial de ONT es **[[Dorado]]** (v2.1.2 en la clase).
- La salida lleva [[Calidad Phred|Q-scores]] por base y, opcionalmente, probabilidades de [[Metilación del ADN|modificación]].

## La evolución de los basecallers

Han evolucionado junto con la química de secuenciación:

| Basecaller | Período | Rasgos |
|---|---|---|
| **Metrichor** | 2014–2017 | Basecalling en la **nube**; primer flujo oficial; enfoque temprano basado en eventos |
| **Albacore** | 2017–2018 | Basecalling **local**; *raw basecalling*; mayor autonomía y precisión |
| **Guppy** | 2018–2024 (*legacy*) | **GPU** y tiempo real; modelos Fast/HAC/SUP; demultiplexado y bases modificadas |
| **[[Dorado]]** | 2023–actualidad | Actual y oficial; integrado en MinKNOW; simplex y [[Secuenciación dúplex\|dúplex]]; ADN y ARN; más rápido y preciso |
| **Bonito** | 2019–actualidad | Rama de **investigación**, código abierto, entrenamiento y evaluación de modelos |

Trayectoria: **nube → local → GPU/tiempo real → ecosistema moderno**.

## FAST, HAC y SUP

Los modelos neuronales **FAST, HAC y SUP** están optimizados para distintos compromisos entre **velocidad de inferencia y exactitud** (SUP > HAC >> FAST en calidad, al revés en velocidad).

## La propiedad singular: rebasecallear

Como la señal cruda se conserva, **el mismo experimento puede volver a analizarse años después** con un modelo mejor y dar una secuencia más exacta, sin volver al laboratorio. Ningún otro tipo de dato de secuenciación tiene esta propiedad.

Su contracara es que **la versión del basecaller y el modelo son parte del resultado** y deben registrarse — un requisito explícito para el [[Uso clínico y marco regulatorio|uso clínico]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
- [[Métodos para el diseño computacional de fármacos]]
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
