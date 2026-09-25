---
tags: [concepto, bioinformática, farmacología]
area: Bioinformática
aliases: [drug repurposing, reposicionamiento, reposicionar, drug repositioning]
---

# Reposicionamiento de fármacos

Encontrarle **un uso nuevo a un fármaco que ya existe**. Es una de las estrategias más atractivas del descubrimiento de fármacos porque saltea buena parte del riesgo: el compuesto ya tiene perfil [[ADMET]] conocido, dosis estudiadas y, muchas veces, aprobación regulatoria.

## El caso de la clase: halicina

El ejemplo emblemático (Stokes et al., *Cell* 2020):

| | |
|---|---|
| Conjunto inicial de entrenamiento | **2.335** moléculas |
| Moléculas evaluadas virtualmente | **> 107 M** (Drug Repurposing Hub + ZINC15) |
| Resultado | Un candidato **inesperado**, después validado |

Una red neuronal de paso de mensajes (*directed message passing*) entrenada sobre un conjunto chico predijo actividad antibiótica; **el modelo priorizó un candidato inesperado** —la **halicina**, un compuesto desarrollado originalmente para diabetes— **que después se validó**: bactericida de amplio espectro, activo contra *Acinetobacter baumannii* y *Clostridioides difficile*.

Es [[Diseño basado en ligandos|LBDD]] + [[Deep Learning|deep learning]] en estado puro: **sin estructura del blanco y sin mecanismo conocido**, solo fenotipo (¿inhibe el crecimiento de *E. coli*?) y aprendizaje. Y también un buen ejemplo de por qué el reposicionamiento se beneficia tanto de la IA: el modelo no tiene los prejuicios químicos de un medicinal chemist, así que puede proponer algo que "no parece" un antibiótico.

## Dónde se hace

La base de referencia es [[DrugBank]] (fármacos, blancos, mecanismos, indicaciones e interacciones) y recursos hermanos como el *Drug Repurposing Hub*. También se aborda desde el otro lado, con [[Cribado virtual inverso|búsqueda inversa de blancos]].

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
