---
tags: [concepto, bioinformática, espacial, desafío]
area: Bioinformática
aliases: [cell segmentation, segmentación]
---

# Segmentación celular

Decidir **qué píxeles y qué transcriptos pertenecen a qué célula** en un experimento de [[Transcriptómica espacial]]. Es el paso más determinante y más frágil de todo el pipeline espacial.

## Por qué hace falta

Las plataformas espaciales no devuelven células: devuelven **transcriptos con coordenadas** (métodos de imagen como [[CosMx SMI]]) o **bins de una grilla** (métodos de captura como [[Visium HD]]). Las fronteras celulares hay que reconstruirlas.

```
transcriptos con (x, y)  +  imagen (DAPI, membranas)
            ↓ segmentación
      "esta célula contiene estos transcriptos"
            ↓
      matriz genes × células → recién ahí empieza el pipeline conocido
```

## Por qué es difícil

- Las tinciones nucleares (DAPI) marcan el núcleo, no la célula. Extrapolar el citoplasma a partir del núcleo es una aproximación grosera, y falla con células muy ramificadas como [[Neurona|neuronas]] y [[Astrocito|astrocitos]].
- Los tejidos son tridimensionales y el corte es una rebanada: células superpuestas en Z se ven fusionadas en la imagen.
- La densidad celular varía enormemente entre regiones del tejido.

## Por qué importa tanto

Un error de segmentación **no se corrige aguas abajo**: se propaga a la [[Matriz de conteo]], a la [[Anotación de tipos celulares]], al [[Clustering]] y a cualquier conclusión sobre [[Neighborhoods]] o [[Spatial niches]].

El artefacto más traicionero es la **contaminación cruzada**: transcriptos asignados a la célula equivocada generan perfiles híbridos que se interpretan como "tipos celulares nuevos" o como evidencia de comunicación entre células vecinas. Un vecindario espurio y un vecindario real se ven igual en los datos.

## Estado del arte

Es un problema de visión por computadora, abordado con modelos de [[Deep Learning]] (Cellpose, Baysor, y otros que combinan imagen con la distribución espacial de los transcriptos).

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
