---
tags: [técnica, single-cell]
area: Técnicas
aliases: [microgotas, droplet-based, microfluídica y microgotas]
---

# Microfluídica y microgotas

El método de [[Aislamiento de células individuales]] que hizo posible la escala actual del [[scRNA-seq]]. Un chip con canales de dimensiones micrométricas encapsula cada célula en una **gota de emulsión** junto con una perla (*bead*) que porta millones de copias del mismo [[Barcode celular]].

## El principio

```
célula  +  perla con barcode  +  reactivos  →  1 gota  →  lisis y RT dentro de la gota
```

Cada gota es un tubo de reacción independiente. Todo el ADNc que se genera dentro de una gota queda marcado con el mismo barcode, y por eso, tras romper la emulsión y secuenciar todo junto, se puede reconstruir de qué célula vino cada lectura.

## Características

- **Ventaja**: miles a decenas de miles de células por corrida, a costo por célula bajísimo.
- **Desventaja**: profundidad limitada por célula (20k–50k lecturas), cobertura sesgada al extremo 3' o 5' del transcripto, y **dobletes** cuando dos células entran en la misma gota.
- La carga sigue una distribución de Poisson: para mantener la tasa de dobletes baja, la mayoría de las gotas quedan vacías.

## Implementación de referencia

[[10x Genomics]] es la plataforma comercial dominante basada en este principio, y es la que la clase usa como ejemplo de workflow.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
