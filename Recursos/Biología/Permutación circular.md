---
tags: [concepto, biología, proteínas, evolución]
area: Biología
aliases: [permutación circular, circular permutation, permutaciones circulares]
---

# Permutación circular

Reordenamiento en el que una proteína conserva **las mismas letras en otro orden**: se corta la cadena en un punto interno, y lo que estaba al final pasa al principio.

```
MKVAG  →  AGMKV
```

## Cuándo es inocua

> **Solo es inocua si los extremos N y C ya estaban *juntos en el espacio*.**

Si en la estructura plegada el extremo amino y el carboxilo están próximos, unirlos y abrir la cadena en otro lado produce **la misma forma** con una secuencia distinta. Si no lo estaban, la permutación rompe la topología y la proteína no se pliega.

Ocurre naturalmente en varias familias de proteínas, y se usa deliberadamente en ingeniería de proteínas — los biosensores fluorescentes basados en GFP circularmente permutada son el ejemplo más conocido.

## Por qué está en la clase

Es la segunda de las **tres ediciones al texto** (junto a la mutación puntual y la [[Homología|homología]]), y aporta el caso más incómodo para un modelo ingenuo: **la composición no cambia en absoluto** —los mismos aminoácidos, las mismas frecuencias, los mismos [[K-mer|k-meros]] salvo en el punto de corte— y sin embargo el resultado puede ser una proteína funcional o una que no se pliega, según la geometría de los extremos.

Ningún modelo que cuente letras o k-meros puede decidir eso. Hace falta **contexto y estructura**: exactamente lo que distingue a [[ProtVec]] de todo lo que vino después.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
