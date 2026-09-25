# Registro de Trabajo en Clase - Taller 7: Opportunities & Solutions

## Fecha de la sesión
_Por confirmar por el equipo (fecha de la sesión de clase en que se trabajó este taller)._

## Integrantes presentes
- Juan David Orozco Rodríguez
- [Nombre del compañero/a] Muñoz

> Ajustar el nombre completo del segundo integrante antes de subir la entrega.

## Actividades realizadas en clase

- Se revisó la [guía paso a paso](guia_paso_a_paso_opportunities_solutions.md) y su ejemplo guiado, que trabaja el TO-BE de RedExpress retomando el C1/C2 del Taller 3 y el mapa de infraestructura con los 3 riesgos ya diagnosticados en el Taller 4.
- Se siguió la metodología oficial en 4 partes: Diagnóstico inicial → Propuesta de mejoras (con matriz de decisión ponderada) → Visualización TO-BE → Análisis de beneficios y riesgos.
- Se dibujó el borrador del TO-BE de Tecnología en `to-be-borrador.drawio`, extendiendo el mapa de infraestructura del Taller 4 (balanceador redundante, BD particionada por región, módulo de rutas en Medellín).
- Herramientas usadas: draw.io para el diagrama, Markdown para las tablas de diagnóstico y decisión.

---

## Parte 1 — Diagnóstico inicial

| Pregunta orientadora | Respuesta para RedExpress | Taller de origen |
|---|---|---|
| ¿Qué procesos o tecnologías generan mayor fricción en la operación? | El balanceador de carga único y la base de datos con escritura centralizada en Bogotá generan lentitud y riesgo de caída total ante picos de demanda (ej. campañas de fin de año). | Taller 4 |
| ¿Qué problemas recurrentes señalan los usuarios o el cliente? | Los usuarios de Medellín reportan demoras en la asignación de rutas porque toda solicitud depende del motor de rutas de Bogotá. | Taller 4 |
| ¿Qué vulnerabilidades o riesgos quedaron evidenciados en el análisis previo? | Punto único de falla en el balanceador, cuello de botella de escritura en la BD, límite de escalabilidad geográfica en Medellín. | Taller 4 |

**Brechas de partida:**

| Riesgo / Brecha | Taller de origen | Tipo |
|---|---|---|
| Balanceador de Carga (instancia única) | Taller 4 | Técnica |
| Base de Datos Distribuida (escritura única en Bogotá) | Taller 4 | Técnica |
| Región Medellín sin módulo de rutas propio | Taller 4 | Técnica / Funcional |

> El ejercicio de clase se enfoca en las brechas técnicas de RedExpress porque son las únicas completamente diagnosticadas en el curso (Taller 4). Con el cliente real (Parte 2), este diagnóstico se completa sumando las brechas de seguridad (Taller 5) y de cumplimiento normativo (Taller 6).

---

## Parte 2 — Propuesta de mejoras

**Lluvia de ideas (sin censura inicial):**

| # | Idea de mejora | Tipo |
|---|---|---|
| 1 | Balanceador de carga redundante (activo-pasivo) | Técnica |
| 2 | Base de datos particionada por región | Técnica |
| 3 | Módulo de rutas propio en Medellín | Técnica / Funcional |
| 4 | Notificaciones proactivas al cliente cuando se detecta una demora prevista en la entrega | Proceso / Comunicación |
| 5 | Checklist digital de verificación del paquete en el punto de entrega, firmado por el mensajero | Proceso |
| 6 | Encuesta corta de satisfacción integrada en la app, justo después de cada entrega | Proceso / Comunicación |
| 7 | Canal de WhatsApp o chatbot para consultar el estado de un envío sin llamar a soporte | Proceso / Comunicación |
| 8 | Panel unificado de monitoreo para operadores, con alertas por región | Técnica (mediano plazo) |

