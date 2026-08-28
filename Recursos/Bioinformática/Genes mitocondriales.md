---
tags: [concepto, bioinformática, single-cell]
area: Bioinformática
aliases: [fracción mitocondrial, porcentaje mitocondrial, MT genes]
---

# Genes mitocondriales

Los genes codificados por el **genoma mitocondrial** (13 genes codificantes de proteínas en humanos, más ARNr y ARNt). Su fracción sobre el total de [[UMI|UMIs]] es una de las tres métricas del [[Control de calidad en scRNA-seq]].

## Por qué funcionan como métrica de calidad

Los transcriptos mitocondriales están **dentro** de la mitocondria, con su propia doble membrana. Cuando una célula se estresa o muere:

```
membrana plasmática comprometida
        ↓
el ARN citoplasmático se escapa al medio
        ↓
el ARN mitocondrial permanece protegido
        ↓
↑ fracción mitocondrial en lo que queda
```

Una fracción mitocondrial alta indica, por lo tanto, una célula dañada — muy frecuentemente por el propio proceso de [[Aislamiento de células individuales]].

## Cuidados

El umbral es **específico del tejido**. Células con alta demanda energética (cardiomiocitos, [[Neurona|neuronas]], músculo) tienen naturalmente una fracción mitocondrial elevada, y aplicarles el umbral estándar del 5% elimina las células sanas junto con las muertas. En protocolos de núcleos aislados (snRNA-seq) ocurre lo contrario: casi no hay señal mitocondrial y la métrica pierde utilidad.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
