# Prompts para usar IA como copiloto en el Taller 7

Estos prompts siguen el método de la [guía paso a paso](../clase/guia_paso_a_paso_opportunities_solutions.md) (secciones 1 a 4 y 2.2). Sirven para **acelerar** el trabajo, no para reemplazarlo: la IA propone; el equipo verifica, justifica y decide.

## Antes de empezar: reglas de uso

1. **Anonimice.** No pegue nombres del cliente, cifras internas ni datos personales. Sustitúyalos por etiquetas (`[CLIENTE]`, `[SISTEMA_A]`, `[REGION_1]`) o confirme por escrito que el cliente autoriza usar la herramienta.
2. **Puntúe primero usted.** En los pasos de puntajes y de decisión, haga su propio trabajo antes de pedirle nada a la IA; si no, se ancla a lo que ella diga.
3. **Los pesos no se delegan.** Los fija el negocio. La IA puede probar escenarios, no decidir qué importa.
4. **Verifique y recalcule.** Toda cifra, plazo o costo que la IA dé es una hipótesis. Contraste con quien sabe (proveedor, líder técnico, cliente) y recalcule cualquier cuenta.
5. **Registre el uso** en la tabla "Registro de uso de IA" de la [plantilla de matriz de decisión](plantilla_matriz_decision.md): qué pidió, qué propuso la IA, qué verificó y qué cambió.

Cómo usar cada prompt: copie el bloque, reemplace lo que está entre `[CORCHETES]` con su información (anonimizada) y péguelo en la herramienta. Cada prompt trae una lista **"Qué revisar"** para evaluar la respuesta antes de usarla.

> **Cláusula que conviene mantener en casi todos los prompts:** «No inventes cifras, costos ni plazos. Si necesitas un dato que no te di, dime cuál falta y marca tus supuestos como SUPUESTO.» Reduce (no elimina) las respuestas inventadas.

---

## Parte 1 · Diagnóstico

### Prompt 1 · Clasificar hallazgos como brechas con origen

Usa el marco de la sección 1 de la guía (tipos de brecha y taller de origen).

```text
Actúa como arquitecto empresarial. Te doy los hallazgos de mi diagnóstico de [CLIENTE_ANONIMIZADO], un [TIPO_DE_NEGOCIO].

Hallazgos:
[PEGUE AQUÍ SUS HALLAZGOS, uno por línea, indicando de qué taller o entregable sale cada uno]

Tarea:
1. Clasifica cada hallazgo en un tipo de brecha: Funcional/Aplicaciones (Taller 3), Técnica/Infraestructura (Taller 4), Seguridad (Taller 5) o Cumplimiento (Taller 6).
2. Devuélvelo en una tabla: Hallazgo | Tipo de brecha | Taller de origen | ¿Tiene evidencia concreta? (sí/no).
3. Señala los hallazgos que NO se pueden rastrear a un entregable anterior: esos son opiniones, no brechas, y dime qué evidencia faltaría para convertirlos en brechas.
No inventes hallazgos nuevos.
```

**Qué revisar:** que no haya reclasificado a su gusto un hallazgo que sí tiene origen, y que los "sin evidencia" realmente lo sean. Complete usted la evidencia que falte.

---

## Parte 2 · Armar la solución

### Prompt 2 · Lluvia de ideas sin censura

```text
Actúa como consultor de arquitectura empresarial. Contexto: [CLIENTE_ANONIMIZADO] es [DESCRIPCIÓN EN 2-3 LÍNEAS]. Sus brechas diagnosticadas son:
[LISTA DE BRECHAS]

Genera 10 ideas de mejora SIN filtrar ni priorizar. Mezcla: mejoras técnicas (infraestructura, aplicaciones, datos, seguridad) y mejoras de proceso o de comunicación con el cliente que no requieran tocar la infraestructura.
Devuélvelas en tabla: # | Idea | Tipo (Técnica / Proceso / Comunicación) | Brecha que atendería.
Marca con "SIN BRECHA" las ideas que no atiendan ninguna brecha de mi lista.
```

