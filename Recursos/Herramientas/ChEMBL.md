---
tags: [herramienta, base-de-datos, bioactividad]
area: Herramientas
aliases: [ChEMBL 37, base ChEMBL]
---

# ChEMBL

Base de datos de **moléculas con actividad experimental medida**, curada manualmente a partir de la literatura por el equipo ChEMBL del **EMBL-EBI** (Reino Unido). Es la fuente clásica para entrenar modelos de [[Diseño basado en ligandos|LBDD]].

| | |
|---|---|
| Tipo de registro | Compuestos distintos |
| Tamaño (corte) | **2.921.148** (v37, publicada 29/05/2026) |
| Qué ofrece | Compuestos, ensayos, blancos, bioactividades, [[ADMET]] y datos de fármacos |
| Consulta típica | *¿Qué compuestos tienen actividad medida frente a este blanco?* |

## Por qué es la base del QSAR

Un modelo [[QSAR]] necesita pares (molécula, actividad). ChEMBL es el mayor repositorio curado de esos pares, y por eso aparece como punto de partida en casi todos los pipelines de la clase: los ligandos de MAO del ejemplo de **VS + ML** salen de ChEMBL, igual que los conjuntos de entrenamiento de la mayoría de los modelos de predicción de actividad.

> [!warning] La advertencia de la clase
> **Ki, Kd, IC50 y respuestas celulares requieren interpretación y curación.** No son intercambiables: dependen del ensayo, de la concentración de sustrato, del tipo celular. Mezclarlos sin cuidado produce modelos que aprenden el ensayo en vez de la química.

Comparte datos con [[BindingDB]]. Frente a [[ZINC]] (≈5·10¹⁰ moléculas enumerables) los ~3·10⁶ compuestos con actividad medida muestran la **asimetría central** del campo: se puede enumerar mucho más de lo que se puede medir.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
