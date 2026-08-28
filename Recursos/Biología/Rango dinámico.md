---
tags: [concepto, biología, análisis]
area: Biología molecular
---

# Rango dinámico

El **rango dinámico** es el intervalo entre la señal más baja y la más alta que un experimento debe poder medir. En [[Transcriptoma|transcriptómica]] ese intervalo abarca **5 o 6 órdenes de magnitud**: desde genes housekeeping con decenas de miles de copias por célula hasta factores de transcripción presentes en unas pocas moléculas.

## Por qué es un problema

1. **Los genes abundantes consumen la librería.** Si GAPDH y ACTB se llevan una fracción enorme de las lecturas, quedan menos para todo lo demás.
2. **Los genes raros son los interesantes.** Los marcadores que distinguen [[Tipo celular|tipos celulares]] y los reguladores maestros suelen ser de baja abundancia.
3. **Genera ceros que no son ceros biológicos.** Un gen expresado a nivel bajo puede no ser detectado simplemente por sampleo — eso es parte de la [[Sparsity]] (*dropout*).

## En proteómica es peor

En [[Proteómica de célula única]] el rango dinámico es aún más amplio que en ARN, **y no se puede amplificar**: no existe una PCR para proteínas. Ésa es una de las tres grandes barreras técnicas del área, junto con la adsorción en superficies.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
