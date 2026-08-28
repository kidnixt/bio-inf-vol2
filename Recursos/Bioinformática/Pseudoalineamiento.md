---
tags: [concepto, bioinformática]
area: Bioinformática
aliases: [pseudo-alineamiento, pseudoalignment, mapeo ligero]
---

# Pseudoalineamiento

La respuesta al tercer desafío del [[scRNA-seq]]. En lugar de calcular dónde alinea exactamente cada lectura, se determina **con qué transcriptos es compatible**.

## Principio

- **Alineamiento directo al [[Transcriptoma]]**, no al genoma. Esto elimina de raíz el problema de los sitios de unión exón–exón.
- **No se buscan coordenadas exactas, sino compatibilidad.** Se descompone la lectura en k-mers, se consulta un índice y se obtiene el conjunto de transcriptos consistentes con todos ellos.

```
Alineamiento clásico:   "esta lectura mapea en chr7:5.527.151-5.527.250, con 1 mismatch"
Pseudoalineamiento:     "esta lectura es compatible con ACTB"
```

## Por qué funciona

Porque el producto que se quiere es una [[Matriz de conteo]] de genes × células. La posición dentro del gen nunca se usa. Se descarta información que de todos modos se iba a descartar.

## El beneficio

Órdenes de magnitud en tiempo y memoria. La clase muestra un benchmark: **20 sets de datos de 30 millones de lecturas, con 20 cores** — un trabajo de horas o días con alineadores clásicos que pasa a resolverse en minutos.

Herramientas típicas de esta familia: kallisto|bustools y salmon/alevin.

## Sus límites

No sirve cuando hace falta la posición: detección de variantes, análisis de splicing, RNA velocity. Ver [[Alineamiento de secuencias]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
