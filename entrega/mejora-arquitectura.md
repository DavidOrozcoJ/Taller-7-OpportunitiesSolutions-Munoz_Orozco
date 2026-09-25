# Mejora de Arquitectura (TO-BE) — Identificación y Priorización de Mejoras

## Cliente
RedExpress (caso base de referencia del curso, retomado de los Talleres 3 y 4 — ver nota de alcance al final de este documento)

## Integrantes del equipo
- Juan David Orozco Rodríguez
- [Nombre del compañero/a] Muñoz

---

## 1. Diagnóstico inicial

- **¿Qué procesos o tecnologías generan mayor fricción en la operación?** El balanceador de carga único y la base de datos con escritura centralizada en Bogotá generan lentitud y riesgo de caída total ante picos de demanda (ej. campañas de fin de año).
- **¿Qué problemas recurrentes señalaron los usuarios o el cliente?** Los usuarios de Medellín reportan demoras en la asignación de rutas porque toda solicitud depende del motor de rutas de Bogotá.
- **¿Qué vulnerabilidades de seguridad o riesgos quedaron evidenciados en el análisis previo?** Punto único de falla en el balanceador, cuello de botella de escritura en la BD, límite de escalabilidad geográfica en Medellín (los 3 riesgos diagnosticados en el Taller 4).

**Resumen del problema actual (foto del AS-IS):** RedExpress opera hoy sobre una infraestructura centralizada en Bogotá: un único balanceador de carga sin redundancia, una base de datos con escritura única, y ningún módulo de procesamiento de rutas propio en Medellín. Esto deja a toda la plataforma expuesta a una caída total si el balanceador falla, degrada el rendimiento del rastreo en tiempo real fuera de Bogotá, y limita el crecimiento de la operación en la región de Medellín, que depende por completo del motor de rutas de la capital.

---

## 2. Propuesta de mejoras

### 2.1 Lluvia de ideas (sin censura inicial)

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

### 2.2 Priorización (2-3 ideas seleccionadas, con justificación)

| Solución priorizada | Esfuerzo | Impacto | Quick win / Largo plazo | Justificación |
|---|---|---|---|---|
| Balanceador redundante | Medio | Alto | Quick win | Única mejora con brecha diagnosticada (Taller 4) que puede implementarse en 4-6 semanas; decidida formalmente mediante matriz de decisión ponderada (ver `plantillas/plantilla_matriz_decision.md` y `clase/notas.md`) frente a un esquema activo-activo y a "no hacer nada" |
| BD particionada por región | Alto | Alto | Largo plazo | Cierra el cuello de botella de latencia diagnosticado en Taller 4; requiere migración planeada, no es un quick win |
| Módulo de rutas en Medellín | Alto | Medio | Largo plazo | Cierra el límite de escalabilidad geográfica; depende de contratar/reasignar personal técnico regional |

