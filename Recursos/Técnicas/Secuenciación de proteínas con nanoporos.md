---
tags: [técnica, proteómica, nanoporos, frontera]
area: Técnicas
aliases: [protein sequencing, secuenciación de proteínas, proteómica de molécula única con nanoporos]
---

# Secuenciación de proteínas con nanoporos

Extender el principio del nanoporo desde los ácidos nucleicos a los **polipéptidos**: hacer pasar una proteína o un péptido por un poro y leer los cambios de corriente que producen los aminoácidos.

> La evolución hacia una plataforma comercial **está sucediendo ahora**.

## Por qué es más difícil que el ADN

El ADN tiene 4 letras químicamente parecidas, carga uniformemente negativa y una estructura lineal regular que un motor puede empujar. Las proteínas tienen **20 aminoácidos** con cargas, tamaños y polaridades muy distintas, se pliegan, y no hay una "carga de arrastre" natural que las conduzca por el poro. De ahí que los hitos incluyan tanto el reconocimiento como el **control del movimiento** (ClpX, helicasas, carboxipeptidasas).

## La línea de tiempo

| Año | Hito | Referencia |
|---|---|---|
| 2013 | **Translocación controlada**: ClpX despliega y conduce proteínas por α-hemolisina | Nivala et al. |
| 2014 | **Huellas de variantes**: el patrón de corriente diferencia variantes proteicas | Nivala et al. |
| 2018 | **Resolución de un residuo**: aerolisina distingue homopéptidos que difieren en un aminoácido | Piguet et al. |
| 2020 | **Los 20 aminoácidos**: reconocimiento eléctrico individual con aerolisina | Ouldali et al. |
| 2021 | **Relectura molecular**: helicasa + MspA detectan sustituciones de un aminoácido | Brinkerhoff et al. |
| 2023 | **Secuenciación de péptidos**: carboxipeptidasa + α-hemolisina | Zhang et al. |
| 2024 | **Proteínas largas**: ClpX + CsgG, lectura multipaso en matriz ONT | Motone et al. |
| 2026 | **Sensado paralelo**: perfilado de péptidos e identificación con bibliotecas OPO | Wang et al. |

## La bioinformática asociada

| Año | Herramienta | Qué hace |
|---|---|---|
| 2017 | **Nano-Align** | Identificación contra bases de datos proteicas |
| 2021 | **NanoporeTERs** | Clasificación de etiquetas proteicas sintéticas |
| 2021 | **Poretitioner** | Detección, extracción y filtrado de eventos |
| 2021 | **Chop-n-drop** | Simulación y alineamiento de huellas proteicas |
| 2024 | **PASTOR-sequencing** | Segmentación, DTW, [[Machine Learning\|aprendizaje automático]] y relecturas |

La trayectoria del campo va **de la detección y segmentación de eventos hacia el *fingerprinting* y la identificación asistida por aprendizaje automático**. El **"[[Basecalling|basecalling]]" de proteínas completas** es hoy el punto caliente de innovación — el mismo problema que el ADN resolvió entre 1989 y 2014, comprimido y todavía abierto.

Se conecta con la [[Proteómica de célula única]] vista en la primera clase del módulo: dos caminos distintos hacia la misma meta de medir proteínas con resolución de molécula individual.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
