# Procedimiento de Actualización y Revisión de la Arquitectura

## Cliente

**Ban100 S.A. (Bancien S.A.)** — establecimiento bancario comercial, NIT `900.200.960-9`, Bogotá D.C.

## Integrantes del equipo

- Santiago Barrera Rueda (santiagobarru@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial

---

## Propósito de este documento

El [plan de implementación](./plan-implementacion.md) ejecuta un cambio ya decidido y el [plan de gobernanza](./plan-gobernanza.md) supervisa esa ejecución. Este documento cubre lo que viene **después de diciembre de 2027**, cuando el roadmap termine: cómo se mantiene viva la arquitectura de Ban100 cuando aparezca una necesidad que este curso no previó.

Es la pieza que evita que el TO-BE de 2027 se convierta, en 2029, en el nuevo AS-IS rígido que hoy estamos corrigiendo.

---

## Disparadores de cambio

| Disparador | Ejemplo concreto para Ban100 |
|---|---|
| **Nueva regulación** | Publicación del MRAE v3.1 o superior por el MinTIC; una nueva circular externa de la SFC que modifique los requisitos de continuidad de la CE 008 de 2023; una reforma al régimen de libranza (Ley 1527 de 2012) que cambie el flujo de visación o el tope de descuento |
| **Cambio de proveedor tecnológico** | Terminación del contrato con **Truora** (biometría y firma, Ley 527 de 1999) o cambio del proveedor de modelos de lenguaje que soporta el Ban-I Bot. Por el estándar de abstracción definido en gobernanza, debe poder sustituirse sin rediseñar el Orquestador, pero sí exige revisar la cadena probatoria del pagaré |
| **Incidente de seguridad** | Materialización de cualquiera de las amenazas T1 a T8 del Taller 5, en particular una fuga de PII desde el Cliente 360 o hacia el proveedor de LLM (T4, T7). Todo incidente con PII dispara revisión de arquitectura, no solo respuesta a incidentes |
| **Crecimiento inesperado de demanda** | Firma de un convenio de libranza con una pagaduría de alto volumen (por ejemplo, una gobernación completa) que multiplique la concurrencia esperada en el Adaptador B2G |
| **Pérdida o vencimiento de un convenio de alto volumen** | Es el **riesgo R8** de la matriz, que se decidió no convertir en fase técnica: se gestiona aquí. El vencimiento de contratos como `CO1.PCCNTR.6460767` (2024–2026) obliga a revisar la concentración del portafolio antes de renovar |
| **Una pagaduría adelanta su adopción MRAE** | Un municipio del Grupo Territorial 3, 4 o 5 publica APIs antes de su plazo. No es un problema sino una oportunidad: debe pasar de la vía asíncrona a la vía rápida del Adaptador, y eso cambia su configuración de integración |
| **Degradación sostenida de una métrica de gobierno** | M1 por debajo del 60 %, M2 por debajo del 95 % dos meses seguidos o M3 por encima de 10 días hábiles de promedio trimestral |

---

## Proceso de cambio

| Paso | Qué ocurre | Quién | Plazo |
|---|---|---|---|
| **1. Radicación** | Cualquier líder de área, el CISO, el Oficial de Protección de Datos o el Líder de Convenios B2G radica la solicitud describiendo el disparador y el impacto observado. No se admiten solicitudes sin disparador identificado | Quien detecta | — |
| **2. Clasificación** | El Arquitecto líder clasifica: **menor** (no altera principios ni capas), **mayor** (altera una capa o un componente del TO-BE) o **estructural** (altera un principio) | Arquitecto líder | 2 días hábiles |
| **3. Evaluación** | Se contrasta contra los cuatro objetivos estratégicos de la Ficha (**O1** cobertura territorial, **O2** calidad de cartera y AAA ESG, **O3** originación < 15 min, **O4** cumplimiento) y contra los cinco principios P1–P5 del plan de gobernanza. Si contradice un principio, se evalúa también si el principio sigue siendo válido | Arquitecto líder + líder del área afectada | 5 días hábiles |
| **4. Dictamen** | El Comité de Arquitectura aprueba, rechaza o devuelve con condiciones. El CISO y el Oficial de Protección de Datos conservan **veto** sobre lo que toque seguridad o PII | Comité de Arquitectura | 10 días hábiles (5 si es bloqueante) |
| **5. Registro** | Toda decisión aprobada de tipo mayor o estructural se documenta como **ADR** con el formato de este documento y se publica en el repositorio de AE | Arquitecto líder | 3 días hábiles tras el dictamen |
| **6. Actualización de modelos** | Se actualizan el tablero integrado, las vistas ArchiMate y la matriz de riesgos. Una ADR aprobada cuyos modelos no se actualizaron es una no conformidad (criterio C1 de gobernanza) | Arquitectura Empresarial | Antes del siguiente comité |

**Criterio de rechazo automático:** una solicitud que exija a una pagaduría pública publicar una API como condición para operar se rechaza sin pasar a comité, por contradecir el principio **P1**. Es el error que este proyecto existe para no repetir.

---

## Registro de decisiones (ADR)

Las dos decisiones siguientes son reales: el equipo las tomó durante los Talleres 4 a 7 y están sustentadas en los informes de esos talleres.

### ADR-01

| Campo | Contenido |
|---|---|
| **Título** | Adoptar un Adaptador B2G de Dos Velocidades en lugar de una integración única con las pagadurías |
| **Estado** | **Aceptada** |
| **Fecha de propuesta** | 10 de octubre de 2026 (Taller 7, lluvia de ideas y priorización) |
| **Fecha de dictamen** | 17 de octubre de 2026 (priorización de SOL-1 en `mejora-arquitectura.md`) |
| **Contexto** | El 94 % de la colocación de Ban100 es libranza y el 98,3 % de ese segmento depende de pagadurías públicas. El Taller 4 cuantificó con el modelo `MRAE.ADM.01` del MinTIC que los Grupos Territoriales 3, 4 y 5 —donde Ban100 opera entre 850 y 880 municipios— tardarán entre **40 y 47 meses** en alcanzar el 100 % de los lineamientos de interoperabilidad. La meta de negocio es originar en menos de 15 minutos. |
| **Problema** | Una interfaz de integración única obliga a elegir entre dos pérdidas: servir solo a las pagadurías maduras (y renunciar a la cobertura territorial, objetivo O1) o nivelar por la contraparte más lenta (y renunciar a la velocidad, objetivo O3). |
| **Decisión** | Construir **un solo adaptador con dos vías**: una vía rápida síncrona (API REST / X-Road con Lenguaje Común) para las pagadurías de Grupos G1–G2, y una vía asíncrona (RPA + motor ETL + Portal Web de Autogestión) para las de G3–G5. La vía que usa cada pagaduría es configuración, no código nuevo. |
| **Alternativas consideradas** | **(a) Esperar a que las pagadurías adopten el MRAE** — descartada: el propio modelo del MinTIC da 40 a 47 meses para los grupos donde está la mayor parte de la operación, y la meta es 2027. **(b) Exigir API como cláusula del convenio** — descartada: Ban100 no es sujeto obligado ni autoridad, no tiene el poder contractual para imponerlo, y hacerlo dejaría fuera el 55 % de la cartera que está en poblaciones de menos de 500.000 habitantes. **(c) Tercerizar la visación en un BPO manual** — descartada: no baja el ciclo de 15 minutos y traslada PII a un tercero, lo que agrava la amenaza T4. **(d) Un único canal asíncrono para todas** — descartada: penalizaría a las pagadurías G1–G2 que ya pueden responder en tiempo real, desaprovechando la única parte del ecosistema que sí está lista. |
| **Consecuencias** | **(+)** Cobertura y velocidad al mismo tiempo, sin depender del calendario del Estado; entrega incremental desde la Fase 2. **(+)** Cierra la brecha G1 y mitiga el riesgo R1 (Nivel 12) y la amenaza T8. **(−)** Hay **dos caminos de integración que mantener, probar y monitorear de forma permanente**, no transitoria: el costo operativo del adaptador no desaparece cuando las pagadurías maduren, porque siempre habrá rezagadas. **(−)** La vía asíncrona depende de que las pagadurías efectivamente usen el Portal de Autogestión; si no lo adoptan, el analista de visación permanece en el circuito y la ganancia de tiempo se diluye (riesgo tratado en la gestión del cambio del plan de implementación). **Trade-off aceptado:** se asume duplicidad permanente de mantenimiento a cambio de no quedar sujetos al calendario de modernización del Estado. |

### ADR-02

| Campo | Contenido |
|---|---|
| **Título** | Desacoplar el Core Bancario con un Bus de Eventos CDC en lugar de reemplazarlo o migrarlo |
| **Estado** | **Aceptada** |
| **Fecha de propuesta** | 10 de octubre de 2026 (Taller 7, SOL-2) |
| **Fecha de dictamen** | 17 de octubre de 2026 |
| **Contexto** | El Taller 4 identificó (riesgo R2) que el microservicio de Originación se comunica de forma **síncrona** con el Core Bancario On-Premise en Bogotá. El checklist 6 del Taller 6 marcó este punto como ⚠️ Parcial frente a la Circular Externa 008 de 2023 de la SFC, que exige continuidad sin dependencia de un único sistema. Las ventanas de mantenimiento son de 30 minutos nocturnos. |
| **Problema** | La originación digital, que es el 100 % del canal de libranza, se detiene cada vez que el Core no responde: durante una ventana de mantenimiento, una ventana de cierre o una degradación. Una operación «100 % digital» con una dependencia dura de un sistema heredado no es resiliente. |
| **Decisión** | Interponer un **Bus de Eventos con captura de cambios (CDC) de menos de 500 ms**, con **Circuit Breaker** hacia el Core y **BCP/DRP automatizado**. El Core sigue siendo el sistema de registro contable; deja de estar en el camino crítico de la respuesta al cliente. |
| **Alternativas consideradas** | **(a) Reemplazar el Core por un core bancario moderno** — descartada: el Taller 0 lo excluyó explícitamente del alcance, y el costo y el riesgo son desproporcionados frente a un problema cuya causa es el acoplamiento, no el Core en sí. **(b) Base de datos replicada por lotes** — descartada: es un patrón de sincronización diferida que deja la latencia en horas; no sirve para una meta de 15 minutos. **(c) Aumentar el *timeout* y reintentar** — descartada: no elimina la indisponibilidad durante las ventanas, solo convierte el error en espera, lo que empeora la experiencia justo donde se mide la meta. **(d) Migrar el Core a nube pública** — descartada: no ataca la causa (el acoplamiento seguiría siendo síncrono) y contradice la decisión de retirar «nube como primera opción» como principio absoluto. |
| **Consecuencias** | **(+)** La originación sobrevive a las ventanas de mantenimiento del Core; habilita la meta de < 15 minutos y cierra el parcial 6 del checklist frente a la CE 008 de 2023. **(+)** Cierra la brecha G2 y mitiga el riesgo R5 (Nivel 8). **(−)** Introduce **consistencia eventual**: una consulta de saldo hecha inmediatamente después del desembolso puede no reflejarlo todavía. Es el riesgo **R12**, que la matriz acepta de forma explícita y justificada. **(−)** Añade una pieza de infraestructura que el equipo del Core no opera hoy: exige capacitación, monitoreo del *lag* del bus y pruebas periódicas de DRP que antes no existían. **Trade-off aceptado:** se cambia consistencia fuerte inmediata por disponibilidad de la originación, porque el negocio pierde más por una solicitud que no se puede tomar que por un saldo que se actualiza medio segundo después. |

---

## Revisión periódica completa

Más allá de los disparadores puntuales, la arquitectura se revisa completa en dos cadencias:

| Revisión | Frecuencia | Alcance |
|---|---|---|
| **Revisión integral de arquitectura** | **Anual**, alineada con la actualización del PETI (`MGGTI.LI.ES.02`, que exige un PETI a cuatro años con actualización anual) | Se contrasta el TO-BE vigente contra el estado real del negocio: los cuatro objetivos de la Ficha, los cinco principios, el checklist normativo completo y el nivel de madurez del instrumento de 300 ítems (MAE, MGGTI, MGPTI) |
| **Revisión de la matriz de riesgos** | **Semestral** | Se recalcula impacto y probabilidad de los 12 riesgos, se cierran los mitigados y se incorporan los nuevos. El riesgo aceptado R12 se reevalúa de forma obligatoria en cada corte: *aceptado* no significa *olvidado* |
| **Revisión de principios** | **Anual, dentro de la revisión integral** | Cada principio debe seguir permitiendo decir «no» a algo concreto. Un principio que en un año no sirvió para rechazar ninguna propuesta es un principio decorativo y se retira |

---

## Referencias

- **TOGAF — Architecture Change Management (Fase H del ADM):** origen de la distinción entre cambio de simplificación, incremental y de rearquitectura, y del criterio de disparadores.
- **Nygard, M. (2011).** *Documenting Architecture Decisions*: formato ADR con contexto, decisión y consecuencias.
- **MinTIC — MRAE v3.0 (Decreto 767 de 2022):** `MAE.LI.PA.05` (AS-IS/TO-BE/Gap), `PA.07` (hoja de ruta en el PETI), `PA.08` (repositorio de AE) y `MGGTI.LI.ES.02` (actualización anual del PETI).
- **Superintendencia Financiera de Colombia — Circular Externa 008 de 2023:** continuidad del negocio, base del contexto de la ADR-02.
- Insumos propios: [informe de infraestructura (Taller 4)](../04-infraestructura/informe.md), [checklist normativo (Taller 6)](../06-normatividad/informe.md) y [mejora de arquitectura (Taller 7)](../07-oportunidades-soluciones/mejora-arquitectura.md).

---

_Este documento hace parte de la entrega final del Taller 9 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