**Qué revisar:** descarte las ideas "SIN BRECHA" o conviértalas en hallazgos a investigar. Recuerde: en su cliente real, una idea de proceso que responde a un problema recurrente de las entrevistas sí se prioriza.

### Prompt 3 · Una opción radicalmente distinta (Paso 4)

```text
Estoy decidiendo cómo cerrar esta brecha: [BRECHA].
Restricciones reales: fecha límite [FECHA], presupuesto [RANGO O "limitado"], equipo [TAMAÑO Y PERFIL].
Ya tengo estas opciones: [OPCIÓN A], [OPCIÓN B].

Propón 3 formas RADICALMENTE distintas de cerrar la brecha (no variantes de A o B). Al menos una debe ser "aceptar el riesgo y solo reducirlo o detectarlo antes". Para cada una indica: en qué consiste, los supuestos que tiene, y qué dato habría que verificar con quien sabe antes de considerarla una opción real.
No inventes costos ni plazos: si los necesitas, dime qué dato falta.
```

**Qué revisar:** cada idea es una **hipótesis**. Solo pasa a ser opción cuando la verifica con quien sabe (proveedor, líder técnico) y puede puntuarla con datos.

### Prompt 4 · Criterios y escalas (Paso 3)

Usa la estructura de la tabla del Paso 3 de la guía. **No** le pida pesos.

```text
Mi problema, enunciado en términos de impacto, es: [ENUNCIADO DEL PROBLEMA].
Las opciones que voy a comparar son: [OPCIONES].

Propón entre 4 y 5 criterios de decisión relevantes para ESTE problema. Para cada criterio define una escala de 1 a 5 en la que 5 SIEMPRE es lo más favorable (más disponible, más barato, más simple, más rápido), describiendo con hechos medibles qué significa un 5, un 3 y un 1.
Devuélvelo en tabla: Criterio | Qué mide | 5 significa | 3 significa | 1 significa.
NO propongas pesos: los define el negocio.
```

**Qué revisar:** que las escalas sean medibles (dólares, semanas, horas de caída) y no adjetivos ("bueno", "malo"). Ajuste los rangos a la realidad de su cliente y asigne usted los pesos con el negocio.

### Prompt 5 · Preparar el consejo (Paso 5)

```text
Voy a decidir entre estas opciones: [OPCIONES] para resolver: [ENUNCIADO DEL PROBLEMA].
Ayúdame a preparar la consulta del Paso 5: dime a qué tipos de personas debería consultar (quien SABE de la tecnología o el proceso, y quien LE AFECTA la decisión) y redacta 3 preguntas concretas para cada una, orientadas a obtener datos verificables (costos, plazos, umbrales de lo tolerable), no opiniones.
Devuélvelo en tabla: A quién | Por qué | Preguntas.
```

**Qué revisar:** haga usted las consultas de verdad y registre los datos: de ahí salen los puntajes justificados.

---

## Parte 3 · Tomar la decisión

### Prompt 6 · Contrastar mis puntajes (Paso 6) — solo después de puntuar usted

```text
Ya puntué la siguiente matriz por mi cuenta (escala 1-5, 5 = más favorable). Necesito una segunda opinión, no que la rehagas.

Criterios y pesos (definidos por el negocio): [CRITERIO 1: PESO %], [CRITERIO 2: PESO %], ...
Mis puntajes con su justificación:
[PEGUE SU TABLA: Opción | Criterio | Puntaje | Razón y dato en que me apoyo]

Tarea:
1. Marca los puntajes cuya justificación NO sostiene el número (por ejemplo, un dato que corresponde a otro rango de la escala).
2. Marca las justificaciones que no citan ningún dato verificable.
3. Señala inconsistencias entre celdas (por ejemplo, dos opciones con el mismo dato pero distinto puntaje).
No cambies mis puntajes ni propongas cifras nuevas: solo señala dónde falla mi razonamiento. Si te falta un dato, dime cuál.
```

**Qué revisar:** decida usted si acepta cada observación. Si cambia un puntaje, anote el dato que lo justifica y regístrelo en el registro de uso de IA.

