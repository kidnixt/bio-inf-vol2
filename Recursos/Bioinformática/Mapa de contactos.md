---
tags: [concepto, bioinformática, estructura]
area: Bioinformática
aliases: [contact map, contactos, mapa de contactos, predicción de contactos]
---

# Mapa de contactos

Matriz que indica, para cada par de residuos de una proteína, si están **en contacto en el espacio** (típicamente, a menos de ~8 Å). Es una representación intermedia entre la secuencia (1D) y la estructura (3D): más fácil de predecir que las coordenadas, y suficiente para reconstruirlas aproximadamente.

Su diagonal es trivial (residuos vecinos en la cadena siempre están cerca); **lo informativo son los contactos lejanos de la diagonal**: posiciones separadas por decenas o cientos de residuos que el plegamiento pone juntas.

## Por qué es el experimento clave de ESM-1b

El hallazgo de [[ESM-1b y ESM-2|ESM-1b]] (Rives et al., 2021) se demuestra justamente con un mapa de contactos: se recupera de las representaciones del modelo y compite con **CCMpred**, el método clásico basado en covariación en un [[Alineamiento múltiple de secuencias|MSA]].

La figura de la clase lo muestra en una sola matriz: debajo de la diagonal, ESM-1b; arriba, CCMpred. Azul son aciertos, rojo falsos positivos, gris el mapa real.

> [!note] Hace falta una sonda
> La información **está** en las representaciones, pero para leerla hace falta una **sonda entrenada** —una proyección lineal o un clasificador chico—. **Nadie le pasó un solo contacto durante el entrenamiento**: los aprendió de rellenar máscaras ([[Masked language modeling]]).

Ese patrón —*[[Embedding|embeddings]] congelados + un clasificador simple*— es el mismo del caso de localización subcelular de Juan Diego Puglia, y una de las ideas transversales de la clase: **el conocimiento está en el vector; extraerlo es barato**.

La conexión mecánica: la atención de un residuo apunta a residuos **lejanos en la secuencia pero cercanos en el espacio**, que es exactamente lo que el [[Transformer]] sabe representar.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
