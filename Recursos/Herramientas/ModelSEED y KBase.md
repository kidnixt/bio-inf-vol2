---
tags: [herramienta, plataforma, modelado]
area: Herramientas
aliases: [ModelSEED, KBase, reconstrucción automática de modelos, reconstrucción de GEMs]
---

# ModelSEED y KBase

Plataformas que **automatizan la reconstrucción** de un [[Modelo metabólico a escala genómica]] a partir de un genoma anotado. Aparecen en la diapositiva que responde *"¿de dónde sale un GEM?"*, junto a [[KEGG]].

## El flujo que automatizan

```
Secuencia de ADN → genoma anotado → red metabólica → modelo estequiométrico
```

A partir de las funciones enzimáticas anotadas, proponen el conjunto de reacciones correspondiente, asignan compartimentos, agregan reacciones de transporte e intercambio y una [[Reacción de biomasa]], y hacen *gap-filling*: completar los huecos que impedirían que el modelo crezca.

| Plataforma | Perfil |
|---|---|
| **ModelSEED** | Pipeline de reconstrucción y gap-filling a partir de genomas anotados |
| **KBase** | Plataforma de análisis de sistemas biológicos que integra anotación, reconstrucción y simulación en un mismo entorno |

## La advertencia implícita

Una reconstrucción automática es un **borrador**. El gap-filling agrega reacciones que hacen crecer al modelo pero que pueden no existir en el organismo real, y una anotación errónea se propaga a todo el análisis. Por eso los modelos de referencia ([[BiGG Models|iML1515]], [[Yeast9]]) son curados manualmente durante años, y por eso existe una herramienta de validación como Memote.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
