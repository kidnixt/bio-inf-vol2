---
tags: [biología, microbiología, clínica]
area: Biología
aliases: [AMR, resistencia a antibióticos, antibiograma, genes de resistencia, antimicrobial stewardship, MRSA, OXA-48, KPC-2]
---

# Resistencia antimicrobiana (AMR)

Capacidad de un microorganismo de sobrevivir a un antimicrobiano que antes lo eliminaba. Es el hilo que atraviesa toda la parte aplicada de la clase.

## Dos formas de estudiarla

| Aproximación | Qué mide | Límite |
|---|---|---|
| **Antibiograma** (fenotípica) | Si el aislado crece o no en presencia del antibiótico | Requiere cultivo; días |
| **Genómica** | Presencia de **genes de resistencia** en la secuencia | Horas, sin cultivo — pero **gen de AMR ≠ fenotipo** |

Esa desigualdad es una de las tres que la clase subraya: un gen presente puede no expresarse, estar truncado, o no conferir resistencia clínicamente relevante. Por eso el [[Secuenciación 16S|16S]] y la [[Metagenómica clínica|metagenómica]] **no reemplazan el antibiograma**.

## En el flujo bioinformático

En la [[Metagenómica clínica|metagenómica clínica]] del NHS, la detección de genes de AMR ocurre en el resultado preliminar (**≈2 h**) usando **Abricate** contra la base **CARD**, con **Scagaire** para filtrar por relevancia según el organismo. La detección precoz de resistencia es lo que permite pasar de tratamiento empírico a **terapia dirigida** el mismo día.

## Por qué las lecturas largas importan aquí

Los genes de resistencia suelen viajar en **[[Plásmido|plásmidos]] y elementos móviles**, rodeados de secuencias repetidas. Con [[Secuenciación de segunda generación|lecturas cortas]] se detecta que el gen está, pero no **en qué molécula** ni **en qué contexto genético** — y por lo tanto no se puede saber si puede saltar a otra especie.

Los casos de [[Vigilancia genómica hospitalaria|vigilancia hospitalaria]] de la clase muestran exactamente eso: **MRSA** en neonatología, transmisión del plásmido **pQEB1/KPC-2** entre especies, *K. variicola* con reservorio ambiental. Y en la región, la primera detección de *Klebsiella pneumoniae* ST15 portadora de **OXA-48** en Sudamérica, y la evidencia de que la microbiota humana disemina resistencia hospitalaria en el ambiente urbano ([[Cecilia Salazar]] y colaboradores).

## Antimicrobial stewardship

El uso racional de antimicrobianos es la métrica con la que se evalúa el impacto clínico de estas tecnologías. En los siete hospitales del NHS, el 16S aportó información útil para stewardship en el **56,9%** de los casos, con confirmación, escalación o desescalación del tratamiento.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
