---
tags: [concepto, bioinformática, espacial]
area: Bioinformática
aliases: [comunicación intercelular, interacción célula-célula, cell-cell communication, ligando-receptor, ligand-receptor]
---

# Comunicación célula-célula

Inferir **qué células se están "hablando"** y a través de qué pares **ligando–receptor**. Es uno de los objetivos principales de combinar [[scRNA-seq]] con [[Transcriptómica espacial]].

## Por qué el espacio es necesario

Las señales **yuxtacrinas y paracrinas** actúan a distancias de **0 a 200 µm**. Los métodos que usan solo scRNA-seq + una base de datos de pares conocidos predicen interacciones entre tipos celulares que quizás **nunca están cerca** en el tejido. El dato espacial permite:

- Exigir **co-localización** del ligando y el receptor (mismo spot o spots adyacentes).
- Estimar **rangos máximos** de señalización y **descartar** interacciones entre células demasiado lejanas.
- Ubicar las interacciones respecto de estructuras del tejido (el borde de un tumor, una placa amiloide) → [[Spatial niches]], [[Neighborhoods]].

## Métodos (según [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics|Longo et al. 2021]], [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]] y [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou 2026]])

| Método | Idea |
|---|---|
| Modelos lineales generalizados | ¿Co-localizan ligando y receptor dentro del spot o entre spots vecinos? |
| **Giotto** | Probabilidad de uso de una interacción según la proximidad de las células que la expresan |
| **SpaOTsc** | Transporte óptimo; estima el rango de señalización a partir de genes blanco río abajo |
| **SVCA** | Cuánta varianza de cada gen se explica por interacciones con vecinos |
| DIALOGUE, CellNEST, Nicheformer | Programas multicelulares, interacciones "en relevo", *foundation models* de nichos |

## Cuidado con los artefactos

- La [[Lateral diffusion]] desplaza transcriptos a spots vecinos y puede generar **falsas interacciones célula–célula** (la consecuencia que muestra la diapositiva de la clase).
- Los errores de [[Segmentación celular]] (transcriptos asignados a la célula vecina) crean co-expresión espuria.
- En plataformas de imagen, muchos pares ligando–receptor **no están en el panel**.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]] *(lectura)*
- [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
