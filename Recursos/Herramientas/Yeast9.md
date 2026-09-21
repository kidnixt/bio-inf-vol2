---
tags: [herramienta, modelo, modelado]
area: Herramientas
aliases: [yeast9, modelo Yeast9, yeast9_anaerobic_biggids]
---

# Yeast9

El [[Modelo metabólico a escala genómica]] consenso de *[[Saccharomyces cerevisiae]]*, y el modelo sobre el que corre el caso de estudio de la clase.

## Su rol en el caso

| Uso | Detalle |
|---|---|
| Red base | Define todas las reacciones y genes disponibles del hospedero |
| Candidatos **KO** | **Todos los genes nativos** del modelo |
| Candidatos **KI** | 13 reacciones heterólogas de metabolismo de xilosa y arabinosa, agregadas al modelo ([[Vías de asimilación de pentosas]]) |
| Condiciones | Aeróbica o anaeróbica; captación permitida de glucosa, xilosa y arabinosa |

Que los candidatos a KO sean *todos* los genes nativos es lo que hace el problema interesante y costoso: el algoritmo no recibe ninguna pista sobre dónde mirar, y aun así **redescubre** blancos conocidos como PGI y RPE.

En [[PECA]] aparece precargada la variante `yeast9_anaerobic_biggids.xml` (versión anaeróbica con identificadores de [[BiGG Models|BiGG]]), junto a `iMM904.xml` — un modelo anterior de la misma levadura — y `PECA_toy.xml`, un modelo de juguete para probar la interfaz.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
