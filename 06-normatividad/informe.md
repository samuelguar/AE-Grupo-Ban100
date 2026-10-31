# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 6 - Normatividad: Cumplimiento regulatorio de Ban100 (SFC, SIC, MRAE v3.0)_

## 👥 Integrantes del equipo
- Santiago Barrera Rueda (santiagobarrue@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A. (Bancien S.A.)

## 🧠 Descripción general del trabajo
Se evaluó el cumplimiento del flujo de originación de libranza frente a quince criterios de la Ley 1581 de 2012, la Ley 527 de 1999, la Circular Externa 008 de 2023 de la SFC, SARLAFT, ISO/IEC 27001:2022 y el MRAE v3.0 (Decreto 767 de 2022). En el checklist solo existen dos estados: **✅ Cumple** y **⚠️ Parcial**; cada parcial se traslada a la hoja *Brechas Identificadas* con su riesgo y su prioridad.

## 🔧 Proceso de desarrollo
1. Identificación de datos sensibles y de la normativa aplicable (tabla siguiente).
2. Construcción del checklist por categoría (consentimiento, protección de datos, seguridad, ciberseguridad SFC, prevención de fugas, retención, roles, SARLAFT, firma electrónica, interoperabilidad MRAE y gobierno de AE).
3. Evaluación con evidencia pública o documentada; no se hicieron pruebas activas.
4. Documentación del riesgo legal u operativo de cada brecha.
5. Priorización y recomendación correctiva concreta.

## 🧩 Análisis del modelo propuesto
### Datos sensibles y normativa aplicable
| Dato / Proceso | Sensibilidad | Normativa aplicable |
|---|---|---|
| Hash biométrico facial (`hash_biometria_truora`) | Alta (dato sensible) | Ley 1581 de 2012 (art. 5 y 6), Decreto 1377 de 2013 |
| Estrato, género y condición de pensionado | Alta | Ley 1581 de 2012; CE 008 de 2023 |
| Mesada pensional y descuentos de nómina | Alta (financiera) | Ley 1581 de 2012; Circular Básica Contable y Financiera 100 de 1995 |
| Pagaré digital y firma electrónica | Alta (probatoria) | Ley 527 de 1999 |
| Consulta de listas restrictivas | Alta | SARLAFT (Circular Básica Jurídica SFC) |
| Convenios y contratos B2G | Media (pública) | Contratos SECOP II; Decreto 767 de 2022 |
| Conversaciones con Ban-I Bot | Alta si contienen PII | Ley 1581; CE 008 de 2023 |

### Resultado del checklist (15 criterios: 9 ✅ Cumple, 6 ⚠️ Parcial)
| N° | Categoría | Criterio (resumen) | Nivel |
|---|---|---|---|
| 1 | Consentimiento | Autorización informada previa al tratamiento | ✅ Cumple |
| 2 | Consentimiento | Revocatoria y supresión ágiles (Ley 1581, art. 8) | ⚠️ Parcial |
| 3 | Protección de Datos | Canal de consultas y reclamos y Defensoría del Consumidor Financiero | ✅ Cumple |
| 4 | Seguridad (ISO/IEC 27001:2022) | Monitoreo continuo con SOC 24/7 | ✅ Cumple |
| 5 | Seguridad (ISO/IEC 27001:2022) | Autenticación biométrica y firma electrónica | ✅ Cumple |
| 6 | Ciberseguridad SFC | Continuidad sin dependencia síncrona de un único Core | ⚠️ Parcial |
| 7 | Prevención de Fugas | DLP sobre datos hacia terceros y proveedores de IA | ⚠️ Parcial |
| 8 | Retención | Custodia desmaterializada del pagaré | ✅ Cumple |
| 9 | Roles y Responsabilidades | Revisoría Fiscal (EY Audit S.A.S.) y patrocinio ejecutivo | ✅ Cumple |
| 10 | SARLAFT | Listas restrictivas y debida diligencia en originación | ✅ Cumple |
| 11 | Firma Electrónica (Ley 527) | Atribución, integridad y no repudio | ✅ Cumple |
| 12 | Interoperabilidad MRAE / Decreto 767 | Integración estandarizada con pagadurías | ⚠️ Parcial |
| 13 | Interoperabilidad MRAE / Decreto 767 | Borde Dual-Stack IPv6 (`MGGTI.LI.ST.14`) | ⚠️ Parcial |
| 14 | Gobierno de AE (MRAE v3.0) | Repositorio unificado y métricas (`MAE.LI.PA.08`) | ⚠️ Parcial |
| 15 | Sostenibilidad y Gobierno de TI | Ventanas de 30 min y reducción de papel del 29 % | ✅ Cumple |

### Brechas y recomendaciones (una por cada ⚠️ Parcial)
| Brecha | Checklist | Riesgo legal u operativo | Recomendación prioritaria | Prioridad |
|---|---|---|---|---|
| **G5** Revocatoria Ley 1581 sin automatizar | 2 | Medio — reclamos ante la SIC y sanciones por no atender derechos del titular | Módulo de revocatoria y supresión con propagación a Cliente 360 y proveedores | Alta |
| **G2** Acoplamiento síncrono al Core | 6 | Alto — incumplimiento de continuidad (CE 008/2023) | Bus de eventos con CDC < 500 ms, circuit breaker y BCP/DRP automatizado | Alta |
| **G6** Sin DLP ni guardrails agénticos | 7 | Alto — fuga de PII y de mesadas al proveedor de LLM | Filtro DLP, mínimo privilegio y Human-in-the-Loop | Alta |
| **G1** Integración B2G asimétrica | 12 | Alto — mora y cupos sin respaldo en pagadurías G3–G5 | Adaptador B2G de dos velocidades y portal de autogestión | Alta |
| **G3** Brecha IPv6 | 13 | Medio — hallazgo de conformidad con `MGGTI.LI.ST.14` y límite de interoperabilidad estatal | Dual-Stack IPv6/IPv4 en WAF, balanceador y API Gateway | Media |
| **G4** Repositorio de AE y métricas | 14 | Medio — madurez MAE sin avanzar de Nivel 3 a 4–5 | Repositorio bajo metamodelo MRAE y tablero de métricas | Media |

### Estatus frente al Decreto 767 de 2022
**Ban100 no es sujeto obligado directo.** Al contrastar el directorio SIGEP de la matriz de plazos del MinTIC con las entidades vigiladas por la SFC, el banco no figura: no integra la Administración Pública (Ley 489 de 1998, art. 39) ni ejerce funciones administrativas delegadas (art. 2.2.9.1.1.2 del Decreto 1078 de 2015, subrogado por el Decreto 767 de 2022) y no reporta el subíndice de Arquitectura del FURAG. En cambio, el *Banco Agrario de Colombia S.A.*, la *Financiera de Desarrollo Nacional* (SIGEP 1321) y *Fiducoldex S.A.* (SIGEP 6389) sí lo son en el Clúster 3 del Orden Nacional (plazos de 10–12, 17–20 y 23–27 meses).

Convergencia por tres vectores: (1) **Grupo de Interés y PNID** (art. 2.2.9.1.2.1 del Decreto 1078 de 2015; `PRI_04`); (2) **dependencia B2G por libranza**, con convenios en SECOP II (`CO1.PCCNTR.6460767`, 2024–2026, y `CO1.PCCNTR.4097470`, 2022–2024; Gobernación del Caquetá, RUP `719325524`), cuyas contrapartes sí están sujetas a plazos MRAE de 40–47 meses en los Grupos Territoriales 3 a 5; (3) **homologación técnica frente a la SFC** (TOGAF, CMMI, GAO, Gartner ITScore, PMI OPM3, ITIL e ISO/IEC 27001 vía MSPI).

### Diagnóstico de madurez (instrumento de 300 ítems)
| Pilar | Marco | Ítems | Nivel diagnosticado |
|---|---|---:|---|
| MAE | GAO (Etapas 0–6) + CMMI (1–5); 4 dimensiones, 15 atributos | 60 elementos (Id 0–59) | **Nivel 3 (Gestionado / Etapa 4 GAO) en transición a Nivel 4**; brecha a Nivel 5 en el repositorio unificado (Elem. 46) y la automatización de métricas (Elem. 58) |
| MGGTI | Gartner ITScore (1–5) + CMMI; 6 dimensiones, 25 atributos | 70 elementos / 202 criterios (Id 0–201) | **Nivel 4 (Diferenciador / Manejado)** con atributos en Nivel 5 (Crit. 3, 4, 82–84, 110, 111, 195, 196) |
| MGPTI | PMI OPM3 (1–5) + CMMI; 4 dimensiones, 16 atributos | 38 elementos (Id 1–38) | **Nivel 4 (Gestionado / Manejado)** (Elem. 1, 2, 3, 16, 19, 27, 30, 38) |
| **Total** | | **300 ítems** (60 + 202 + 38) | |

El diagnóstico por pilar corresponde al análisis del equipo con información pública; la calificación ítem por ítem requiere evidencia interna de Ban100.

## 📈 Diagrama final entregado
Excel: [`checklist-cliente.xlsx`](./checklist-cliente.xlsx) (hojas `Checklist General` y `Brechas Identificadas`).

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Superintendencia Financiera de Colombia | Regulador | CE 008/2023, CBCF 100/1995, SARLAFT | Cumplimiento |
| Superintendencia de Industria y Comercio | Regulador | Ley 1581 de 2012 | Oficial de Protección de Datos |
| MinTIC | Entidad rectora | MRAE v3.0 y Decreto 767 de 2022 | Arquitectura Empresarial |
| Defensoría del Consumidor Financiero | Canal | Consultas y reclamos | Servicio al cliente |

## 🔍 Investigación complementaria
### Tema investigado:
Normativa sectorial de la SFC y del MinTIC aplicable a una entidad financiera privada con dependencia de contratación pública.

### Resumen:
La Circular Externa 008 de 2023 refuerza los requerimientos de seguridad de la información y ciberseguridad (gobierno, monitoreo, gestión de incidentes, nube y continuidad); la Ley 1581 de 2012 y el Decreto 1377 de 2013 rigen el tratamiento de datos personales y los derechos ARCO; la Ley 527 de 1999 da validez a mensajes de datos y firmas. El MRAE v3.0 no obliga a Ban100, pero sus lineamientos sirven de marco de auditoría homologable: `MAE.LI.PA.01` (evaluación de madurez), `PA.03` (Comité de AE, 1,31 %), `PA.05` (AS-IS/TO-BE/Gap: 15,96 % del esfuerzo total = 368 h a 910 h), `PA.07` (hoja de ruta en el PETI) y `PA.08` (repositorio de AE); `MGGTI.LI.GO.10` (Políticas de TI, 2,54 %), `GO.02` (no conformidades de auditorías) y `GS.01–GS.04` (MSPI, riesgos, controles y monitoreo). La distribución del esfuerzo: 106 lineamientos = 29 MAE (34,03 %), 63 MGGTI (58,10 %) y 14 MGPTI (7,87 %).

### Vista ArchiMate equivalente
Cada brecha es un *Constraint* o *Requirement* de Motivación que restringe a un proceso o aplicación y se convierte en un *Gap* en el Taller 7 (G5 y G6 → Gap 4; G1 → Gap 1; G2 → Gap 2; G3 y G4 → Gap 3).

## 📚 Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 6 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
