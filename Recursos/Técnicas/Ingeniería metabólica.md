---
tags: [concepto, técnica, ingeniería-metabólica]
area: Técnicas
aliases: [metabolic engineering, ingeniería metabólica clásica]
---

# Ingeniería metabólica

Modificar el metabolismo de un organismo para que haga algo de interés industrial: producir un compuesto, consumir un sustrato, tolerar una condición.

## El enfoque clásico

> **De a una modificación a la vez: un gen → una enzima → una [[Vía metabólica|vía metabólica]].**

Se elige un paso de una vía conocida y se lo refuerza (sobreexpresión, introducción de una enzima heteróloga) o se lo corta ([[Knock-out y knock-in|knock-out]]).

### Limitaciones

| Limitación | Por qué ocurre |
|---|---|
| **Visión limitada de los efectos** | Una intervención local se propaga por toda la red: cofactores compartidos, metabolitos que alimentan varias vías |
| **Modificaciones clave pueden no ser consideradas** | Si el blanco relevante está lejos de la vía que se está mirando, nunca se lo propone |

La clase lo ilustra contrastando un esquema del metabolismo fermentativo central con el mapa global de [[KEGG]]: el enfoque clásico mira un rincón de esa maraña.

## Lo que la desbloqueó

| Frente | Aporte |
|---|---|
| [[Biología sintética]] | Varios genes a la vez, experimentos high throughput |
| Computacional | Ómicas ([[Integración de datos multiómicos]]), [[Modelo metabólico a escala genómica\|genome scale models]], [[Inteligencia Artificial\|IA]]/[[Machine Learning\|ML]] |

El resultado es la ingeniería metabólica **de sistemas**: razonar sobre la red completa con [[Diseño computacional de cepas|diseño computacional de cepas]], dentro del [[Ciclo DBTL]].

## La brecha pendiente

> **These type of methods do not reach the experimental metabolic engineers. There is a gap to bridge.**

Los métodos computacionales existen y funcionan, pero quienes hacen los experimentos no los usan. Interfaces como [[PECA]] buscan cerrar esa brecha.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Schneider et al 2022 - StrainDesign]] *(lectura)*
