---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [GO, ontología génica, enriquecimiento funcional]
---

# Gene Ontology (GO)

Vocabulario controlado y estructurado que describe los genes en tres dominios:

| Dominio | Qué describe |
|---|---|
| **Biological Process** | En qué proceso participa el gen (apoptosis, ciclo celular) |
| **Molecular Function** | Qué hace la proteína (unión a ATP, actividad quinasa) |
| **Cellular Component** | Dónde se localiza (membrana, núcleo, mitocondria) |

Los términos están organizados jerárquicamente, de lo general a lo específico.

## Para qué se usa

Es la herramienta estándar para **interpretar una lista de DEGs** ([[Expresión diferencial]]). En lugar de mirar 500 genes uno por uno, se pregunta: ¿hay algún proceso biológico sobrerrepresentado en esta lista respecto de lo esperable al azar? La respuesta se obtiene con un test de enriquecimiento.

## Cuidados

- **El universo importa.** El conjunto de fondo debe ser el de los genes efectivamente medidos, no todo el genoma. En [[scRNA-seq]], con [[Sparsity]] alta, muchos genes nunca se detectan y no deberían estar en el universo.
- **Sesgo de anotación.** Los procesos más estudiados tienen más genes anotados, y por eso salen enriquecidos más a menudo. Los términos genéricos ("regulación de procesos metabólicos") suelen ser poco informativos.
- Es análisis **descriptivo**, no mecanístico: sugiere hipótesis, no las demuestra.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
