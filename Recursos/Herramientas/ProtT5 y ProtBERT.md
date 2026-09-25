---
tags: [herramienta, modelo, PLM, transformer]
area: Herramientas
aliases: [ProtT5, ProtBERT, ProtTrans, Rostlab]
---

# ProtT5 y ProtBERT

Los dos modelos principales del proyecto **ProtTrans** (Elnaggar et al., 2021, *IEEE TPAMI*), que llevó el [[Transformer]] a las proteínas a gran escala. Disponibles en `huggingface.co/Rostlab`.

| Modelo | Arquitectura | Objetivo de entrenamiento |
|---|---|---|
| **ProtBERT** | Solo *encoder* | [[Masked language modeling\|Masked]] |
| **ProtT5** | *Encoder-decoder* | *Denoising* (reconstruir tramos corruptos) |

## Lo que demostró

- Un [[Modelo de lenguaje de proteínas|PLM]] **sin [[Alineamiento múltiple de secuencias|MSA]]** ni información evolutiva explícita **iguala o supera** a los métodos clásicos.
- Sus [[Embedding|embeddings]] alimentan **clasificadores simples** y aun así rinden — el patrón que después reaparece en el caso de Puglia y en la sonda de contactos de [[ESM-1b y ESM-2|ESM-1b]].

> **Sin alineamientos.** La información evolutiva que los métodos clásicos sacaban de un MSA, el modelo **la aprende de haber visto millones de secuencias**. Esa es la afirmación central de toda la familia.

En el benchmark de localización subcelular, ProtT5 y ProtBERT compiten de igual a igual con ESM-1b, DeepLoc y los métodos con información evolutiva explícita.

> [!warning] Ojo con los nombres
> **ProtT5** lee secuencia (1D). **[[ProstT5]]** —con **s**— lee secuencia *y* estructura (3D). Son modelos distintos, del mismo grupo.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences]] *(lectura)*
- [[Elnaggar et al 2021 - ProtTrans]] *(lectura)*
- [[Elnaggar et al 2023 - Ankh]] *(lectura)*
- [[Heinzinger et al 2019 - SeqVec]] *(lectura)*
- [[Heinzinger et al 2024 - ProstT5]] *(lectura)*
- [[Rives et al 2021 - Biological structure and function emerge from scaling]] *(lectura)*
