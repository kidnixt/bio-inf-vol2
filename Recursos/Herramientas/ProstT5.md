---
tags: [herramienta, modelo, PLM, estructura]
area: Herramientas
aliases: [ProstT5, AA2fold, fold2AA]
---

# ProstT5

[[Modelo de lenguaje de proteínas|PLM]] **bilingüe**: lee y escribe tanto secuencia de aminoácidos como **forma**, usando el [[Alfabeto 3Di|alfabeto 3Di]] de [[Foldseek]] (Heinzinger et al., 2024, *NAR Genomics and Bioinformatics* 6(4), lqae150). `huggingface.co/Rostlab/ProstT5`

## La jugada

Los modelos anteriores leen **solo la secuencia**. Pero una proteína también **es** una estructura 3D. ¿Se puede escribir la forma con letras?

> **Otra vez, 20 letras.** El alfabeto 3Di usa 20 símbolos, así que **un PLM lo lee sin cambiar de arquitectura**. Foldseek lo inventó; ProstT5 lo aprendió.

**Traducción en dos sentidos**, marcada con tokens de control:

| Token | Dirección | Para qué |
|---|---|---|
| `<AA2fold>` | secuencia → forma | Predecir el 3Di **sin calcular la estructura**, y buscar con eso. **×1000 más rápido** que extraer el 3Di de una estructura predicha |
| `<fold2AA>` | forma → secuencia | ***[[Inverse folding]]***: proponer secuencias que adopten una forma dada. Diseño guiado por **la forma** |

Se preentrena en dos etapas (*span denoising* sobre un subconjunto de alta calidad de AFDB, y después traducción bidireccional secuencia↔estructura).

## El resultado más fuerte

El 3Di **predicho** es tan bueno que, pasado a Foldseek, detecta **[[Homología remota|homología remota]]** —proteínas muy divergentes con la misma forma— **casi al nivel de usar estructuras experimentales**. Sin [[Alineamiento múltiple de secuencias|MSA]] y sin predecir coordenadas 3D: **la señal estructural ya está en los embeddings**.

## Dónde se usa

- [[Phold]] lo usa para anotar genomas de bacteriófagos por forma.
- El trabajo de tesis de **Juan Diego Puglia** (ORT) lo usa junto a [[ESM-1b y ESM-2|ESM-C]] para representar proteínas y predecir localización subcelular.

> [!warning] Ojo con los nombres
> **[[ProtT5 y ProtBERT|ProtT5]]** lee secuencia (1D). **ProstT5** —con **s**— lee secuencia *y* estructura (3D).

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
