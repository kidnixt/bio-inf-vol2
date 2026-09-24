---
tags: [concepto, bioinformática, IA, machine-learning]
area: Bioinformática
aliases: [active learning, AL, aprendizaje activo]
---

# Aprendizaje activo

> El **Aprendizaje Activo (AL)** es un proceso dinámico e iterativo de retroalimentación que identifica y selecciona de manera eficiente **los datos más valiosos** dentro del espacio químico para ser etiquetados o evaluados.

Es la forma explícita del ciclo que la clase resume como ***AI-driven drug design***:

```
Datos → Modelo → Candidatos → Ensayo
   ↑_______________________________|
   la medición actualiza el modelo
```

> **IA-driven no significa "IA sola": significa un ciclo de decisión guiado por aprendizaje.**

## El ciclo

1. Entrenar el modelo con los datos etiquetados disponibles.
2. Predecir sobre el pool **no etiquetado**, con su probabilidad/incertidumbre.
3. **Seleccionar k candidatos** — no los mejores, sino los **más informativos**.
4. Medirlos experimentalmente.
5. Agregarlos al conjunto y repetir.

Las preguntas de diseño que plantea la clase: qué representación usar (para fármacos y para células), qué arquitectura de modelo, **cómo elegir los pares** y cuál es el **impacto de k**.

## Por qué cambia las cosas

El [[Diseño de fármacos asistido por computadora|CADD]] convencional selecciona compuestos **manualmente, en rondas sucesivas**, y tiende a elegir los de mejor score — que son los que el modelo ya entiende. El AL elige los que **más reducen la incertidumbre**, que suelen estar en zonas mal cubiertas del espacio químico. Es la diferencia entre *explotar* y *explorar*.

## Aplicaciones en descubrimiento de fármacos

| Área | Qué aporta |
|---|---|
| Predicción de interacción compuesto–blanco | Aborda el **desbalance** del conjunto etiquetado; facilita explorar el espacio CTI |
| [[Virtual screening]] | Ayuda al LBVS a descubrir ***scaffolds* nuevos** (*scaffold hopping*); mejora la eficiencia y precisión del SBVS |
| Generación y optimización de moléculas | Mejora la calidad de las moléculas generadas; acelera la evaluación de propiedades |
| Predicción de propiedades | Aborda las limitaciones de los conjuntos etiquetados |

Es la etapa "selección experimental" de la tabla de [[Inteligencia Artificial|dónde interviene la IA en el CADD]], y la más directamente conectada con el laboratorio: el modelo **decide qué experimento hacer**.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
