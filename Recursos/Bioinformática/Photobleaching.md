---
tags: [concepto, bioinformática, espacial, artefacto]
area: Bioinformática
aliases: [fotoblanqueo]
---

# Photobleaching (fotoblanqueo)

Degradación irreversible de los fluoróforos por la propia exposición a la luz de excitación. Es un artefacto de los [[Métodos basados en sondas]].

## Por qué es crítico en espacial

Estos métodos no toman una imagen: toman **muchas rondas** de hibridación e imagen sobre la misma muestra. Cada ronda expone el tejido a luz intensa.

```
Ronda 1: señal fuerte    ████████
Ronda 2:                 ██████
Ronda 3:                 ████
Ronda N: señal débil     ██
```

Como la identidad de cada gen se decodifica a partir del **patrón completo** de señales a lo largo de las rondas, perder intensidad en las últimas rondas no degrada un poco el resultado: puede hacer que el código se lea mal y el transcripto se asigne al gen equivocado, o se descarte.

## Consecuencias analíticas

- Sesgo sistemático contra los genes codificados en las rondas tardías.
- Necesidad de normalizar la intensidad ronda a ronda, lo que introduce sus propios supuestos.
- Límite práctico al número de rondas, y por lo tanto al tamaño del panel de genes.

## Mitigaciones

Fluoróforos más fotoestables, medios anti-fading, minimizar el tiempo de exposición, y esquemas de codificación robustos a la pérdida de señal en una ronda.

## Aparece junto con

[[Optical crowding]], [[Autofluorescencia]] y [[Stage drift]] — los cuatro problemas ópticos que enumera la clase.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