### Prompt 7 · Abogado del diablo y sensibilidad (Paso 7)

```text
Esta es mi matriz de decisión ponderada.
Criterios y pesos: [CRITERIOS Y PESOS %]
Puntajes: [TABLA DE PUNTAJES]
Decisión tomada: [OPCIÓN ELEGIDA] con total [TOTAL].

Ataca mi decisión:
1. Lista los 3 supuestos que, si fallan, la invalidarían, y qué evidencia buscarías para confirmarlos.
2. Propón 3 escenarios de pesos alternativos y razonables (por ejemplo, priorizando costo, o priorizando disponibilidad) y calcula el total de cada opción en cada escenario, MOSTRANDO EL CÁLCULO paso a paso (puntaje × peso).
3. Dime con qué peso, del criterio más importante, cambiaría la opción ganadora.
4. Dime qué argumento usaría un opositor a mi decisión ante un comité.
```

**Qué revisar:** **recalcule usted cada total.** Las herramientas se equivocan en aritmética y en umbrales (en la guía, una IA afirma que con 50 % de disponibilidad ganaría B y es falso). Lo valioso es la pregunta y los supuestos; la cifra la confirma usted.

### Prompt 8 · Riesgos y dependencias de la opción elegida (Parte 4)

```text
La opción elegida es [OPCIÓN] para cerrar la brecha [BRECHA] en [CLIENTE_ANONIMIZADO]. Contexto: [RESTRICCIONES].

Lista riesgos, limitaciones y dependencias que podrían impedir o retrasar su implementación, en tabla: Riesgo o dependencia | Causa | Impacto | Probabilidad (alta/media/baja) | Mitigación posible.
Cubre al menos: presupuesto, personal y habilidades, ventanas de mantenimiento o downtime, dependencia de terceros, seguridad y cumplimiento normativo.
Marca como SUPUESTO todo lo que asumas sobre el cliente.
```

**Qué revisar:** confirme con el cliente cada SUPUESTO; agregue los riesgos que ya tenga evidenciados en los Talleres 5 y 6.

### Prompt 9 · Borrador de ADR (Registro)

```text
Convierte esta decisión en un borrador de ADR (Architecture Decision Record) con estos campos: Título, Estado (Propuesta), Contexto, Problema, Decisión, Alternativas consideradas (cada una con la razón por la que se descartó), Consecuencias (incluye las negativas y la deuda que se acepta), Trade-off aceptado.

Usa SOLO la información que te doy; no agregues datos, cifras ni alternativas nuevas.
Problema: [ENUNCIADO]
Opciones evaluadas y totales: [OPCIONES Y TOTALES]
Decisión: [OPCIÓN] por estas razones: [RAZONES]
Datos verificados: [DATOS DEL PASO 5]
Se vuelve a evaluar cuando: [DISPARADOR O FECHA]
```

**Qué revisar:** que cada alternativa descartada tenga su razón, que las consecuencias incluyan lo negativo y que **ninguna cifra sea nueva**: todo debe salir de su matriz. En el Taller 9 este borrador se formaliza.

---

## Parte 4 · Capacidades y paquetes de trabajo

### Prompt 10 · Capacidades y paquetes (sección 4.1)

```text
Estas son las brechas que voy a cerrar en [CLIENTE_ANONIMIZADO]: [BRECHAS].
Estos son sus procesos clave (de la ficha del cliente): [PROCESOS CLAVE].

1. Propón entre 5 y 8 capacidades de negocio (verbo + objeto, SIN nombres de sistemas ni tecnologías). Recuerda: capacidad = qué debe saber hacer la empresa; proceso = cómo lo hace; aplicación = qué sistema lo soporta.
2. Para cada capacidad, propón una madurez AS-IS de 1 a 5 (1 = ad hoc y frágil, 3 = funciona con fallas conocidas, 5 = fiable, medida y escalable) SOLO si mis hallazgos la respaldan; si no, escribe "sin evidencia".
3. Conecta cada brecha con la capacidad que más mejora y propón paquetes de trabajo (agrupa las brechas que mejoran la misma capacidad).
Tabla: Capacidad | Madurez AS-IS y evidencia | Brechas que la afectan | Paquete de trabajo.
```

