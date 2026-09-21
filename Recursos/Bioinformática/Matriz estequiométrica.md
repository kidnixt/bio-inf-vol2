---
tags: [concepto, bioinformática, modelado]
area: Bioinformática
aliases: [matriz S, S, stoichiometric matrix, modelo estequiométrico, stoichiometric model]
---

# Matriz estequiométrica

La representación matemática de una red metabólica: **una fila por metabolito, una columna por reacción**. Cada entrada es el coeficiente estequiométrico del metabolito en esa reacción.

| Signo | Significado |
|---|---|
| **Negativo** | El metabolito se **consume** (sustrato) |
| **Positivo** | El metabolito se **produce** (producto) |
| **0** | No participa |

## El ejemplo de la clase

Para las reacciones `R1: A + B → C`, `R2: C + D → E + F`, `R3: E + G → 2H`:

| | R1 | R2 | R3 |
|---|---|---|---|
| A | −1 | 0 | 0 |
| B | −1 | 0 | 0 |
| C | +1 | −1 | 0 |
| D | 0 | −1 | 0 |
| E | 0 | +1 | −1 |
| F | 0 | +1 | 0 |
| G | 0 | 0 | −1 |
| H | 0 | 0 | **+2** |

C es producido por R1 y consumido por R2; H tiene coeficiente 2 porque R3 produce dos moléculas.

## La ecuación

Junto con el vector de flujos **v** (la velocidad de cada reacción), la dinámica de las concentraciones es:

```
dc/dt = S · v
```

En [[Modelado basado en restricciones|estado estacionario]] se exige `S · v = 0`: ningún metabolito interno se acumula ni se agota. Ese sistema lineal, con más reacciones que metabolitos, tiene infinitas soluciones; los límites en los flujos lo acotan al [[Espacio de flujos factible]].

La matriz es la forma concreta que toma un [[Modelo metabólico a escala genómica]]: en iML1515, por ejemplo, es de 1877 × 2712.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] *(lectura)*
