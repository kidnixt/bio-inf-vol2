---
tags: [herramienta, plataforma, espacial]
area: Plataformas
aliases: [GeoMx, Digital Spatial Profiler, GeoMx Digital Spatial Profiler]
---

# GeoMx DSP (Digital Spatial Profiler)

Plataforma de [[Transcriptómica espacial]] de [[Nanostring]]. Su lógica no es "célula por célula" sino **región por región**: el usuario selecciona [[ROI|regiones de interés]] sobre la imagen del tejido y la plataforma perfila cada una.

## Cómo funciona

Se hibridan sondas con un oligo de código de barras unido por un **linker fotoescindible**. Al iluminar una [[ROI]] con luz UV, sólo los códigos de esa región se liberan; se aspiran, se colectan en un pocillo y se cuantifican. La posición queda codificada por **qué región se iluminó**, no por dónde estaba la molécula.

```
Tejido + sondas  →  seleccionar ROI  →  UV  →  liberar barcodes  →  aspirar  →  contar
```

## Especificaciones (según la clase)

| | |
|---|---|
| **Sensibilidad** | Hasta **1200 proteínas**, o **[[Transcriptoma]] completo** |
| **[[ROI]]** | Entre **50 y 600 µm** de diámetro |
| **Células por ROI** | Entre **50 y 500** |

## Su lugar en el trade-off

| # Genes | Resolución espacial | Throughput |
|---|---|---|
| Alto a completo | **Baja – regional (ROI)** | Alto |

Es la plataforma correcta cuando la pregunta es *"¿en qué se diferencian estas dos zonas del tejido?"* — comparar tumor vs estroma, capa vs capa, lesión vs tejido sano. No lo es cuando la pregunta es *"¿qué hace cada célula?"*; para eso está el [[CosMx SMI]].

Conceptualmente, es la versión automatizada y escalada de la [[Microdisección por captura láser]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