**Qué revisar:** que no haya nombres de sistemas en las capacidades, que cada madurez cite un hallazgo real y que el TO-BE de madurez lo defina usted con el cliente.

---

## Cuando una opción incluye IA

### Prompt 11 · Criterios adicionales para una opción con IA

```text
Una de las opciones que evalúo es [DESCRIPCIÓN DE LA SOLUCIÓN CON IA: por ejemplo, un asistente que responde consultas de clientes].
Mi matriz actual tiene estos criterios: [CRITERIOS].

1. Propón criterios ADICIONALES específicos de una solución con IA, con escala 1-5 (5 = más favorable): autonomía y supervisión humana, fiabilidad (qué pasa si se equivoca), costo variable por uso, dependencia del proveedor del modelo.
2. Evalúa si se cumplen las tres condiciones de la "tríada letal": (a) acceso a datos privados, (b) exposición a contenido no confiable, (c) capacidad de comunicar hacia afuera. Indica cuál de las tres se podría romper con el menor costo.
3. Dime qué acciones del agente deberían exigir aprobación humana.
Marca como SUPUESTO todo lo que asumas.
```

**Qué revisar:** contraste con el ejemplo de código del Taller 5 y con el [patrón de sistemas agénticos](https://github.com/CesarAVegaF312/AREM-ArchiMate/blob/main/patron_sistemas_agenticos.md). La decisión de qué acciones exigen aprobación es suya y del cliente.

---

## Revisión final

### Prompt 12 · Revisor del entregable

```text
Actúa como revisor exigente de un documento de mejora de arquitectura. Te doy mi documento y la lista de verificación. Evalúa cada ítem como CUMPLE, PARCIAL o NO CUMPLE, citando la parte del documento que lo respalda o indicando qué falta. No reescribas mi documento.

Lista de verificación:
- Respondí las tres preguntas orientadoras del diagnóstico (fricción, problemas recurrentes, vulnerabilidades y riesgos previos).
- Consolidé las brechas de los Talleres 3, 4, 5 y 6.
- Hice una lluvia de ideas de al menos 6 mejoras antes de priorizar 2-3.
- Cada elemento del TO-BE está trazado a una brecha del AS-IS.
- Cada brecha con varias soluciones tiene su matriz de decisión: problema en términos de impacto, último momento responsable, criterios con escala, pesos definidos por el negocio, 2-3 opciones (una radicalmente distinta), puntajes justificados, sensibilidad y trade-off aceptado.
- El análisis incluye riesgos y dependencias, no solo beneficios.
- Las brechas están agrupadas por capacidad y organizadas en paquetes de trabajo.

Mi documento:
[PEGUE SU DOCUMENTO, ANONIMIZADO SI CORRESPONDE]
```

**Qué revisar:** use el resultado como lista de pendientes, no como calificación; el docente evalúa con la rúbrica del taller.

---

## Errores frecuentes al usar estos prompts

| Error | Por qué es un problema | Cómo evitarlo |
|---|---|---|
| Pegarle a la IA los datos reales del cliente | Puede violar la confidencialidad o la Ley 1581 si hay datos personales | Anonimice o pida autorización por escrito |
| Pedirle los pesos | Los pesos reflejan lo que le importa al negocio, no al modelo | Defínalos con el cliente |
| Copiar los puntajes que propone | Se ancla a un número sin datos que lo respalden | Puntúe primero usted (Prompt 6) |
| Aceptar cifras o cálculos sin revisarlos | Puede afirmar con aplomo un dato inventado o un umbral equivocado | Recalcule y contraste con quien sabe |
| Usar una sola respuesta como definitiva | Las respuestas varían y tienden a favorecer lo más común | Repita el prompt, pida contra-opinión y compare |
| No registrar el uso | La decisión deja de ser rastreable | Complete el registro de uso de IA de la plantilla |
