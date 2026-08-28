---
tags: [herramienta, plataforma, espacial]
area: Plataformas
---

# Visium

Plataforma de [[Transcriptómica espacial]] de [[10x Genomics]], dentro de la familia de [[Métodos basados en secuenciación]].

## Cómo funciona

El corte de tejido se coloca sobre un portaobjetos cubierto de **spots**, cada uno con oligos que llevan un [[Barcode espacial]] propio. Se permeabiliza el tejido, el ARN difunde hacia abajo y es capturado por los oligos del spot que tiene debajo. Después se hace retrotranscripción y secuenciación convencional.

```
spot ──► barcode espacial ──► coordenada (x, y) conocida
lectura ──► gen + barcode ──► "este gen se expresaba aquí"
```

## Características

- **Transcriptoma completo**, sin panel predefinido → habilita descubrimiento.
- **Resolución limitada**: cada spot tiene un diámetro de decenas de micras y agrupa **varias células**. La medición no es de una célula sino de un pequeño vecindario.
- Por eso Visium clásico requiere **deconvolución**: usar una referencia de [[scRNA-seq]] para estimar qué proporción de cada [[Tipo celular]] compone cada spot. Ver [[Integración de datos single cell y spatial]].

## Evolución

[[Visium HD]] es la generación siguiente: reemplaza la grilla de spots por una grilla continua mucho más fina y pasa a captura basada en sondas, acercándose a resolución de célula única sin perder cobertura del transcriptoma.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
