---
tags: [concepto, bioinformática, espacial, desafío]
area: Bioinformática
aliases: [deconvolución espacial, integración spatial, label transfer]
---

# Integración de datos single cell y spatial

Combinar dos tipos de datos con fortalezas complementarias y debilidades opuestas.

| | [[scRNA-seq]] | [[Transcriptómica espacial]] |
|---|---|---|
| Transcriptoma | Completo y profundo | Panel limitado o menos profundo |
| Resolución | Célula única real | Spot, bin o célula segmentada |
| Posición | **Ninguna** | Conocida |

La idea es usar el scRNA-seq como **referencia** —qué tipos celulares existen y cuál es su perfil— y aplicarlo sobre los datos espaciales.

## Las dos tareas

### Deconvolución

Para plataformas cuya unidad contiene varias células ([[Visium]], [[ROI|ROIs]] de [[GeoMx DSP]]): estimar **qué proporción de cada [[Tipo celular]]** compone cada spot.

```
spot = 0.4 × neurona + 0.3 × astrocito + 0.2 × microglía + 0.1 × endotelial
```

### Label transfer / mapeo

Para plataformas de célula única ([[CosMx SMI]], [[Visium HD]]): asignar a cada célula segmentada la etiqueta del tipo celular más compatible con la referencia. Es [[Anotación de tipos celulares]] con una referencia externa.

## Los supuestos que hay que vigilar

- Que la referencia **contenga** todos los tipos presentes en el tejido espacial. Un tipo ausente en la referencia se asigna al más parecido y desaparece.
- Que ambos datasets provengan de tejido comparable (misma especie, región, condición, edad).
- Que no haya un [[Batch effect]] entre plataformas que domine la señal biológica.
- Que la [[Segmentación celular]] sea buena: perfiles híbridos por mala segmentación se anotan mal por definición.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
