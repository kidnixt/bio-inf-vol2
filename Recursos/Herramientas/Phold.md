---
tags: [herramienta, software, anotación, virus]
area: Herramientas
aliases: [phold]
---

# Phold

Anotador de genomas de **[[Bacteriófago|bacteriófagos]]** que funciona **por estructura** en vez de por secuencia (Bouras et al., 2026, *Nucleic Acids Research* 54:gkaf1448). Código abierto en `github.com/gbouras13/phold`.

## El problema

Los fagos son los virus más abundantes del planeta y los **más difíciles de anotar**. Evolucionan tan rápido que **más del 65 % de sus proteínas no se pueden anotar por homología de secuencia**: no hay con qué compararlas.

## Cómo lo resuelve

Combina exactamente las dos piezas de la clase:

1. **[[ProstT5]]** genera [[Embedding|embeddings]] de **1024 dimensiones por residuo** (encoder de 1000 millones de parámetros).
2. Una **CNN de dos capas** predice el token [[Alfabeto 3Di|3Di]] de cada residuo.
3. **[[Foldseek]]** busca esa "secuencia de forma" contra una base de **1,36 millones** de estructuras predichas.

## El resultado

Sobre **16.460 CDS** de fagos, porcentaje anotado:

| Método | % anotado |
|---|---|
| MMseqs2 (secuencia) | 34,7 % |
| PyHMMER (perfil HMM) | 37,7 % |
| **Phold** (estructura) | **49,4 %** |

Y con estructuras de ColabFold sube a **51,5 %**.

> **Lo que demuestra:** la forma **conserva señal que la secuencia ya perdió**. Los fagos con más anotación son justamente los de metabolismo de ácidos nucleicos y funciones enzimáticas.

Es el hallazgo de [[ESM-1b y ESM-2|ESM-1b]] —*la estructura está adentro de las representaciones*— **llevado a producción**: sin [[Alineamiento múltiple de secuencias|MSA]] y sin predecir coordenadas 3D, un PLM más un buscador de formas resuelve un problema real de anotación.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
