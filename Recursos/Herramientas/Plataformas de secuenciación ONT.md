---
tags: [herramienta, plataforma, nanoporos]
area: Herramientas
aliases: [MinION, GridION, PromethION, Flongle, flow cell, MinKNOW]
---

# Plataformas de secuenciación ONT

La familia de equipos de [[Oxford Nanopore Technologies]] cubre un rango de escala poco habitual: **del dispositivo de bolsillo de 130 g al equipo de 4,8 Tb por corrida**, todos con la misma química y el mismo tipo de dato.

| | MinION Mk1D | GridION | PromethION 2 Integrated | PromethION 24 |
|---|---|---|---|---|
| Flow cells | 1 | 1–5 | 1–2 | 1–24 |
| Output por flow cell | 15–35 Gb | 15–35 Gb | 100–200 Gb | 100–200 Gb |
| Output por equipo | 15–35 Gb | 75–175 Gb | 200–400 Gb | **2,4–4,8 Tb** |
| Análisis a bordo | — | ✓ | ✓ | ✓ |
| Pantalla táctil | — | ✓ | ✓ | — |
| Peso | **130 g** | 14,4 kg | 10,6 kg | 23 + 26 kg |

- **Longitud de lectura:** cualquiera, de 20 pb a más de 4 Mb, en todos los equipos.
- **Tiempo de corrida:** ~1–72 h, con [[Secuenciación en tiempo real|streaming en tiempo real]]; en PromethION se puede detener cuando hay datos suficientes, lavar y reutilizar la flow cell.

## Usos declarados

| Gama | Aplicaciones |
|---|---|
| MinION / GridION / Flongle | Genomas pequeños, secuenciación dirigida, **identificación microbiana**, perfilado de [[Resistencia antimicrobiana\|AMR]], expresión génica |
| PromethION | Genomas humanos y grandes, cáncer, **[[Metagenómica clínica\|metagenómica]]**, transcriptómica de isoformas, single-cell |

El **Flongle** es el adaptador de flow cell más pequeño y barato, pensado para tests rápidos y de bajo volumen.

## MinKNOW

Es el software de control de la corrida: opera la flow cell, muestra la ocupación de poros en tiempo real, integra el [[Basecalling|basecalling]] con [[Dorado]] y permite el análisis a bordo en los equipos que lo soportan.

## GridION Dx

Versión certificada **CE y UKCA** (2026) del GridION, primer dispositivo de [[Uso clínico y marco regulatorio|diagnóstico *in vitro*]] de ONT registrado en el Reino Unido y Europa. Corre únicamente flujos validados por terceros.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
