# Referencias Bibliográficas del Taller

Este archivo contiene las fuentes consultadas para el desarrollo del taller, tanto para el componente técnico como para la investigación complementaria.

## Taller
Taller 7 - Opportunities & Solutions (TO-BE de RedExpress)

---

## Referencias utilizadas

1. Microsoft. *Deployment Stamps pattern — Azure Architecture Center*. Microsoft Learn. https://learn.microsoft.com/azure/architecture/patterns/deployment-stamp — patrón de referencia para replicar un módulo (como el motor de rutas) en varias regiones de forma independiente, aplicado a la propuesta del Motor de Rutas - Medellín.
2. Microsoft. *Sharding pattern — Azure Architecture Center*. Microsoft Learn. https://learn.microsoft.com/azure/architecture/patterns/sharding — fundamento técnico para la partición de la base de datos por región (geo-sharding), usado para justificar la BD particionada Bogotá/Medellín.
3. Microsoft. *Geodes pattern — Azure Architecture Center*. Microsoft Learn. https://learn.microsoft.com/azure/architecture/patterns/geodes — patrón complementario de distribución geográfica de instancias que sirvieron como respaldo (backplane replicado) para el diseño del TO-BE de tecnología.
4. YugabyteDB. *Latency-optimized geo-partitioning*. Documentación técnica. https://docs.yugabyte.com/stable/develop/build-global-apps/latency-optimized-geo-partition/ — evidencia cuantitativa de reducción de latencia al particionar datos por región, usada para justificar el beneficio esperado de la BD particionada.
5. Kovtun, V.; Yukhimchuk, M.; Dubovoi, V.; Leshchenko, Y.; Lesko, V. *Routing algorithms in urban logistics for last mile delivery optimization*. CEUR Workshop Proceedings, 2026. https://ceur-ws.org/Vol-4126/paper8.pdf — investigación académica sobre algoritmos de enrutamiento urbano para última milla, referenciada como respaldo del sector para la mejora del módulo de rutas regional.
6. Microsoft. *Cloud Design Patterns — Azure Architecture Center*. Microsoft Learn. https://learn.microsoft.com/azure/architecture/patterns/ — catálogo general de patrones de arquitectura de nube usado como referencia transversal para justificar la redundancia del balanceador de carga (patrón de alta disponibilidad activo-pasivo).

---

## Recomendaciones

- Usa formato APA o IEEE para citar si el docente lo exige en el documento formal.
- Si usas inteligencia artificial para redactar o investigar, cítalo como "Fuente asistida por IA: Claude (Anthropic), septiembre 2026".

---

_Este archivo forma parte de la entrega académica del curso AREM - Universidad de La Sabana._
