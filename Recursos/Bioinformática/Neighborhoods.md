---
tags: [concepto, bioinformática, espacial, análisis]
area: Bioinformática
aliases: [vecindarios celulares, cellular neighborhoods]
---

# Neighborhoods (vecindarios)

Qué [[Tipo celular|tipos celulares]] aparecen **sistemáticamente juntos** en el tejido. El análisis se hace sobre la composición local: para cada célula, qué hay en su entorno inmediato.

## Cómo se analiza

```
para cada célula:
    mirar sus k vecinos más cercanos (o un radio fijo)
    contar la composición de tipos celulares
        ↓
agrupar células por composición de vecindario
        ↓
"vecindario tipo A: 60% neuronas, 20% astrocitos, 20% microglía"
```

También se hacen tests de **co-ocurrencia**: ¿el tipo X aparece cerca del tipo Y más de lo esperable si las células estuvieran distribuidas al azar?

## Qué revela

Relaciones funcionales que la composición global no muestra. Dos tejidos pueden tener exactamente la misma proporción de tipos celulares y organizaciones completamente distintas. La composición es un histograma; el vecindario es una estructura.

## La advertencia metodológica

Todo análisis de vecindarios depende críticamente de la [[Segmentación celular]]. Si los transcriptos se asignan a la célula equivocada, aparecen perfiles híbridos que se leen como células vecinas "comunicándose" — y un vecindario espurio se ve igual que uno real. Lo mismo vale para la [[Lateral diffusion]] en plataformas de captura.

## Relacionado

[[Spatial domains]] (escala mayor, regiones), [[Spatial niches]] (vecindario con función).

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
