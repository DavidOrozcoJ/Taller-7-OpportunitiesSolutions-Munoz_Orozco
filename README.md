# Taller 7: Opportunities & Solutions

## Objetivo

Proponer la arquitectura objetivo (TO-BE) de Aplicaciones y de Tecnología del cliente real, identificando las brechas frente al estado actual (AS-IS) documentado en los Talleres 1 a 6 — incluyendo seguridad y cumplimiento normativo — y priorizando las soluciones que las cierran.

---

## Guía paso a paso

Antes de proponer el TO-BE, revise la [**Guía Paso a Paso: Opportunities & Solutions**](clase/guia_paso_a_paso_opportunities_solutions.md). Incluye qué cuenta como una brecha válida en este taller, la metodología en 4 partes (Diagnóstico inicial → Propuesta de mejoras → Visualización TO-BE → Análisis de beneficios y riesgos, siguiendo la actividad oficial de mejora de arquitectura del curso), un ejemplo completo construido paso a paso sobre el AS-IS de RedExpress ya trabajado en los Talleres 3 y 4, y una tabla de errores comunes. Además incluye tres apoyos para decidir: la **matriz de decisión ponderada** (sección 2.1, con el marco de 8 pasos), el uso de la **IA como copiloto de la decisión** (sección 2.2) y la agrupación de brechas por **capacidad de negocio** en paquetes de trabajo (sección 4.1). Para la clase hay también una presentación (`7. Oportunidades_Soluciones.pptx`) que sigue el hilo contexto, armar la solución y tomar la decisión.

### Versión visual: Opportunities & Solutions

