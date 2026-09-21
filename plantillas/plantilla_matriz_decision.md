# Matriz de Decisión Ponderada

Use una matriz por cada brecha que tenga **más de una solución posible**. Guía y ejemplo completo: sección 2.1 de la [guía paso a paso](../clase/guia_paso_a_paso_opportunities_solutions.md).

---

## Brecha que se decide

_Brecha (con el taller de origen que la evidencia):_

---

## Paso 1 — Problema en términos de impacto

_Qué se pierde, cuándo y cuánto. Sin nombrar ninguna herramienta ni escribir «necesitamos»:_

---

## Paso 2 — Último momento responsable para decidir

| Dato | Valor |
|---|---|
| Fecha en que el problema empieza a doler | |
| Tiempo que necesita la opción más probable (implementación + pruebas) | |
| **Último momento responsable** (fecha − tiempo necesario) | |
| Fecha de hoy y días que quedan | |

---

## Paso 3 — Criterios, pesos y escala

Los pesos los define o valida el negocio (no solo el equipo técnico) y **suman 100**. En la escala 1-5, 5 siempre es lo más favorable.

| Criterio | Peso (%) | Qué significa 5 | Qué significa 1 |
|---|---|---|---|
| | | | |
| | | | |
| | | | |
| | | | |
| **Total** | **100** | | |

_Por qué esos pesos:_

_Criterio eliminatorio (opcional): «toda opción con ___ menor a ___ se descarta»:_

---

## Paso 4 — Opciones (2 a 3, al menos una radicalmente distinta)

| Opción | Descripción |
|---|---|
| A | |
| B | |
| C | |

---

## Paso 5 — Consejo consultado

| A quién (quien sabe / a quien le afecta) | Qué aportó | Qué opción afecta |
|---|---|---|
| | | |
| | | |

---

## Paso 6 — Puntajes con justificación

Cada celda lleva el puntaje **y** su razón (cita la escala del Paso 3 o el dato del Paso 5).

| Opción | Criterio 1 | Criterio 2 | Criterio 3 | Criterio 4 |
|---|---|---|---|---|
| A | | | | |
| B | | | | |
| C | | | | |

**Totales ponderados** (puntaje × peso, sumado):

| Opción | Cálculo | Total |
|---|---|---|
| A | | |
| B | | |
| C | | |

**Sensibilidad:** cambie los pesos a un escenario alternativo razonable (por ejemplo, priorizando costo). ¿Se invierte el resultado?

| Escenario de pesos | Total A | Total B | Total C | ¿Gana la misma opción? |
|---|---|---|---|---|
| Pesos del negocio | | | | |
| Escenario alternativo: | | | | |

_Si dos opciones quedan a menos de 0,3 puntos, trátelas como empate y decida por el criterio más crítico o por el riesgo de reversión._

---

## Paso 7 — Decisión

- **Decisión:**
- **Trade-off aceptado** (qué se sacrifica y a cambio de qué):
- **Alternativas descartadas y su razón:**

---

## Paso 8 — Reevaluación

_Cuándo o ante qué disparador se vuelve a mirar esta decisión:_

---

## Registro de uso de IA (solo si usó una herramienta de IA)

La IA propone; el equipo justifica y decide ([guía, sección 2.2](../clase/guia_paso_a_paso_opportunities_solutions.md)). Anonimice los datos del cliente o confirme que autoriza usar la herramienta.

| Paso | Qué se le pidió a la IA | Qué propuso | Dato verificado o recalculado | Qué cambió el equipo |
|---|---|---|---|---|
| | | | | |
| | | | | |

- [ ] Puntué por mi cuenta antes de comparar con la IA (evita el anclaje).
- [ ] Verifiqué o recalculé toda cifra y afirmación de la IA que entró a la matriz.
- [ ] Los pesos los fijó o validó el negocio, no la IA.

---

_Esta decisión es el borrador de una ADR: en el Taller 9 se formaliza su registro (Contexto, Problema, Decisión, Alternativas, Consecuencias)._
