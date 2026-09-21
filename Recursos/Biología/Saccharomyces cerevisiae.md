---
tags: [organismo, biología, levadura]
area: Biología
aliases: [S. cerevisiae, levadura, levadura de cerveza, yeast, saccharomyces]
---

# Saccharomyces cerevisiae

La levadura de panadería y cervecería, y el hospedero (*host*) del caso de estudio de la clase. Es uno de los organismos más usados en [[Ingeniería metabólica|ingeniería metabólica]] industrial: eucariota, fácil de cultivar, tolerante al etanol y con una caja de herramientas genéticas muy desarrollada.

## Su problema con los azúcares

| Azúcar | Comportamiento |
|---|---|
| **Glucosa** | Consumo preferente |
| **Xilosa, arabinosa** ([[Pentosas]]) | Lento, ineficiente o nulo |

De ahí toda la línea de trabajo que la clase repasa: [[Vías de asimilación de pentosas|vías heterólogas]], ingeniería de transportadores y [[Evolución adaptativa de laboratorio|evolución adaptativa]], y finalmente el [[Co-consumo de azúcares|co-consumo forzado]].

## Sus modelos metabólicos

| Modelo | Nota |
|---|---|
| [[Yeast9]] | El usado en el caso de estudio; los KO candidatos fueron **todos** sus genes nativos |
| **iMM904** | Modelo previo de *S. cerevisiae*, precargado en [[PECA]] |
| `yeast9_anaerobic_biggids.xml` | Variante anaeróbica de Yeast9, también precargada en PECA |

## Aeróbico vs anaeróbico

El caso de estudio corrió ambas condiciones. En aerobiosis se encontraron 729 diseños (332 con balance score > 5 %); en anaerobiosis, 158 diseños y **ninguno** supera el 5 %. La clase marca ese contraste como un desafío de relevancia industrial.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