[`clase/visualizacion-opportunities-solutions.html`](clase/visualizacion-opportunities-solutions.html) es una página interactiva autocontenida: un mapa de tecnología de RedExpress con un interruptor AS-IS/TO-BE que redibuja el mismo diagrama — en TO-BE aparecen el balanceador pasivo, la BD de Medellín y el módulo de rutas de Medellín, marcados con la etiqueta NUEVO —, la lluvia de ideas priorizada de la Parte 2, la matriz de brechas cerradas con sus riesgos de implementación, una matriz de decisión ponderada con deslizadores para mover los pesos y ver cambiar el ranking en vivo, y el mapa de capacidades con sus paquetes de trabajo. Haga clic en cualquier elemento (nuevo o existente) para ver qué brecha resuelve, el beneficio esperado y el riesgo asociado. GitHub no la renderiza interactiva desde la vista de archivo; para verla:
- Descargue el archivo y ábralo con doble clic (funciona sin conexión, es HTML plano), o
- Pegue esta URL en [htmlpreview.github.io](https://htmlpreview.github.io/): `https://raw.githubusercontent.com/CesarAVegaF312/AREM-Taller_7_Opportunities_Solutions/main/clase/visualizacion-opportunities-solutions.html`

## Caso base de referencia: RedExpress (continuación de los Talleres 3 y 4)

Este taller no introduce un cliente ficticio nuevo: retoma el C1/C2 de RedExpress (Taller 3) y su mapa de infraestructura con los 3 riesgos ya diagnosticados (Taller 4) para proponer, sobre esa misma base, una arquitectura objetivo.

**Por qué este taller va después de Seguridad y Normatividad:**
- Proponer un TO-BE antes de conocer las amenazas de seguridad (Taller 5) o las brechas de cumplimiento (Taller 6) significa diseñar una solución que puede quedar insegura o incumplir la normativa desde el primer día.
- Aquí se consolidan brechas técnicas, funcionales, de seguridad y normativas en una sola matriz — no solo las de infraestructura.

---

## Parte 1: Trabajo en Clase

Durante la clase se espera que el equipo:

Siga la metodología en 4 partes de la [guía paso a paso](clase/guia_paso_a_paso_opportunities_solutions.md) sobre el AS-IS de RedExpress:

1. **Diagnóstico inicial**: consolide los hallazgos del AS-IS (Talleres 3 y 4, y en su cliente real también 5 y 6) respondiendo las tres preguntas orientadoras (fricción, problemas recurrentes, vulnerabilidades/riesgos).
2. **Propuesta de mejoras**: haga una lluvia de ideas de al menos 6 mejoras y priorice 2-3 con justificación, distinguiendo quick wins de mejoras de mayor impacto o largo plazo. Para cada brecha con más de una solución posible, decida con una **matriz de decisión ponderada** (criterios con pesos definidos por el negocio, puntajes justificados, análisis de sensibilidad y trade-off aceptado; [sección 2.1 de la guía](clase/guia_paso_a_paso_opportunities_solutions.md)). Si usa una herramienta de IA como copiloto (ideas, borrador de puntajes, "abogado del diablo"), siga las reglas de la [sección 2.2](clase/guia_paso_a_paso_opportunities_solutions.md) y use la [biblioteca de prompts](plantillas/prompts_ia_decision.md): la IA propone, el equipo verifica, justifica y decide.
3. **Visualización TO-BE**: defina el TO-BE de Aplicaciones (extendiendo el C2 del Taller 3) y de Tecnología (extendiendo el mapa del Taller 4), señalando qué controles de seguridad del Taller 5 se integran.
4. **Análisis de beneficios y riesgos**: construya la matriz de brechas (Gap Analysis) con el beneficio esperado de cada solución priorizada y contrástela con una tabla de riesgos/limitaciones de implementación, y valide con la [checklist de autoevaluación](clase/guia_paso_a_paso_opportunities_solutions.md#5-checklist-de-autoevaluación-antes-de-entregar).

- Use draw.io o Astah UML para los diagramas TO-BE.
- Reciba retroalimentación del docente y registre avances en `clase/notas.md` (use la [plantilla de notas](plantillas/plantilla_notas.md)).

---

## Parte 2: Aplicación al Cliente Real

Después de la clase, el equipo debe:

- Consolidar las brechas técnicas (Talleres 3 y 4), de seguridad (Taller 5) y de cumplimiento (Taller 6) identificadas para su cliente real.
- Proponer el TO-BE de Aplicaciones y de Tecnología del cliente, extendiendo sus propios entregables de los Talleres 3 y 4, y guardar los diagramas como anexos en `entrega/to-be-aplicaciones-final.drawio` y `entrega/to-be-tecnologia-final.drawio`.
- Construir la matriz de brechas priorizada en `entrega/matriz-brechas.xlsx` (también como anexo).
- Redactar el documento único en `entrega/mejora-arquitectura.md` usando la [plantilla de mejora de arquitectura](plantillas/plantilla_mejora_arquitectura.md), siguiendo las 4 partes de la guía (Diagnóstico → Propuesta de mejoras → Visualización TO-BE → Beneficios y riesgos) y referenciando los anexos anteriores. Este es el equivalente en Markdown del documento oficial de la actividad (máx. 6 páginas + anexos); el equipo puede redactar aquí en Markdown y exportar a PDF con el nombre `EquipoX_Mejora_Arquitectura.pdf` para la entrega formal, si el docente lo pide aparte.
- Investigar patrones de solución reales para brechas similares en el sector del cliente, y registrar las fuentes en `entrega/referencias.md` con la [plantilla de referencias](plantillas/plantilla_referencias.md).

---

## Estructura esperada del repositorio

```text
taller-07-opportunities-solutions/
├── README.md
├── 7. Oportunidades_Soluciones.pptx                  # Presentación de la clase
├── clase/
│   ├── guia_paso_a_paso_opportunities_solutions.md   # Qué es una brecha, metodología en 4 partes y ejemplo guiado
│   ├── to-be-borrador.drawio
│   └── notas.md                                      # Ver plantillas/plantilla_notas.md
├── entrega/
│   ├── to-be-aplicaciones-final.drawio                # Anexo: referenciado desde mejora-arquitectura.md
│   ├── to-be-tecnologia-final.drawio                  # Anexo: referenciado desde mejora-arquitectura.md
│   ├── matriz-brechas.xlsx                            # Anexo: referenciado desde mejora-arquitectura.md
│   ├── mejora-arquitectura.md                         # Ver plantillas/plantilla_mejora_arquitectura.md — exportar a PDF como EquipoX_Mejora_Arquitectura.pdf
│   └── referencias.md                                 # Ver plantillas/plantilla_referencias.md
└── plantillas/
    ├── plantilla_mejora_arquitectura.md               # Plantilla principal de entrega de este taller
    ├── plantilla_matriz_decision.md                   # Matriz de decisión ponderada (una por brecha con varias soluciones)
    ├── prompts_ia_decision.md                         # 12 prompts para usar IA como copiloto (uno por paso del método)
    ├── plantilla_informe_taller.md
    ├── plantilla_notas.md
    └── plantilla_referencias.md
```

---

## Errores comunes

Antes de entregar, compare su TO-BE y su matriz contra los errores más frecuentes (TO-BE sin brechas concretas de origen, brechas de seguridad/normatividad ignoradas, priorización solo por impacto) documentados en la [sección 4 de la guía paso a paso](clase/guia_paso_a_paso_opportunities_solutions.md#4-errores-comunes-a-evitar).

## Entregables

- Documento único de mejora de arquitectura (`entrega/mejora-arquitectura.md`), máx. 6 páginas + anexos, siguiendo las 4 partes: Diagnóstico inicial, Propuesta de mejoras, Visualización TO-BE, Análisis de beneficios y riesgos.
- Anexos: Modelo TO-BE de Aplicaciones (extensión del C2 del Taller 3), Modelo TO-BE de Tecnología (extensión del mapa del Taller 4) y Matriz de brechas (Gap Analysis) priorizada.
- Referencias e investigación complementaria.
- Para la entrega formal ante el docente, exportar el documento como PDF con nombre `EquipoX_Mejora_Arquitectura.pdf`.

---

## Rúbrica de Evaluación

Pesos y criterios oficiales de la actividad de mejora de arquitectura del curso:

| Criterio                                      | Peso | Excelente (5)                                                                 | Aceptable (3) / Insuficiente (1–2)                                   |
|------------------------------------------------|------|--------------------------------------------------------------------------------|------------------------------------------------------------------------|
| Diagnóstico claro de problemas y riesgos        | 20%  | Resume con evidencia la fricción, los problemas recurrentes y las vulnerabilidades ya diagnosticadas en los Talleres 3-6, sin inventar hallazgos nuevos | Diagnóstico genérico, sin trazabilidad a los talleres previos, o incompleto |
| Generación y priorización de ideas de mejora    | 25%  | Presenta al menos 6 ideas variadas (proceso, tecnología, seguridad) y prioriza 2-3 con justificación clara, distinguiendo quick wins de mejoras de largo plazo | Menos de 6 ideas, ideas repetidas o triviales, o priorización sin justificación |
| Modelado TO-BE coherente y visualmente claro    | 25%  | El TO-BE extiende coherentemente el C2/mapa de infraestructura del AS-IS, incluye el proceso mejorado y señala los controles de seguridad integrados | TO-BE desconectado del AS-IS, sin controles de seguridad, o difícil de leer |
| Justificación de beneficios y riesgos           | 20%  | Contrasta beneficios de negocio y tecnológicos/de seguridad con riesgos, limitaciones y dependencias reales de implementación | Solo lista beneficios sin riesgos, o riesgos genéricos sin relación con las soluciones propuestas |
| Calidad de redacción y presentación             | 10%  | Documento único, máximo 6 páginas + anexos, bien redactado y fácil de seguir  | Excede el límite de páginas, está desorganizado o tiene errores de redacción |

---

## Licencia

Este taller hace parte del curso de Arquitectura Empresarial - Universidad de La Sabana. Uso académico bajo licencia MIT.
