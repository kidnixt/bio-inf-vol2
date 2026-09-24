---
tags: [concepto, técnica, estructura]
area: Bioinformática
aliases: [rayos X, difracción de rayos X, RMN, Cryo-EM, criomicroscopía electrónica, métodos estructurales experimentales]
---

# Cristalografía de rayos X

*(y los otros métodos experimentales de determinación estructural)*

Las tres vías experimentales para obtener la estructura 3D de una proteína, que alimentan el [[PDB]] y habilitan el [[Diseño basado en estructura|SBDD]]:

| Método | Cómo funciona | Qué permite |
|---|---|---|
| **Cristalografía de rayos X** | Difracción de un haz de rayos X por un **cristal** de proteína | Estructuras de **alta resolución** |
| **Espectroscopía de RMN** | Campos magnéticos sobre la proteína **en solución** | Estructuras en solución, y dinámica |
| **Cryo-EM** (criomicroscopía electrónica) | Microscopía electrónica sobre muestras vitrificadas | Estructuras a nivel nanométrico **sin cristalizar** |

## Los compromisos

- La **cristalografía** da la mejor resolución, pero exige cristalizar la proteína — un paso que puede ser imposible (proteínas de membrana, complejos flexibles) y que además la fija en *una* conformación, la que el empaquetamiento del cristal favorece.
- La **RMN** trabaja en solución, más cerca de las condiciones fisiológicas, y captura **flexibilidad**; pero está limitada al tamaño de la proteína.
- La **Cryo-EM** esquiva la cristalización y por eso abrió los complejos grandes y las proteínas de membrana.

Ese detalle —**la estructura experimental es una foto, en unas condiciones**— es el que justifica todo el bloque de [[Dinámica molecular]] y de flexibilidad del receptor en [[Docking molecular]]: la proteína real es un *ensemble* de estados, no la coordenada depositada.

Cuando ninguno de los tres está disponible, quedan [[Modelado por homología]], [[Threading]] y [[AlphaFold]].

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
