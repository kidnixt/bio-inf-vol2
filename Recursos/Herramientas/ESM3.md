---
tags: [herramienta, modelo, PLM, generativo, multimodal]
area: Herramientas
aliases: [esmGFP, EvolutionaryScale ESM3]
---

# ESM3

El modelo **multimodal y generativo** de EvolutionaryScale (Hayes et al., 2025, *Science*, *Simulating 500 million years of evolution with a language model*). `github.com/evolutionaryscale/esm`

## Tres modalidades, un vocabulario

Si [[ProstT5]] une **dos** modalidades, ESM3 une **tres**:

| Secuencia | Estructura | Función |
|---|---|---|
| Las 20 letras | Coordenadas 3D **como tokens** | Palabras clave, sitios catalíticos |

Las tres pistas entran como **tokens discretos** y se fusionan en un solo **espacio latente**. El primer bloque lleva **atención geométrica**, que permite condicionar por coordenadas atómicas.

| | |
|---|---|
| Parámetros | **98.000 millones** |
| Cómputo | más de 10²⁴ FLOPS — un orden de magnitud más que [[ESM-1b y ESM-2\|ESM-2]] |
| Entrenamiento | Se enmascara todo y se rellena **posición por posición** |
| Versión abierta | 1.4B, licencia MIT |

**El diseño se puede guiar** dando parte de la secuencia, parte de la estructura, o una palabra de función. Eso convierte al modelo en una herramienta de **diseño *de novo***, no solo de representación.

## esmGFP: una proteína que no existía

Se le dio **solo la estructura de los residuos del núcleo** de una GFP natural (los que forman y catalizan el cromóforo). ESM3 razonó en cadena, probó **96 generaciones** y encontró proteínas que **fluorescen de verdad**, medidas en lisado de *E. coli*.

Desde el pocillo B8 (57 % de identidad) siguió la cadena hasta C10: **esmGFP**, con **58 % de identidad** y **96 mutaciones sobre 229 aminoácidos**. El equivalente, según los autores, a **≈ 500 millones de años** de evolución.

> [!note] Matiz importante
> No es que el modelo **"sepa" biología**. Simula evolución porque **predecir el token enmascarado lo obliga** a aprender cómo se mueve la evolución en el espacio de proteínas posibles. Ver los límites en [[Modelo de lenguaje de proteínas]].

De la fidelidad al *prompt* sale un matiz práctico: **promptear por estructura funciona muy bien** (cRMSD bajo con pTM alto), mientras que **SASA y palabras clave son las pistas más flojas**.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Hayes et al 2025 - Simulating 500 million years of evolution]] *(lectura)*
