---
tags: [concepto, bioinformática, estructura, IA]
area: Bioinformática
aliases: [co-plegado, co-folding, Boltz-1, Boltz-1x, NeuralPLexer, RoseTTAFold All-Atom]
---

# Cofolding

Predecir **el complejo entero de una sola vez** —proteína más ligando, ácido nucleico o ion— en lugar de predecir la proteína y después dockear el ligando encima.

```
secuencias y componentes → modelo conjunto → complejo 3D
```

## Los modelos

| Modelo | Origen |
|---|---|
| **[[AlphaFold\|AlphaFold3]]** | Google DeepMind (Abramson et al., 2024) |
| **Boltz-1 / Boltz-1x** | Abierto |
| **NeuralPLexer** | — |
| **RoseTTAFold All-Atom** | Krishna et al., 2024 |

La figura de la clase superpone predicciones de Boltz-1x sobre estructuras de rayos X: coinciden estrechamente, incluida la pose del ligando.

## Por qué es distinto del docking

El [[Docking molecular|docking]] clásico asume una estructura del receptor **dada** y busca dónde encaja el ligando. El cofolding **construye las dos cosas juntas**, así que puede representar el ajuste mutuo —el *induced fit*— sin tener que tratarlo como un caso especial caro.

Su límite es el mismo de toda la familia: predice bien **geometría**, no **[[Energía libre de unión|afinidad]]**. *"La afinidad todavía es difícil"* sigue siendo la precaución que la clase le pone a AlphaFold3.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
