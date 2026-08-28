---
tags: [concepto, bioinformática, espacial, artefacto]
area: Bioinformática
aliases: [crosstalk, optical crowding/crosstalk, hacinamiento óptico]
---

# Optical crowding / crosstalk

Artefacto de los [[Métodos basados en sondas]]. Ocurre cuando hay **demasiadas señales fluorescentes en un mismo volumen óptico** como para resolverlas por separado.

## Qué ocurre

El microscopio tiene un límite de difracción: dos puntos más cercanos que ~200 nm se ven como uno solo. En una célula con miles de transcriptos de genes abundantes, muchas señales caen dentro de ese límite y se **fusionan**.

Consecuencias:

- Los genes abundantes se **subestiman** (varias moléculas se cuentan como una).
- Se generan **falsos positivos** por combinación accidental de colores en la codificación combinatoria.
- El *crosstalk* espectral entre fluoróforos cuyos espectros se superponen añade ambigüedad.

## Por qué limita el panel

Es una de las razones por las que estos métodos trabajan con paneles **dirigidos** de cientos a pocos miles de genes, y no con el transcriptoma completo: agregar más sondas satura ópticamente la muestra. Es exactamente el desafío que la clase resume como "cantidad de sondas utilizadas".

## Mitigaciones

- Codificación combinatoria con **corrección de errores** (MERFISH, [[Vizgen]]).
- Diluir la señal repartiendo los genes entre más rondas de hibridación, a costa de más tiempo y más [[Photobleaching]].
- Expansión física del tejido (*expansion microscopy*) para separar las moléculas.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
