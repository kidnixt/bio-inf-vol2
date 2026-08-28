---
tags: [concepto, biología]
area: Biología molecular
---

# Expresión génica

**Expresión génica** es el proceso por el cual la información contenida en un gen se convierte en un producto funcional — típicamente una proteína, a veces un ARN funcional. Es el mecanismo que hace que células con el **mismo genoma** tengan identidades y funciones completamente distintas: una [[Neurona]] y un [[Astrocito]] comparten el ADN, pero no el programa de expresión.

## El flujo de la información

Sigue el [[Dogma central de la biología molecular]]:

```
ADN ──transcripción──► ARN ──traducción──► Proteína
```

Cada flecha es un punto de regulación, y cada punto tiene su propia ómica de medición:

| Nivel | Qué se regula | Técnica single-cell |
|---|---|---|
| ADN / [[Cromatina]] | Qué genes son accesibles | [[scATAC-seq]] |
| ARN | Cuánto se transcribe | [[scRNA-seq]] |
| [[Traducción]] | Cuánto se traduce realmente | [[scRibo-seq]] |
| Proteína | Producto final y su abundancia | [[Proteómica de célula única]] |

## Por qué importa en bioinformática

La idea central de las ómicas de célula única es que **la identidad de una célula puede definirse por qué genes expresa** — ver [[Identidad celular]]. Eso convierte a la medición de expresión en una medición de identidad, y habilita [[Clustering]] y [[Anotación de tipos celulares]] a partir de datos puramente moleculares.

> [!warning] Cuidado conceptual
> Cuando decimos "medimos expresión" con [[Bulk RNA-seq]] o [[scRNA-seq]], en realidad estamos cuantificando **la abundancia de moléculas de ARN muestreadas**. No es lo mismo: hay sampleo, [[Profundidad de secuenciación]], ruido y una distribución de conteos de por medio.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
