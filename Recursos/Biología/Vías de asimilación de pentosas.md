---
tags: [concepto, biología, metabolismo, ingeniería-metabólica]
area: Biología
aliases: [vía de Weimberg, Weimberg pathway, vía de la isomerasa bacteriana, bacterial isomerase pathway, vías heterólogas de pentosas, asimilación de pentosas]
---

# Vías de asimilación de pentosas

Las rutas que hay que **introducir** ([[Knock-out y knock-in|knock-in]]) para que una levadura metabolice [[Pentosas|pentosas]]. En el caso de estudio los candidatos eran 13 reacciones heterólogas de metabolismo de xilosa y arabinosa; el diseño seleccionado usa dos rutas completas.

## Arabinosa → vía de la isomerasa bacteriana

| Paso | Enzima (KI) | Producto |
|---|---|---|
| 1 | **ARAI** (arabinosa isomerasa) | L-ribulosa |
| 2 | **RBK_L1** (ribuloquinasa) | L-ribulosa-5-P |
| 3 | **RBP4E** (ribulosa-5-P 4-epimerasa) | **D-xilulosa-5-P** |

Desemboca en la [[Vía de las pentosas fosfato]].

## Xilosa → vía de Weimberg

Ruta **oxidativa**, sin fosforilación, que lleva la xilosa directo al ciclo de Krebs:

| Paso | Enzima (KI) | Producto |
|---|---|---|
| 1 | **XYLOR** | D-xilonolactona |
| 2 | **XYLLN** | D-xilonato |
| 3 | **DXYLTD** | 2-ceto-3-desoxi-D-xilonato |
| 4 | **2D3DDAD** | α-cetoglutarato semialdehído |
| 5 | **2OGSAD** | **α-cetoglutarato** |

Lo característico es que **no pasa por la vía de las pentosas fosfato**. Eso es justamente lo que el diseño quiere: el KO de **XYLTD_D** cierra la ruta alternativa (xilosa → xilitol → D-xilulosa-5-P), de modo que la xilosa solo pueda ir por Weimberg y aporte α-cetoglutarato, mientras la arabinosa se queda con la PPP.

## Por qué esto produce complementariedad

Al forzar que cada azúcar entre por una puerta distinta, los productos de cada uno dejan de ser intercambiables:

> **Los precursores y los [[Cofactores energéticos|transportadores de energía cargados]] que produce un azúcar no pueden ser reemplazados por completo por los otros.**

Ver [[Co-consumo de azúcares]].

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
