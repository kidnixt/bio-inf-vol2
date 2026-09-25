---
tags: [concepto, bioinformática, IA, proteínas]
area: Bioinformática
aliases: [PLM, PLMs, protein language model, modelos de lenguaje de proteínas, Ankh]
---

# Modelo de lenguaje de proteínas

Un **PLM** es un modelo entrenado sobre secuencias de aminoácidos con las mismas técnicas que los modelos de lenguaje natural, para producir [[Embedding|representaciones vectoriales]] de proteínas.

## La premisa

Una proteína **es texto**:

| Ingeniería (lenguaje) | Biotecnología (proteínas) |
|---|---|
| ~27 letras → palabras → oraciones | 20 aminoácidos → motivos → proteínas |

| Nivel biológico | Equivalente en lenguaje | Qué captura |
|---|---|---|
| Estructura primaria | Texto plano | El orden de los símbolos |
| Estructura secundaria | Morfología | Patrones locales |
| **Estructura terciaria** | **Sintaxis y gramática** | **Elementos distantes que se relacionan** |
| Función biológica | Semántica | El significado global |

La tercera fila es la que justifica todo: las dependencias a larga distancia son el problema que el [[Transformer]] resuelve.

## La genealogía

| Año | Modelo | Qué agrega |
|---|---|---|
| 2013 | [[Word2vec]] | Vectores densos (en lenguaje natural) |
| 2015 | [[ProtVec]] | La idea, aplicada a [[K-mer\|3-meros]] — pero **sin contexto** |
| 2019 | [[ELMo y SeqVec\|SeqVec]] | El vector **depende del entorno** |
| 2021 | [[ProtT5 y ProtBERT]] | Transformers a escala, **sin [[Alineamiento múltiple de secuencias\|MSA]]** |
| 2021–23 | [[ESM-1b y ESM-2]] | La **estructura emerge**; escala a 15 B de parámetros |
| 2024 | [[ProstT5]] | Bilingüe: secuencia **y** forma |
| 2025 | [[ESM3]] | Secuencia, estructura y función; **generativo** |

> **El patrón:** cada salto agrega **contexto**. Primero una letra, después su entorno, después la secuencia entera, después la forma — y finalmente la función.

## Qué aprende sin que nadie se lo diga

Entrenado **solo con secuencias sin etiquetar**, un PLM aprende propiedades **biofísicas** (hidrofobicidad, carga, peso), **estructura secundaria** (hélices y láminas) y **contactos 3D**.

> **Por qué funciona:** la evolución **ya resolvió el problema**. Las secuencias que existen son las que **se pliegan y funcionan**. El modelo absorbe esas restricciones sin que nadie se las explicite.

## ¿Más grande o mejor diseñado?

| La narrativa del *scaling* | **Ankh**: el contrapunto |
|---|---|
| Más parámetros → representaciones más ricas | Optimiza **para proteínas** en vez de escalar |
| Tendencia dominante | Estado del arte con **< 10 %** de parámetros |
| Cuesta cómputo, dinero y energía | **< 7 %** de inferencia · **< 30 %** de dimensión |

> **La accesibilidad importa:** un modelo que corre en hardware modesto **democratiza la investigación**. *(Elnaggar et al., arXiv:2301.06568)*

Lo confirma el resultado local: en el trabajo de Juan Diego Puglia (ORT), el mejor de los tres modelos fue **ESM-C 300m**, el más chico.

## Lo que estos modelos *no* hacen

> **No "entienden" biología.** Aprenden **correlaciones estadísticas de la evolución**. No simulan física, ni química, ni termodinámica.

| Situación | Qué pasa |
|---|---|
| Proteína **sin homólogos** conocidos | Poco de dónde aprender |
| Mutación que cambia **la física** | Puede no anticiparla |
| Condiciones ***in vivo*** reales | Fuera de su alcance |

> **Un buen *score in silico* es una hipótesis, no un resultado.** *La mesada sigue mandando.*

Es la misma conclusión que la clase 6 saca sobre los scores de [[Docking molecular|docking]] (ver [[Función de puntuación]]).

## Usar vs. entrenar

| Usar un PLM | Entrenar un PLM |
|---|---|
| Pesos preentrenados (HuggingFace) | Miles de GPU-hora |
| Inferencia en **una GPU de consumo** | Clusters especializados |
| **Accesible hoy** | **Barrera real de entrada** |

> **Entrenar es de pocos; usar es de casi todos.**

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Métodos para el diseño computacional de fármacos]]
- [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences]] *(lectura)*
- [[Elnaggar et al 2021 - ProtTrans]] *(lectura)*
- [[Elnaggar et al 2023 - Ankh]] *(lectura)*
- [[Hayes et al 2025 - Simulating 500 million years of evolution]] *(lectura)*
- [[Heinzinger et al 2019 - SeqVec]] *(lectura)*
- [[Heinzinger et al 2024 - ProstT5]] *(lectura)*
- [[Lin et al 2023 - Evolutionary-scale prediction with a language model]] *(lectura)*
- [[Mikolov et al 2013 - Efficient estimation of word representations]] *(lectura)*
- [[Rives et al 2021 - Biological structure and function emerge from scaling]] *(lectura)*
