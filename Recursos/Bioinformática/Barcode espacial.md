---
tags: [concepto, bioinformática, espacial]
area: Bioinformática
aliases: [barcodes espaciales, spatial barcode]
---

# Barcode espacial

La misma idea que el [[Barcode celular]], pero la etiqueta no codifica **de qué célula** viene una molécula sino **de qué posición** del portaobjetos.

## Cómo funciona

La superficie de captura se fabrica de modo que cada spot (o cada cuadrado de la grilla, en [[Visium HD]]) tenga oligos con una secuencia única y **conocida de antemano**. Al secuenciar, el barcode se traduce en coordenadas:

```
lectura = [barcode espacial] + [UMI] + [ADNc]
              ↓ tabla de decodificación
          (x, y) en el tejido
```

La reconstrucción espacial es por lo tanto **computacional**, no óptica: nunca se "ve" dónde estaba la molécula, se lo deduce del barcode. Ésa es la diferencia de fondo con los [[Métodos basados en sondas]], donde la posición se mide directamente por imagen.

## Su punto débil

Si el ARN se desplaza antes de ser capturado, el barcode registra una posición incorrecta. Ése es el fenómeno de [[Lateral diffusion]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
