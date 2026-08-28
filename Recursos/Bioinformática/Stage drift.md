---
tags: [concepto, bioinformática, espacial, artefacto]
area: Bioinformática
aliases: [deriva de la platina, drift]
---

# Stage drift (deriva de la platina)

Desplazamiento mecánico de la muestra entre rondas sucesivas de imagen en los [[Métodos basados en sondas]]. Causas: dilatación térmica, vibración, imprecisión del motor de la platina, o el propio manipuleo entre ciclos de hibridación.

## Por qué es grave aquí y no en microscopía normal

Porque la identidad de cada transcripto se decodifica combinando la señal del **mismo punto físico** a lo largo de muchas rondas.

```
Ronda 1: punto en (100, 200)
Ronda 2: punto en (100, 200)  ← ¿es la misma molécula, o el campo se corrió 1 µm?
```

Si las imágenes no se alinean con precisión sub-micrométrica, se combinan señales de moléculas distintas y el código resultante es basura. Con transcriptos separados por menos de 1 µm, una deriva pequeña arruina la decodificación.

## Mitigaciones

- **Fiduciales**: microesferas fluorescentes fijas en la muestra que sirven de referencia para el registro de imágenes.
- Registro computacional entre rondas antes de decodificar.
- Control térmico y sistemas de autofocus.

## Aparece junto con

[[Optical crowding]], [[Photobleaching]] y [[Autofluorescencia]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
