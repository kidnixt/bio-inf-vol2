---
tags: [concepto, bioinformática, espacial, artefacto]
area: Bioinformática
aliases: [autofluorescence]
---

# Autofluorescencia

Emisión de fluorescencia por parte de moléculas **propias del tejido**, sin ninguna sonda de por medio. Es señal de fondo que se suma a la señal real en los [[Métodos basados en sondas]].

## Fuentes típicas

- **Lipofuscina**: pigmento que se acumula con la edad en neuronas y otras células post-mitóticas. Emite en un rango amplio del espectro y es especialmente problemática en cerebro humano añejo — justo el tejido de interés en estudios de neurodegeneración.
- **Colágeno y elastina** en tejido conectivo.
- **Flavinas y NADH** del metabolismo celular.
- **Glóbulos rojos** y restos de fijación con formaldehído.

## Por qué es un problema

Reduce la relación señal/ruido y puede generar **falsos positivos**: un punto de autofluorescencia se confunde con un transcripto detectado. Como la codificación combinatoria depende de leer correctamente la presencia o ausencia de señal en cada ronda, un fondo alto corrompe la decodificación.

Su intensidad varía **entre regiones del mismo tejido**, así que introduce un sesgo espacial: la tasa de falsos positivos no es uniforme sobre el corte, lo que puede simular [[Spatial domains]] que no existen.

## Mitigaciones

Tratamientos de quenching químico, imágenes de control sin sondas para sustraer el fondo, y elección de fluoróforos que emitan lejos del rango autofluorescente.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
