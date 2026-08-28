---
tags: [concepto, células, ejemplo]
area: Neurobiología
---

# Tejido cerebral

El ejemplo que usa la clase para ilustrar la [[Heterogeneidad celular]], por su escala y por lo fina que es su clasificación celular.

## Escala

| | Número aproximado de células |
|---|---|
| Cerebro de ratón | ~110 millones |
| Cerebro humano | ~170 mil millones |

## Los 4 grandes tipos celulares

| Clase general | Subclases |
|---|---|
| **[[Neurona\|Neuronas]]** | Excitatorias, inhibitorias |
| **[[Macroglía\|Macroglías]]** (soporte y mantenimiento) | [[Astrocito\|Astrocitos]], [[Oligodendrocito\|oligodendrocitos]], progenitores de oligodendrocitos |
| **[[Microglía\|Microglías]]** (sistema inmune) | Homeostática, reactiva |
| **Células sanguíneas / vasculares** | [[Célula endotelial\|Endoteliales]], musculares |

Y la jerarquía completa que se despliega al aumentar la resolución:

```
[Clase General]  (4)  ➜  [Subclase]  (docenas)  ➜  [Clúster / Tipo Celular]  (>3000)
```

## Por qué es el ejemplo elegido

Porque hace evidentes las dos limitaciones que la clase quiere atacar:

- El [[Bulk RNA-seq]] de un corte de cerebro promedia neuronas y glía juntas — y la glía es mayoritaria, así que domina la señal.
- Regiones vecinas (corteza vs hipocampo) tienen arquitecturas radicalmente distintas, y esa diferencia se pierde tanto en el bulk como en el [[scRNA-seq]] tras la disociación. Eso motiva la [[Transcriptómica espacial]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
