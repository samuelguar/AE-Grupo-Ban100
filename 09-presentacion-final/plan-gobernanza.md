# Plan de Gobernanza de la Implementación

## Cliente

**Ban100 S.A. (Bancien S.A.)** — establecimiento bancario comercial, NIT `900.200.960-9`, Bogotá D.C.

## Integrantes del equipo

- Santiago Barrera Rueda (santiagobarru@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial

---

## Propósito de este documento

El **Comité de Arquitectura Empresarial** de Ban100 (homologado a `MAE.LI.PA.03` del MRAE v3.0) supervisa la ejecución de las cuatro fases del [plan de implementación](./plan-implementacion.md) mediante una puerta de fase: ninguna fase se da por cerrada sin que su resultado visible haya sido comprobado por alguien ajeno a TI.

Cuando una fase se desvía del diseño TO-BE aprobado en el Taller 7, no se detiene la obra: se radica una excepción, el comité la dictamina en un plazo acotado y, si la aprueba, la excepción queda registrada como ADR en el [procedimiento de actualización](./procedimiento-cambios.md). Una desviación sin ADR es una no conformidad, no una decisión.

---

## Principios Arquitectónicos

### Nota sobre el borrador del Taller 0

La vista de motivación del Taller 0 (`00-vision-preliminar/vista-archimate-motivacion.drawio`) declaró *stakeholders*, un *driver*, dos *goals* y un *requirement*, pero **no principios arquitectónicos explícitos**. Lo que existía eran restricciones de alcance y objetivos. Este documento los formaliza como principios y los contrasta con la evidencia de los Talleres 1 a 8, que es el ejercicio que pide el Taller 9.

### Principios vigentes

| Principio | Declaración | Implicación (qué descarta) | Justificación en el proyecto | Estado frente al Taller 0 |
|---|---|---|---|---|
| **P1 · Desacople asimétrico de la contraparte** | La velocidad de Ban100 no se condiciona a la madurez digital de un tercero. Toda integración B2G debe funcionar aunque la contraparte nunca publique una API. | Descarta cualquier diseño que exija API en la pagaduría como precondición, y descarta esperar a que el Estado se modernice. | El Taller 4 midió plazos MRAE de 40 a 47 meses para los Grupos Territoriales 3, 4 y 5, donde Ban100 opera 850–880 municipios (riesgo R1, Nivel 12). SOL-1 del Taller 7 nace de aquí. | **Nuevo** — en el Taller 0 era un *driver*, no un principio |
| **P2 · El Core no se cambia, se desacopla** | El Core Bancario transaccional permanece; lo que se elimina es la dependencia síncrona hacia él. | Descarta el reemplazo del Core por un producto nuevo y descarta la migración completa a nube pública. | El Taller 0 ya excluyó el cambio de Core del alcance; el Taller 4 (R2) y el checklist 6 del Taller 6 mostraron que el problema no es el Core sino el acoplamiento. SOL-2 del Taller 7. | **Confirmado** — estaba como restricción de alcance, se eleva a principio |
| **P3 · Dato personal mínimo y supervisado** | Ningún componente, humano o agéntico, accede a más PII de la que su tarea exige, y ninguna acción de alto impacto se ejecuta sin aprobación humana. | Descarta enviar el expediente completo al proveedor de LLM y descarta la autonomía total del agente sobre desembolsos o supresiones. | Amenazas T4 y T7 del Taller 5 (fuga de PII hacia el LLM) y parcial 7 del checklist del Taller 6. Alineado con NIST SP 800-207 (mínimo privilegio, verificación continua). | **Nuevo** |
| **P4 · Cumplir antes de escalar** | Una brecha normativa abierta bloquea el despliegue de la fase que la toca; el cumplimiento no se pospone para después de la funcionalidad. | Descarta aplazar la revocatoria de la Ley 1581 «hasta que esté el Adaptador», que era la secuencia intuitiva. | El Taller 6 dejó seis criterios en ⚠️ Parcial. Es la razón por la que la Fase 1 del roadmap es regulatoria y no funcional, pese a que R1 tiene mayor nivel de riesgo. | **Nuevo** |
| **P5 · Trazabilidad como activo de cartera** | Toda operación de libranza debe quedar reconstruible de punta a punta, porque de esa trazabilidad depende la calificación de las titularizaciones. | Descarta integraciones que no dejen evidencia por solicitud y descarta ajustes manuales de cupo sin registro. | Objetivo O2 del Taller 0: la calificación AAA ESG de Sustainable Fitch para programas de hasta COP $1 billón se sostiene sobre la auditabilidad del modelo de datos (Taller 2). | **Confirmado** — estaba como objetivo O2 |

### Principios retirados

| Principio retirado | Qué evidencia lo contradijo |
|---|---|
| **«Nube como primera opción»** (`MGGTI.LI.ST.03`), que el equipo arrastraba del marco MRAE como si fuera un principio absoluto | El Taller 4 documentó que el Core Bancario y el Cliente 360 (MDM) están On-Premise en Bogotá y que el Taller 0 excluyó su reemplazo. Además, el cuello de botella de los 3 a 5 días **no es la ubicación del Core** sino la contraparte B2G: migrarlo no acerca la meta de < 15 min y sí reabre un riesgo que el Taller 0 había cerrado. Se conserva únicamente como criterio por defecto para componentes nuevos (que efectivamente se despliegan en Kubernetes en nube pública), no como regla general. |

---

## Estándares Tecnológicos

Estándares autorizados para los componentes del roadmap. Donde el estándar ya existe en el AS-IS se indica; donde es una decisión nueva de este plan, también.

| Categoría | Estándar definido | Por qué |
|---|---|---|
| **Contratos de API** | OpenAPI 3.x para la vía rápida; **X-Road / Lenguaje Común del MRAE** para entidades públicas *(nuevo)* | `MGGTI.LI.GI.05` exige publicar los servicios de intercambio, y el Lenguaje Común es lo que las pagadurías de Grupos G1–G2 ya están obligadas a adoptar: usar otro formato obligaría a Ban100 a mantener una traducción propia. |
| **Tipo de comunicación** | REST síncrono solo en el borde y hacia el cliente final; **todo cruce hacia el Core va por eventos (CDC)** *(nuevo)* | Es P2 hecho regla verificable. Cualquier componente nuevo que abra un enlace síncrono al Core reintroduce el riesgo R5. |
| **Orquestación y cómputo** | Kubernetes en nube pública para componentes nuevos *(ya en el AS-IS, Taller 4)*; el Core y el MDM permanecen On-Premise | Mantiene el estándar que el banco ya opera y evita introducir una tercera plataforma de despliegue. |
| **API Gateway** | Kong *(ya en el AS-IS)*, en configuración **Activo-Activo** obligatoria *(nuevo)* | El AS-IS lo tiene Activo-Pasivo, que es el origen del riesgo de disponibilidad en el borde. |
| **Identidad y firma electrónica** | Truora como proveedor único de biometría y firma certificada *(ya contratado)* | Fragmentar el proveedor fragmentaría la cadena probatoria del pagaré bajo la Ley 527 de 1999. |
| **Transporte** | TLS 1.3 en todos los enlaces *(ya en el AS-IS)* | Línea base del Taller 4; no se admiten excepciones por compatibilidad con pagadurías. |
| **Acceso a datos desde el agente** | El Orquestador Ban-I Bot accede a datos **solo por herramientas declaradas**, nunca directo a la base, y con filtro DLP en la salida *(nuevo)* | Es P3 hecho regla. Sin esto, el patrón de sistemas agénticos deja abierta la fuga T7. |
| **Repositorio de arquitectura** | Metamodelo MRAE v3.0, repositorio único *(nuevo, Fase 4)* | Cierra la brecha G4 (`MAE.LI.PA.08`) y es la fuente de la métrica M3. |

---

## Mecanismo de gobierno

| Rol | Responsabilidad | Persona / equipo sugerido |
|---|---|---|
| **Comité de Arquitectura Empresarial** | Aprueba el cierre de cada fase, dictamina excepciones y mantiene vigentes los principios | Presidido por el Arquitecto líder; lo integran CISO, Oficial de Protección de Datos, Líder de Plataforma, Líder del Core y Líder de Convenios B2G |
| **Arquitecto líder** | Custodia el TO-BE y el repositorio de AE; prepara el dictamen de cada excepción | Arquitectura Empresarial |
| **CISO** | **Veto** sobre cambios que afecten las mitigaciones de las amenazas T1 a T8 del Taller 5 | Oficial de Seguridad de la Información |
| **Oficial de Protección de Datos** | **Veto** sobre cambios que toquen PII, consentimiento o revocatoria (Ley 1581) | Cumplimiento |
| **Líder de Convenios B2G** | Representa la voz de la contraparte pública y valida la viabilidad operativa del Portal de Autogestión | Operaciones |
| **Revisoría Fiscal** | Verificación independiente del resultado visible de las fases con efecto contable o regulatorio | EY Audit S.A.S. |
| **Patrocinador ejecutivo** | Libera presupuesto por fase y resuelve los escalamientos que el comité no concilie | Presidencia Ejecutiva |

---

## Cadencia de seguimiento

| Instancia | Frecuencia | Qué se revisa |
|---|---|---|
| Comité de Arquitectura ordinario | **Mensual** | Avance del roadmap, excepciones radicadas y las tres métricas de gobierno |
| Puerta de fase (*gate*) | **Al cierre de cada fase** | El resultado visible de la fase, comprobado fuera de TI. Sin esa comprobación la fase no se cierra y la siguiente no arranca |
| Revisión ante Junta Directiva | **Trimestral** | Informe de una página por fase cerrada y estado de los riesgos de nivel ≥ 8 |
| Comité extraordinario | **A demanda, máx. 5 días hábiles** | Excepciones marcadas como bloqueantes y disparadores de cambio de severidad alta |

---

## Criterio de conformidad

Cada criterio es verificable con una evidencia concreta; ninguno depende de una opinión.

| # | Criterio | Cómo se verifica |
|---|---|---|
| C1 | Todo componente desplegado figura en el tablero integrado del Taller 8 **sin elementos huérfanos** | Se vuelve a correr la verificación de 0 huérfanos sobre `08-integracion-vistas/tablero-integrado-cliente.drawio` actualizado |
| C2 | **Ningún componente nuevo abre un enlace síncrono hacia el Core** | Inventario de conexiones del API Gateway y del bus: cualquier ruta directa μS → Core es una no conformidad |
| C3 | El checklist normativo del Taller 6 **no retrocede** | Ningún criterio pasa de ✅ Cumple a ⚠️ Parcial entre dos comités consecutivos |
| C4 | Cada fase cerrada tiene su **resultado visible comprobado por alguien fuera de TI**, con nombre y fecha | Acta de la puerta de fase firmada por el verificador designado en el plan de implementación |
| C5 | Toda desviación del TO-BE aprobado tiene **una ADR con alternativas y consecuencias** | Revisión del registro de decisiones; una desviación sin ADR es no conformidad |
| C6 | El agente no accede a datos fuera de sus herramientas declaradas | Revisión de los logs del Orquestador en el SOC 24/7 |

---

## Escalamiento

1. **Propone** la excepción el líder técnico de la fase, con un formato que incluye: qué del TO-BE se desvía, por qué, qué alternativas se descartaron y qué consecuencia negativa se acepta.
2. **Evalúa** el Arquitecto líder, que prepara el dictamen contra los cinco principios y los cuatro objetivos estratégicos de la Ficha (O1 a O4).
3. **Dictamina** el Comité de Arquitectura. Si la excepción toca PII o seguridad, el Oficial de Protección de Datos o el CISO tienen **veto**, y el comité no puede sobrepasarlo.
4. **Autoriza** la Presidencia Ejecutiva cuando la excepción implique presupuesto adicional o afecte un compromiso con un tercero (convenio SECOP II, calificadora o regulador).
5. **Plazo:** 10 días hábiles para excepciones ordinarias y 5 para las marcadas como bloqueantes. Vencido el plazo sin dictamen, el escalamiento sube automáticamente al patrocinador ejecutivo — esto es lo que mide la métrica M3.

---

## Métricas de gobierno

| Métrica | Qué mide (principio) | Fórmula | Fuente que ya existe | Línea base | Umbral |
|---|---|---|---|---|---|
| **M1 · Originación dentro de meta** | P1 — si el desacople de la contraparte funciona de verdad | (Solicitudes aprobadas con `tiempo_aprobacion_min` < 15 ÷ total de solicitudes aprobadas del mes) × 100 | Campo `tiempo_aprobacion_min` del modelo de información del Taller 2, ya capturado por solicitud | **≈ 0 %** — hoy el ciclo es de 3 a 5 días | Por debajo del **60 %** a los dos meses de cerrada la Fase 2, el comité revisa el Adaptador antes de autorizar la Fase 3 |
| **M2 · Conciliación de descuentos por convenio** | P5 — si la trazabilidad que sostiene la calificación AAA ESG se mantiene | (Convenios con `estado_conciliacion` = conciliado al cierre de mes ÷ convenios activos) × 100 | Campo `estado_conciliacion` del modelo de información del Taller 2, ya usado para el seguimiento de cartera | Por establecer con el primer corte mensual; la fuente ya existe | Por debajo del **95 %** dos meses seguidos escala a Junta Directiva: compromete el respaldo de las titularizaciones |
| **M3 · Tiempo de dictamen del comité** *(mide al propio comité)* | P4 — si el órgano que exige cumplir antes de escalar es él mismo el cuello de botella | Promedio de días hábiles entre la radicación de una excepción y su dictamen, en el trimestre | **No existe hoy:** nace con el acta del Comité de Arquitectura que crea este plan. No se inventa línea base | Promedio trimestral por encima de **10 días hábiles** obliga al comité a delegar el dictamen de excepciones no bloqueantes en el Arquitecto líder |

> Las tres métricas se publican en el repositorio de AE de la Fase 4 (`MAE.LI.PA.08`). Mientras ese repositorio no exista, el Arquitecto líder las presenta en el comité mensual y quedan en acta.

---

## Referencias

- **MinTIC — MRAE v3.0 (Decreto 767 de 2022):** `MAE.LI.PA.03` (Comité de Arquitectura, 1,31 % del esfuerzo), `MAE.LI.PA.08` (repositorio de AE), `MGGTI.LI.GO.10` (Políticas de TI) y `MGGTI.LI.GO.02` (no conformidades de auditorías).
- **TOGAF — Architecture Governance (Parte VII)** y *Architecture Compliance Review*: origen del criterio de conformidad verificable y del flujo de excepciones.
- **NIST SP 800-207, Zero Trust Architecture:** sustenta el principio P3 (mínimo privilegio y verificación continua).
- **Superintendencia Financiera de Colombia — Circular Externa 008 de 2023** e **ISO/IEC 27001:2022** (vía MSPI): marco de los vetos del CISO.

---

_Este documento hace parte de la entrega final del Taller 9 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
