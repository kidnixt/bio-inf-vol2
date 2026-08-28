---
tags: [técnica, single-cell]
area: Técnicas
---

# Dilución al límite

Método clásico de [[Aislamiento de células individuales]]: se diluye la suspensión celular hasta que, estadísticamente, cada pocillo de una placa reciba **una sola célula**.

## Características

- **Ventaja**: simple, no requiere instrumental especializado.
- **Desventaja**: es probabilístico, no determinista. Siguiendo una distribución de Poisson, muchos pocillos quedan vacíos y algunos reciben dos o más células (**dobletes**). Se suele diluir a menos de 1 célula por pocillo en promedio para minimizar dobletes, lo que desperdicia la mayoría de los pocillos.
- **Escala**: decenas a cientos de células. Inviable para los miles o millones que requiere el [[scRNA-seq]] moderno.

Es una de las técnicas que la clase agrupa como **poco automatizadas y poco eficientes**, junto con la [[Micromanipulación]] y la [[Microdisección por captura láser]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
