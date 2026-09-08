---
tags: [clínica, regulación, secuenciación]
area: Técnicas
aliases: [RUO, LDT, IVD, diagnóstico in vitro, CE, UKCA, GridION Dx, Research Use Only, Laboratory Developed Test]
---

# Uso clínico y marco regulatorio

La distancia entre "esto funciona en el laboratorio" y "esto puede usarse para decidir el tratamiento de un paciente" es regulatoria, y la clase la marca explícitamente.

## Las tres categorías

| Sigla | Qué significa | Implicancia |
|---|---|---|
| **RUO** | *Research Use Only* | No puede usarse para diagnóstico. **La mayor parte de las aplicaciones microbiológicas de ONT sigue en esta categoría** |
| **LDT** | *Laboratory Developed Test* | Ensayo desarrollado y validado internamente por un laboratorio, bajo su propia responsabilidad. Varios de los protocolos clínicos citados en la clase (16S hospitalario, metagenómica respiratoria) son LDT |
| **IVD** | Diagnóstico *in vitro* | Dispositivo registrado y certificado para uso diagnóstico |

## GridION Dx (2026)

ONT obtiene para GridION las certificaciones **CE y UKCA**, convirtiéndolo en el **primer dispositivo de diagnóstico *in vitro* de la compañía registrado en el Reino Unido y Europa**.

- Se utilizará con **protocolos validados por terceros**.
- **No** admite desarrollo de ensayos custom ni modos research/developer — para eso ONT ofrece la línea Q-Line, orientada a flujos LDT.
- Según ONT, la certificación confirma el cumplimiento de estándares internacionales de calidad, seguridad y rendimiento, y posiciona a la compañía para mercados clínicos regulados.

## Por qué importa para la bioinformática

La cuarta consideración final de la clase lo dice sin rodeos: la aplicación clínica sigue limitada por

- **bases de datos curadas y actualizadas**,
- **trazabilidad de las versiones de [[Basecalling|basecaller]] y software**,
- acreditación regulatoria,
- evaluación costo-beneficio.

La trazabilidad es un requisito propio de esta tecnología: como el mismo [[POD5]] rebasecalleado con [[Dorado]] v4 o v5 da resultados distintos, **la versión del software es parte del resultado clínico** y debe quedar registrada.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
