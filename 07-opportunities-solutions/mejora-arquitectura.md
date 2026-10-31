# 📄 Mejora de Arquitectura (TO-BE) — Identificación y Priorización de Mejoras

## 🔖 Cliente
**Ban100 S.A. (Bancien S.A.)** — NIT `900.200.960-9`

## 👥 Integrantes del equipo
- Santiago Barrera Rueda (santiagobarrue@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial

---

## 1. Diagnóstico inicial

Respuestas basadas exclusivamente en lo diagnosticado en los Talleres 3 a 6.

| Pregunta orientadora | Respuesta para Ban100 | Taller de origen |
|---|---|---|
| ¿Qué procesos o tecnologías generan mayor fricción? | La visación de cupo con 850–880 pagadurías municipales de Grupos MRAE 3 a 5 (sin API directa) y el enlace síncrono μS Originación ↔ Core On-Premise frenan la meta de originar libranza en < 15 min (hoy 3–5 días). | Talleres 3 y 4 |
| ¿Qué problemas recurrentes señaló el cliente? | Retraso en validación de cupos y visación con pagadurías de baja madurez digital; el 94 % de la colocación es libranza y el 98,3 % de ese segmento es sector público/pensionados. | Taller 0 y 1 |
| ¿Qué vulnerabilidades o riesgos quedaron evidenciados? | T1 suplantación biométrica, T4 exposición de PII, T7 fuga de PII hacia el LLM, T8 archivo de visación alterado; seis parciales normativos (Ley 1581, CE 008/2023, DLP, IPv6, interoperabilidad y repositorio de AE). | Talleres 5 y 6 |

**Resumen del problema actual (foto del AS-IS):** Ban100 originó digitalmente el 95 % de sus créditos en 2024 (100 % en libranza), pero el ciclo de libranza sigue limitado por la contraparte pública más lenta y por un Core On-Premise acoplado de forma síncrona. La arquitectura carece de controles específicos para el asistente conversacional y de un repositorio unificado de AE (MAE Nivel 3 → 4).

**Brechas consolidadas (Talleres 3, 4, 5 y 6):** G1 asimetría B2G (T4, T5) · G2 acoplamiento síncrono (T4, T6) · G3 brecha IPv6 (T4, T6) · G4 repositorio de AE y métricas (T6) · G5 revocatoria Ley 1581 (T6) · G6 DLP y guardrails agénticos (T5, T6).

---

## 2. Propuesta de mejoras

### 2.1 Lluvia de ideas (sin censura inicial)

| # | Idea de mejora | Tipo |
|---|---|---|
| 1 | Adaptador B2G de Dos Velocidades (X-Road/REST para G1-G2; RPA/ETL para G3-G5) | Tecnología |
| 2 | Portal Web de Autogestión para pagadurías de Grupos 3 a 5 | Proceso |
| 3 | Bus de Eventos y CDC (< 500 ms) con Circuit Breaker hacia el Core | Tecnología |
| 4 | Borde Dual-Stack IPv6/IPv4 y API Gateway Activo-Activo | Tecnología |
| 5 | Revocatoria y supresión Ley 1581 en autogestión | Seguridad / Proceso |
| 6 | Filtro DLP y guardrails para el asistente conversacional | Seguridad |
| 7 | Orquestador agéntico Ban-I Bot con 4 herramientas y Human-in-the-Loop | IA agéntica |
| 8 | Repositorio de AE bajo metamodelo MRAE y métricas automatizadas | Proceso |
| 9 | Comunicación proactiva a pagadurías sobre plazos MRAE y guías de integración | Comunicación |
| 10 | Detección de vida certificada y OTP en la validación biométrica | Seguridad |

### 2.2 Priorización (3 soluciones estructurales)

| Solución priorizada | Esfuerzo | Impacto | Quick win / Largo plazo | Justificación |
|---|---|---|---|---|
| **SOL-1** Adaptador B2G de Dos Velocidades (ideas 1, 2, 9) | Alto | Alto | Largo plazo (entrega incremental desde la Fase 2) | Cierra G1 y mitiga T8: atiende a la vez a las pagadurías G1-G2 con interfaz estandarizada y a las 850–880 de G3-G5 sin exigirles API. |
| **SOL-2** Desacoplamiento asimétrico del Core con Bus CDC, Circuit Breaker y BCP/DRP (ideas 3, 4) | Alto | Alto | Largo plazo | Cierra G2 y G3: elimina la dependencia síncrona y habilita continuidad y Dual-Stack IPv6. |
| **SOL-3** Capa agéntica segura y gobierno de datos personales (ideas 5, 6, 7, 10) | Bajo-Medio | Alto | **Quick win** | Cierra G5 y G6 con controles de bajo esfuerzo y alto efecto regulatorio (Ley 1581, CE 008/2023). |

La idea 8 (repositorio de AE) se ejecuta como habilitador de gobierno dentro de la Fase 4 y cierra G4.

---

## 3. Visualización TO-BE

### 3.1 Proceso mejorado
El proceso del Taller 1 se mantiene, con un cambio de fondo en la compuerta *¿Pagaduría tiene interoperabilidad API/X-Road (G1-G2) o requiere vía asíncrona (G3-G5)?*: la vía asíncrona deja de ser manual y pasa a un motor RPA/ETL con cola de mensajería y un portal de autogestión; además, el asistente solo responde con datos devueltos por sus herramientas y escala a un analista las acciones de alto impacto.

### 3.2 Cambios en aplicaciones, infraestructura y flujos de información
- **Aplicaciones** (extiende el C2 del Taller 3, conservando sus nombres): [Ver C2 TO-BE en draw.io](./to-be-aplicaciones-final.drawio). Adiciones 🆕: Adaptador B2G de Dos Velocidades, Orquestador Agéntico Ban-I Bot con Guardrails DLP y Aprobación Humana (Human-in-the-Loop), Módulo de Revocatoria y Supresión Ley 1581, API Gateway Redundante Activo-Activo y Bus de Eventos CDC con Circuit Breaker.
- **Infraestructura** (extiende el mapa del Taller 4): [Ver mapa TO-BE en draw.io](./to-be-tecnologia-final.drawio). Adiciones 🆕: Borde Dual-Stack IPv6/IPv4 (`MGGTI.LI.ST.14`), API Gateway Activo-Activo, Bus CDC (< 500 ms) y BCP/DRP automatizado.
- **Migración**: [Ver vista ArchiMate de Implementación y Migración en draw.io](./vista-archimate-migracion.drawio): Plateau AS-IS 2026 → 4 Gaps → 4 Work Packages → Plateau TO-BE 2027.

| Elemento TO-BE | Brecha que cierra | Origen AS-IS |
|---|---|---|
| Adaptador B2G de Dos Velocidades | G1 | Riesgo R1 (Taller 4), T8 (Taller 5) |
| Bus CDC + Circuit Breaker + BCP/DRP | G2 | Riesgo R2 (Taller 4), checklist 6 |
| Borde Dual-Stack IPv6 y Gateway Activo-Activo | G3 | Riesgo R3 (Taller 4), checklist 13 |
| Repositorio de AE y métricas | G4 | Checklist 14 (Taller 6) |
| Módulo de Revocatoria y Supresión Ley 1581 | G5 | Checklist 2 (Taller 6) |
| Guardrails DLP + Orquestador con HITL | G6 | T7 (Taller 5), checklist 7 |

### 3.3 Controles de seguridad integrados
Del Taller 5 se integran: **T1** liveness certificado y OTP (idea 10); **T4** DLP y control de acceso por atributos sobre Cliente 360; **T5** Gateway Activo-Activo y límites de tasa; **T6** cuentas de servicio de mínimo privilegio con doble autorización de desembolsos; **T7** filtro DLP, separación de instrucciones y entrada, y Human-in-the-Loop; **T8** firma digital de los archivos de pagaduría y portal de autogestión con autenticación fuerte. El agente se modela con el patrón de sistemas agénticos: [Ver vista del sistema agéntico](../../archimate-transversal/vista-sistema-agentico-ban-i-bot.drawio).

---

## 4. Análisis de beneficios y riesgos

| Mejora / Solución | Beneficio de negocio | Beneficio tecnológico/seguridad | Riesgo, limitación o dependencia de implementación |
|---|---|---|---|
| SOL-1 Adaptador B2G de Dos Velocidades | Acerca la originación a la meta < 15 min sin esperar a que cada municipio se modernice. | Interoperabilidad estandarizada (`MGGTI.LI.GI.05`) y trazabilidad de cada visación. | Depende del ritmo de adopción de las pagadurías (plazos MRAE de 40 a 47 meses) y de convenios y soporte a municipios. |
| SOL-2 Desacoplamiento del Core | Originación disponible aun con ventanas de mantenimiento del Core. | Menor acoplamiento, recuperación automatizada y Dual-Stack IPv6. | Consistencia eventual y complejidad operativa del bus; requiere pruebas periódicas de DRP. |
| SOL-3 Capa agéntica segura y Ley 1581 | Cumplimiento regulatorio y confianza de pensionados (estratos 1–3). | Prevención de fuga de PII y supervisión humana de acciones críticas. | Dependencia de un proveedor de LLM, costo por sesión y necesidad de monitoreo continuo por el SOC 24/7. |

**Work Packages (alimentan el plan de implementación):**

| WP | Fase | Ventana | Entregables | Brechas |
|---|---|---|---|---|
| WP1 | Fase 1: Quick Win | 0–1 mes | Revocatoria Ley 1581; política DLP del Bot; liveness y OTP | G5, G6 |
| WP2 | Fase 2: Corto Plazo | 1–3 meses | Adaptador B2G (vía rápida y Portal de Autogestión); agente con HITL | G1, G6 |
| WP3 | Fase 3: Mediano Plazo | 3–6 meses | Bus CDC, Circuit Breaker y BCP/DRP automatizado | G2 |
| WP4 | Fase 4: Largo Plazo | 6–12 meses | Dual-Stack IPv6, Gateway Activo-Activo y repositorio de AE | G3, G4 |

---

## 📎 Anexos
- Diagrama TO-BE de Aplicaciones: [`to-be-aplicaciones-final.drawio`](./to-be-aplicaciones-final.drawio)
- Diagrama TO-BE de Tecnología: [`to-be-tecnologia-final.drawio`](./to-be-tecnologia-final.drawio)
- Vista de Implementación y Migración: [`vista-archimate-migracion.drawio`](./vista-archimate-migracion.drawio)
- Matriz de brechas (Gap Analysis): [`matriz-brechas.xlsx`](./matriz-brechas.xlsx)

---

**Homologación MRAE v3.0:** `MAE.LI.PA.05` (definición de AS-IS/TO-BE/Gap), `PA.07` (hoja de ruta en el PETI), `MGGTI.LI.ES.02` (PETI a 4 años con actualización anual), `ST.14` (IPv6), `GI.05` (publicación de servicios de intercambio) y `MGPTI.LI.CES.04` (PMO de TI, 1,14 %).

_Este documento hace parte de la entrega del Taller 7 (Opportunities & Solutions) del curso AREM - Universidad de La Sabana._