**Priorización (justificación):** de las 8 ideas, se priorizan las 3 mejoras técnicas (#1, #2, #3) porque son las únicas con brecha ya diagnosticada y evidenciada en el Taller 4 (trazabilidad directa AS-IS → TO-BE). Las ideas de proceso (#4-#7) son válidas y de bajo esfuerzo (quick wins), pero quedan como backlog porque aún no tienen un hallazgo formal que las respalde en este ejercicio de clase.

| Solución priorizada | Esfuerzo | Impacto | Quick win / Largo plazo | Prioridad |
|---|---|---|---|---|
| Balanceador redundante | Medio | Alto | Quick win | 1 |
| BD particionada por región | Alto | Alto | Largo plazo | 2 |
| Módulo de rutas en Medellín | Alto | Medio | Largo plazo | 3 |

### Matriz de decisión ponderada — Balanceador de carga (brecha #1)

**Brecha que se decide:** punto único de falla del balanceador de carga (Taller 4).

**Paso 1 — Problema en términos de impacto:** si el balanceador cae durante la campaña de fin de año, toda la plataforma queda inaccesible en el país: en el pico de ~1.200 envíos/hora, cada hora de caída deja esos envíos sin asignar y sin seguimiento.

**Paso 2 — Último momento responsable:**

| Dato | Valor |
|---|---|
| La campaña de fin de año empieza el | 1 de noviembre |
| Tiempo de la opción más probable (aprovisionamiento + pruebas de failover) | 6 semanas + 2 semanas = 8 semanas |
| **Último momento responsable** | 1 de noviembre − 8 semanas ≈ **6 de septiembre** |
| Fecha de hoy (supuesto) y días que quedan | 25 de agosto → ~12 días para decidir |

**Paso 3 — Criterios, pesos y escala:**

| Criterio | Peso | Qué significa 5 | Qué significa 1 |
|---|---|---|---|
| Disponibilidad lograda | 35% | Ninguna caída perceptible ante la falla del balanceador | La falla sigue dejando la plataforma inaccesible |
| Costo total | 25% | Menos de USD 100/mes adicionales | Más de USD 1.200/mes adicionales |
| Complejidad operativa | 20% | No hay nada nuevo que operar | Sincronización y pruebas continuas entre componentes |
| Tiempo de implementación | 20% | Menos de 1 semana | Más de 10 semanas |
| **Total** | **100%** | | |

_Por qué esos pesos:_ el balanceador es el riesgo Alto de disponibilidad del Taller 4 (35%); el presupuesto adicional es la dependencia principal de la Parte 4 (25%); complejidad y tiempo pesan igual porque el equipo de plataforma es pequeño (20% cada uno).

_Criterio eliminatorio:_ toda opción con Disponibilidad menor a 3 se descarta, sin importar su total.

**Paso 4 — Opciones:**

| Opción | Descripción |
|---|---|
| A | Balanceador activo-pasivo con failover automático |
| B | Balanceador activo-activo, con almacén de sesión compartido |
| C | Mantener el balanceador único y reforzar el monitoreo (opción radicalmente distinta) |

**Paso 5 — Consejo consultado:**

| A quién | Qué aportó | Qué opción afecta |
|---|---|---|
| Líder de infraestructura (sabe) | La conmutación activo-pasivo demora 30-60 s; el activo-activo exige un almacén de sesión compartido que hoy no existe | A y B |
| Proveedor cloud (sabe) | Cotiza: segunda instancia ≈ USD 400/mes; esquema activo-activo ≈ USD 1.100/mes; monitoreo reforzado ≈ USD 60/mes | A, B, C |
| Jefe de operadores logísticos (le afecta) | 30-60 s de espera al conmutar es tolerable; una caída de más de 10 minutos en campaña, no | A vs. C |

**Paso 6 — Puntajes con justificación:**

| Opción | Disponibilidad | Costo | Complejidad | Tiempo |
|---|---|---|---|---|
| A · Activo-pasivo | 4 — conmuta solo, ventana de 30-60 s | 4 — +USD 400/mes (rango 100-500) | 4 — un componente nuevo, failover simple | 3 — 4-6 semanas |
| B · Activo-activo | 5 — sin ventana de conmutación | 2 — +USD 1.100/mes (rango 800-1.200) | 2 — sincronización y pruebas continuas | 2 — 8-10 semanas |
| C · Único + monitoreo | 1 — no elimina el punto único de falla | 5 — +USD 60/mes | 5 — nada nuevo que operar | 5 — menos de 1 semana |

**Totales ponderados:**

| Opción | Cálculo | Total |
|---|---|---|
| A · Activo-pasivo | 4×0,35 + 4×0,25 + 4×0,20 + 3×0,20 | **3,80** |
| B · Activo-activo | 5×0,35 + 2×0,25 + 2×0,20 + 2×0,20 | **3,05** |
| C · Único + monitoreo | 1×0,35 + 5×0,25 + 5×0,20 + 5×0,20 | **3,60** |

**Sensibilidad:** con pesos alternativos (costo 35%, complejidad 25%, tiempo 25%, disponibilidad solo 15%), los totales cambian a A = 3,75, B = 2,45, **C = 4,40** — ganaría no hacer nada. Esto confirma que el desacuerdo real está en qué valora el negocio, no en las opciones. Con el criterio eliminatorio (Disponibilidad < 3 se descarta), C queda fuera del juego en ambos escenarios y la decisión real es entre A y B.

**Paso 7 — Decisión:**
- **Decisión:** implementar un balanceador activo-pasivo con failover automático (opción A).
- **Trade-off aceptado:** se sacrifica la conmutación instantánea (ventana de 30-60 s) a cambio de menor costo y menor complejidad operativa que el activo-activo.
- **Alternativas descartadas:** B, por costo (+USD 1.100/mes) y por no llegar a la campaña (8-10 semanas + pruebas); C, por no eliminar el punto único de falla (falla el criterio eliminatorio).

**Paso 8 — Reevaluación:** revisar la decisión después de la campaña de fin de año, o antes si el tráfico crece 30% sobre el pico registrado; si eso ocurre, reconsiderar B.

> Las otras dos brechas priorizadas (BD particionada por región y módulo de rutas en Medellín) tienen una única solución razonable dado el diagnóstico del Taller 4, por lo que no requieren una matriz de decisión aparte — se documentan directamente en la Parte 3 (TO-BE) y la Parte 4 (beneficios y riesgos).

---

## Parte 3 — Visualización TO-BE

**Boceto inicial del modelo:** ver [`to-be-borrador.drawio`](to-be-borrador.drawio) — mapa de tecnología TO-BE que extiende el del Taller 4, con los 3 elementos nuevos resaltados en verde: balanceador pasivo, BD Medellín (partición regional) y módulo de rutas Medellín.

**TO-BE de Aplicaciones (extiende el C2 del Taller 3):** se agrega un Módulo de Procesamiento de Rutas y Paquetes - Medellín, réplica del de Bogotá, para que la región deje de depender de un solo punto de procesamiento.

**TO-BE de Tecnología (extiende el mapa del Taller 4):** el balanceador pasa a ser redundante (activo-pasivo, decisión de la matriz anterior) y la base de datos se particiona por región para reducir la dependencia de una única escritura centralizada en Bogotá. Diagrama completo en `to-be-borrador.drawio`.

**Controles de seguridad integrados:** el ejercicio de clase sobre RedExpress no tiene un Taller 5 (STRIDE) construido específicamente para este caso — el ejemplo guiado de STRIDE del curso usa un sistema académico distinto. Queda pendiente para la Parte 2 (cliente real): ahí sí se debe declarar explícitamente qué mitigaciones STRIDE del Taller 5 protegen los componentes que el TO-BE modifica.

---

## Parte 4 — Análisis de beneficios y riesgos

**Brechas cerradas y beneficios esperados:**

| AS-IS | TO-BE | Brecha que cierra | Beneficio esperado |
|---|---|---|---|
| Balanceador único | Balanceador redundante (activo-pasivo) | Punto único de falla | Alta disponibilidad de toda la plataforma |
| BD con escritura única en Bogotá | BD particionada por región | Cuello de botella de latencia | Mejor rendimiento del rastreo en tiempo real fuera de Bogotá |
| Medellín sin módulo de rutas propio | Módulo de rutas replicado en Medellín | Límite de escalabilidad geográfica | La región puede crecer sin saturar Bogotá |

**Riesgos, limitaciones y dependencias de implementación:**

| Solución | Riesgo / limitación / dependencia |
|---|---|
| Balanceador redundante | Depende de la aprobación de presupuesto adicional del proveedor cloud; si no se aprueba, la mejora no puede iniciar en el plazo previsto. |
| BD particionada por región | Requiere migración con ventana de mantenimiento; riesgo de downtime parcial e inconsistencia de datos durante la sincronización inicial. |
| Módulo de rutas en Medellín | Depende de contratar o reasignar personal técnico en la región; sin ese equipo local, el módulo replicado no tiene quién lo opere ni lo mantenga. |

### Capacidades de negocio y paquetes de trabajo

| Capacidad | Madurez AS-IS | Madurez TO-BE | Qué la explica |
|---|---|---|---|
| Recepción y registro de envíos | 4 | 4 | Sin brechas diagnosticadas; no se toca en esta iteración |
| Planeación y asignación de rutas | 2 | 4 | Medellín depende del motor de Bogotá y se demora (Taller 4) |
| Seguimiento en tiempo real | 3 | 4 | Escritura centralizada en Bogotá lo hace lento fuera de allí |
| Notificación y atención al cliente | 3 | 3 | Sin brecha formal; ideas #4 y #7 quedaron en backlog |
| Continuidad operativa de la plataforma | 2 | 4 | Punto único de falla en el balanceador |

| Paquete de trabajo | Brechas que incluye | Capacidad que mejora | Tipo |
|---|---|---|---|
| WP1 · Continuidad de la plataforma | Balanceador redundante activo-pasivo (decisión de la matriz) | Continuidad operativa (2 → 4) | Quick win · 4-6 semanas |
| WP2 · Rutas y datos regionales | Módulo de rutas en Medellín + BD particionada por región | Planeación y asignación de rutas (2 → 4) y Seguimiento en tiempo real (3 → 4) | Largo plazo |

---

## Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Pasar `to-be-borrador.drawio` a los diagramas finales de aplicaciones y tecnología | Por asignar | Antes de iniciar Parte 2 |
| Revisar checklist de autoevaluación (sección 5 de la guía) | Juan David Orozco Rodríguez | Antes de la entrega de Parte 1 |
| Consolidar brechas técnicas, de seguridad (Taller 5) y normativas (Taller 6) del cliente real, y construir su propia matriz de decisión | Equipo completo | Al iniciar Parte 2, en otro repositorio |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 7 (Parte 1) en el curso Arquitectura Empresarial (AREM) - Universidad de La Sabana._