Las ideas de proceso (#4-#7) son válidas y de bajo esfuerzo (quick wins), pero quedan como backlog para una siguiente iteración porque todavía no tienen un hallazgo formal que las respalde en este ejercicio (no hubo entrevistas de cliente real documentadas para RedExpress en el curso).

**Decisión con matriz ponderada (brecha #1 — balanceador):** se evaluaron 3 opciones (activo-pasivo, activo-activo, mantener único + monitoreo) contra 4 criterios ponderados por el negocio (disponibilidad 35%, costo 25%, complejidad 20%, tiempo 20%). Resultado: **A · Activo-pasivo gana con 3,80 puntos** sobre B (3,05) y C (3,60, descartada por criterio eliminatorio de disponibilidad < 3). El desarrollo completo de los 8 pasos, incluyendo el análisis de sensibilidad, está documentado en `clase/notas.md`.

---

## 3. Visualización TO-BE

### 3.1 Proceso mejorado
El proceso de asignación de rutas para envíos originados en Medellín deja de depender de una llamada remota al motor de rutas de Bogotá: con el módulo replicado, la asignación se resuelve localmente, reduciendo la latencia percibida por mensajeros y operadores en esa región.

### 3.2 Cambios en aplicaciones, infraestructura y flujos de información
El TO-BE de Aplicaciones extiende el C2 del Taller 3 agregando el **Motor de Rutas - Medellín** (réplica del de Bogotá), conectado al mismo Módulo de Gestión de Paquetes. El TO-BE de Tecnología extiende el mapa de infraestructura del Taller 4: el balanceador de carga pasa a ser redundante (activo-pasivo, con conmutación por falla) y la base de datos se particiona por región, con una instancia local en Medellín además de la de Bogotá. Ver diagramas completos en los anexos (`to-be-aplicaciones-final.drawio` y `to-be-tecnologia-final.drawio`).

### 3.3 Controles de seguridad integrados
El ejercicio de clase sobre RedExpress no cuenta con un Taller 5 (análisis STRIDE) construido específicamente para este caso — el ejemplo guiado de STRIDE del curso usa un sistema académico distinto. Por eso este TO-BE no declara controles de seguridad específicos del Taller 5; queda marcado como pendiente en el diagrama de tecnología (`to-be-tecnologia-final.drawio`). En la aplicación a un cliente real, aquí se debe declarar explícitamente qué mitigaciones STRIDE protegen los componentes que el TO-BE modifica.

---

## 4. Análisis de beneficios y riesgos

| Mejora / Solución | Beneficio de negocio | Beneficio tecnológico/seguridad | Riesgo, limitación o dependencia de implementación |
|---|---|---|---|
| Balanceador redundante (activo-pasivo) | Continuidad de la operación en picos de demanda (ej. fin de año) | Elimina el punto único de falla del balanceador | Depende de la aprobación de presupuesto adicional (~USD 400/mes) para la segunda instancia |
| BD particionada por región | Mejor experiencia de rastreo en tiempo real para clientes fuera de Bogotá | Reduce la latencia de escritura y la dependencia de un único nodo | Migración con ventana de mantenimiento; riesgo de downtime parcial e inconsistencia durante la sincronización inicial |
| Módulo de rutas en Medellín | La región puede crecer en volumen de envíos sin saturar Bogotá | Reduce la dependencia crítica de un único punto de procesamiento de rutas | Depende de contratar o reasignar personal técnico local que opere y mantenga el módulo |

La matriz de brechas completa, con capacidades de negocio y paquetes de trabajo (WP1 · Continuidad de la plataforma, WP2 · Rutas y datos regionales), está en el anexo `matriz-brechas.xlsx`.

---

## Anexos
- Diagrama TO-BE de Aplicaciones: `entrega/to-be-aplicaciones-final.drawio`
- Diagrama TO-BE de Tecnología: `entrega/to-be-tecnologia-final.drawio`
- Matriz de brechas (Gap Analysis): `entrega/matriz-brechas.xlsx`
- Trabajo de clase y matriz de decisión ponderada completa: `clase/notas.md`

---

## Nota de alcance

Este documento desarrolla la actividad de Opportunities & Solutions **sobre el caso base RedExpress** trabajado en clase (Talleres 3 y 4), no sobre un cliente real externo con Talleres 5 (STRIDE) y 6 (normatividad) propios. Por eso las secciones 1 y 3.3 no incluyen brechas de seguridad ni de cumplimiento normativo — el diagnóstico de RedExpress solo cubre lo evidenciado en el Taller 4 de infraestructura, tal como aclara la propia guía del taller. Si el docente pide la versión con el cliente real del equipo, este documento debe rehacerse consolidando además los hallazgos de los Talleres 5 y 6 de ese cliente.

**Formato de entrega:** documento único de máximo 6 páginas + anexos, entregado como PDF con nombre `EquipoX_Mejora_Arquitectura.pdf`.

---

_Este documento hace parte de la entrega del Taller 7 (Opportunities & Solutions) del curso AREM - Universidad de La Sabana._
