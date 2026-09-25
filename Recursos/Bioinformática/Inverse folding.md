---
tags: [concepto, bioinformática, diseño-de-proteínas]
area: Bioinformática
aliases: [plegamiento inverso, diseño de secuencias, protein design]
---

# Inverse folding

El problema **al revés** del plegamiento: dada una **forma** deseada, proponer **secuencias** que la adopten.

| Plegamiento | Inverse folding |
|---|---|
| secuencia → estructura | **estructura → secuencia** |
| [[AlphaFold]], [[ESMFold]] | [[ProstT5]] (`<fold2AA>`), [[ESM3]] |

Es la operación que convierte la predicción estructural en **diseño**: en vez de preguntar qué hace una proteína que existe, se pregunta qué secuencia habría que sintetizar para obtener una función que todavía no existe.

## Cómo lo hace ProstT5

Con el [[Alfabeto 3Di|3Di]] como lengua intermedia. El modelo se entrena a traducir en los dos sentidos entre secuencia de aminoácidos y secuencia de forma; el token `<fold2AA>` activa la dirección estructura → secuencia. La clase lo resume como **"diseño guiado por la forma, no por la secuencia"**.

## La versión generativa

[[ESM3]] lo lleva más lejos: como enmascara y rellena las tres modalidades a la vez, el diseño se puede **guiar dando parte de la secuencia, parte de la estructura, o una palabra de función**. El caso **esmGFP** es exactamente eso: se le dio solo la estructura de los residuos del núcleo de una GFP y el modelo generó el resto — una proteína fluorescente con 58 % de identidad y 96 mutaciones respecto de cualquier GFP natural.

Y un matiz de la figura de fidelidad al prompt: **promptear por estructura funciona muy bien**; SASA y palabras clave son pistas mucho más flojas.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Hayes et al 2025 - Simulating 500 million years of evolution]] *(lectura)*
- [[Heinzinger et al 2024 - ProstT5]] *(lectura)*
