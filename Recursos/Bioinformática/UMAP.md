---
tags: [concepto, bioinformática, análisis, visualización]
area: Bioinformática
aliases: [Uniform Manifold Approximation and Projection]
---

# UMAP

Método **no lineal** de [[Reducción dimensional]] usado para proyectar células a 2 dimensiones. Es la visualización canónica del [[scRNA-seq]]: la "nube de puntitos de colores" que aparece en prácticamente todos los papers del área.

## Cómo funciona (idea)

Construye un grafo de vecinos más cercanos en el espacio de componentes principales ([[PCA]]) y busca una disposición en 2D que preserve esa estructura de vecindad local.

## Qué sí y qué no se puede leer

| Se puede interpretar | **No** se puede interpretar |
|---|---|
| Qué células son vecinas | La **distancia** entre dos clusters |
| Que hay grupos separados | El **tamaño** relativo de los clusters |
| La estructura local | La disposición global / posición relativa |

> [!warning] El error más común
> Un UMAP es un espacio de **similitud transcriptómica**, no un mapa de nada físico. La clase de [[Biología espacial - mapeando la expresión génica a su entorno|biología espacial]] usa exactamente este punto como bisagra: dos células juntas en el UMAP pueden estar en extremos opuestos del órgano, y dos células vecinas en el tejido pueden caer en clusters distintos. El flujo `Tejido → disociación → células → scRNA-seq → UMAP` conserva la identidad y pierde la posición.

También es sensible a sus hiperparámetros (número de vecinos, distancia mínima): la misma matriz puede producir figuras bastante distintas.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
