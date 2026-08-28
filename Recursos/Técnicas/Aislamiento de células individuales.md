---
tags: [técnica, single-cell]
area: Técnicas
---

# Aislamiento de células individuales

El primer requisito físico del [[scRNA-seq]]: separar las células de un tejido para poder hacer **reacciones de biología molecular en compartimentos individuales**.

## Métodos de primera generación

Precisos pero **poco automatizados y poco eficientes**; requieren mucho tiempo para aislar grandes números de células:

- [[Dilución al límite]]
- [[Micromanipulación]]
- [[Microdisección por captura láser]]

## Métodos de alto rendimiento

Los que hicieron viable la escala actual (miles a millones de células):

- [[Citometría de flujo]] (*cell sorting*)
- [[Microfluídica]] y microgotas

## El costo oculto

Toda disociación es **destructiva**: rompe la estructura del tejido y elimina la [[Transcriptómica espacial|información espacial]] — posición, arquitectura, vecinos, relaciones espaciales. Además introduce sesgos: las células frágiles (como las [[Neurona|neuronas]] adultas) se pierden preferentemente, y el estrés de la disociación induce genes de respuesta inmediata que contaminan la señal biológica.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
