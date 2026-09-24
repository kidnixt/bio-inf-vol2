---
tags: [herramienta, modelo, estructura, IA]
area: Herramientas
aliases: [ESM Fold]
---

# ESMFold

Predictor de estructura construido sobre [[ESM-1b y ESM-2|ESM-2]] (Lin et al., 2023, *Science* 379:1123–1130). Su rasgo distintivo: **no necesita [[Alineamiento múltiple de secuencias|MSA]]**.

## La arquitectura

```
secuencia → ESM-2 (preentrenado con máscaras)
          → Folding Trunk (48 bloques)
          → Structure Module (8 bloques)
          → estructura + confianza
              ↑__________ recycling __________|
```

El ***recycling*** vuelve a pasar el resultado por la red: **el modelo se refina sobre su propio borrador**.

## Frente a AlphaFold 2

| | [[AlphaFold]] 2 | ESMFold |
|---|---|---|
| ¿Necesita MSA? | **Sí** | **No** |
| Velocidad | Lento | **Muy rápido** (14,2 s para 384 residuos en una V100) |
| De dónde sale la señal | De los **homólogos** | Del **[[Modelo de lenguaje de proteínas\|PLM]]** |

Predicen casi lo mismo **sin que ESMFold vea alineamientos**. Y contra estructuras del [[PDB]], ESMFold acierta una proteína **metagenómica que no se parecía a nada conocido** — el caso donde un MSA no tendría de dónde sacar señal.

## Por qué importa la velocidad

Porque habilita la escala: sin el costo de construir un MSA por secuencia, se puede predecir **el catálogo entero** de lo secuenciado. Eso es el [[ESM Atlas]]: 600+ millones de estructuras metagenómicas en 2 semanas.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
