---
tags: [técnica, single-cell]
area: Técnicas
aliases: [cell sorting, FACS, citometría]
---

# Citometría de flujo (cell sorting)

Método de alto rendimiento de [[Aislamiento de células individuales]]. Las células, en suspensión y marcadas con anticuerpos fluorescentes, pasan de a una por un haz láser; se mide su fluorescencia y dispersión de luz, y un sistema de deflexión electrostática las desvía a un tubo o a un pocillo según el criterio elegido (FACS: *fluorescence-activated cell sorting*).

## Características

- **Ventaja**: permite **seleccionar** poblaciones específicas antes de secuenciar. Si interesa una población rara, se la enriquece en lugar de secuenciar millones de células para encontrarla.
- **Ventaja**: puede depositar exactamente una célula por pocillo de una placa de 96 o 384, lo que la hace compatible con protocolos de placa tipo Smart-seq (mayor profundidad por célula, menos células).
- **Desventaja**: requiere marcadores de superficie conocidos, la célula sufre estrés mecánico, y el throughput es menor que el de la [[Microfluídica]].

Combinada con secuenciación profunda por célula, es la vía "pocas células, mucha información". La microfluídica es la vía opuesta: "muchas células, poca profundidad".

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
