---
tags: [concepto, biología, metabolismo]
area: Biología
aliases: [PPP, pentose phosphate pathway, pentosas fosfato, ruta de las pentosas fosfato]
---

# Vía de las pentosas fosfato

Vía que corre en paralelo a la [[Glucólisis]] y cumple tres funciones: generar **NADPH** (rama oxidativa), producir **ribosa-5-fosfato** para nucleótidos, y interconvertir azúcares de 3 a 7 carbonos (rama no oxidativa: transcetolasas TKT1/TKT2 y transaldolasa TALA).

## Por qué es central en el caso de co-consumo

Es el punto de encuentro natural de las [[Pentosas|pentosas]] con el metabolismo central: tanto la xilosa (vía xilitol → D-xilulosa-5-P) como la arabinosa (vía L-ribulosa → L-ribulosa-5-P → D-xilulosa-5-P) entran por acá.

El diseño seleccionado aprovecha eso para repartir roles:

- **Arabinosa** entra a la PPP por D-xilulosa-5-P (KIs ARAI, RBK_L1, RBP4E) y desde ahí alimenta ribosa-5-P → PRPP → adenosina, y eritrosa-4-P → corismato → **aminoácidos aromáticos** (tirosina, fenilalanina, triptófano, tirosol).
- **Xilosa** queda excluida de la PPP: el KO de **XYLTD_D** bloquea la ruta xilitol → D-xilulosa-5-P, y la xilosa tiene que ir por la [[Vías de asimilación de pentosas|vía de Weimberg]].

## Enzimas de la PPP en el paisaje de soluciones

Aparecen con frecuencia como KO en los diseños muestreados: **RPE** (ribulosa-5-P epimerasa), **GND**, **PGL**, **G6PDH2r**. RPE es la segunda mitad de la lógica *pgi1Δ rpe1Δ* de Papapetridis et al. (2018): sin RPE, la ribulosa-5-P no entra a la rama no oxidativa.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
