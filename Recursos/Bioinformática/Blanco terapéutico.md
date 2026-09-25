---
tags: [concepto, bioinformática, farmacología]
area: Bioinformática
aliases: [blanco, diana, target, blanco molecular, dianas terapéuticas]
---

# Blanco terapéutico

> Un **blanco** o **diana** es una entidad biológica cuya modificación puede producir un efecto terapéutico.

Identificarlo es la **etapa 1** del [[Descubrimiento y desarrollo de fármacos|desarrollo de un fármaco]], y la pregunta que la gobierna es *"¿cómo convertimos una enfermedad compleja en una hipótesis tratable?"*.

## Tipos de blanco y mecanismos de acción

| Tipo | Qué hace | Cómo se lo modula |
|---|---|---|
| **Enzima** | Acelera una reacción química | Un **inhibidor** reduce esa actividad |
| **Receptor** | Reconoce señales | Un **agonista** activa una respuesta; un **antagonista** la bloquea |
| **Canal o transportador** | Controla el paso de sustancias a través de una membrana | Bloqueo o modulación |
| **Ligando** | Molécula que se une a un blanco | La unión puede modificar su función |

> **La pregunta terapéutica incluye qué modificar, en qué dirección y dónde.**

Las tres partes importan: no alcanza con elegir una proteína (*qué*), hay que decidir si conviene inhibirla o activarla (*en qué dirección*) y en qué tejido o compartimento (*dónde*).

## Qué hace falta saber de él

Un blanco "tratable y seguro" requiere: **identidad y secuencia** ([[UniProt]]), idealmente **estructura 3D** ([[PDB]] o [[AlphaFold DB]]) para hacer [[Diseño basado en estructura|SBDD]], **ligandos conocidos** ([[ChEMBL]], [[BindingDB]]) para hacer [[Diseño basado en ligandos|LBDD]], y evidencia biológica de que modificarlo produce el efecto buscado sin daño colateral.

Ese último punto —selectividad— es lo que conecta con [[Cribado virtual inverso|la búsqueda inversa de blancos]]: dada una molécula activa, ¿contra qué actúa realmente?

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
