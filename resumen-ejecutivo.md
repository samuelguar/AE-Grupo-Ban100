# Resumen Ejecutivo — Arquitectura Empresarial Ban100

**Para:** Presidencia Ejecutiva y Junta Directiva de Ban100 S.A. (Bancien S.A.)
**De:** Ban100 — Grupo de Arquitectura Empresarial (Santiago Barrera Rueda, Krish Purmessur Moros, Samuel Guerrero Arcos)
**Fecha:** 14 de noviembre de 2026

## 1. El problema

El 94 % de la colocación de Ban100 es libranza y el 98,3 % de ese segmento está en pensionados y empleados de gobierno, de modo que el tiempo para aprobar un crédito depende de la pagaduría más lenta. En 850 a 880 municipios (Grupos Territoriales 3, 4 y 5 del MRAE) las pagadurías tienen una madurez digital baja y plazos de adopción de 40 a 47 meses. A la vez, el enlace entre el servicio de originación y el sistema central On-Premise es síncrono, y existen seis brechas normativas parciales (datos personales, ciberseguridad, DLP, IPv6, interoperabilidad y gobierno de la arquitectura).

## 2. La propuesta

| Solución | Qué cambia para el negocio | Brecha que cierra |
|---|---|---|
| **Integración B2G de dos velocidades** | Conexión estándar (X-Road/REST) con pagadurías avanzadas y canal asíncrono con portal de autogestión para las demás | G1 |
| **Desacoplamiento del sistema central** | La originación sigue disponible durante mantenimientos del Core; sincronización en menos de 500 ms y recuperación automatizada | G2, G3 |
| **Asistente Ban-I Bot seguro y gobierno de datos** | Atención digital con filtro de datos personales, aprobación humana de acciones críticas y revocatoria automática (Ley 1581) | G5, G6 |
| **Repositorio de arquitectura con métricas** | Madurez MAE de Nivel 3 hacia Nivel 4–5 | G4 |

## 3. Beneficios esperados

| Beneficio | Indicador | Línea base → meta |
|---|---|---|
| Originación inmediata | Tiempo de aprobación de libranza (`tiempo_aprobacion_min`) | 3–5 días → **< 15 minutos** |
| Cobertura | Municipios con originación digital | 965 (2024) → 1.000+ (2025, 90 % de 1.101) sostenidos |
| Capital de confianza | Calificación de titularizaciones | Mantener **AAA con certificación ESG** (programas hasta COP $1 billón) |
| Cumplimiento | Criterios del checklist normativo | 9 de 15 "Cumple" → 15 de 15 |
| Madurez de arquitectura | Instrumento MRAE de 300 ítems | MAE Nivel 3 → 4; MGGTI Nivel 4; MGPTI Nivel 4 |

## 4. Cómo y cuándo (cuatro fases)

| Fase | Ventana | Entregables | Brechas |
|---|---|---|---|
| 1 · Quick Win | 0–1 mes | Revocatoria Ley 1581, política DLP del Bot, liveness y OTP | G5, G6 |
| 2 · Corto Plazo | 1–3 meses | Adaptador B2G (vía rápida y Portal de Autogestión) y agente con aprobación humana | G1, G6 |
| 3 · Mediano Plazo | 3–6 meses | Bus de eventos CDC, Circuit Breaker y BCP/DRP automatizado | G2 |
| 4 · Largo Plazo | 6–12 meses | Borde Dual-Stack IPv6, API Gateway Activo-Activo y repositorio de AE | G3, G4 |

## 5. Relación con el MRAE v3.0 (MinTIC)

Ban100 **no es sujeto obligado directo** del Decreto 767 de 2022 ni reporta en el FURAG, pero converge con el MRAE por tres vectores: pertenece al grupo de interés del sector privado de la Política de Gobierno Digital, depende de convenios en SECOP II con entidades territoriales (por ejemplo, los contratos `CO1.PCCNTR.6460767` y `CO1.PCCNTR.4097470` con la Gobernación del Caquetá) cuyas contrapartes sí tienen plazos MRAE, y puede usar sus 106 lineamientos (29 MAE, 63 MGGTI y 14 MGPTI) como marco homologable ante la SFC.

## 6. Riesgos principales de la implementación

- La adopción de las pagadurías no depende de Ban100: la vía asíncrona es la que garantiza avance.
- El bus de eventos introduce consistencia eventual y exige pruebas periódicas de recuperación.
- El asistente depende de un proveedor externo de modelos de lenguaje; requiere monitoreo del SOC 24/7 y control de costos.

## 7. Dónde profundizar

- [README del repositorio](README.md)
- [Mejora de arquitectura y matriz de brechas](07-oportunidades-soluciones/mejora-arquitectura.md)
- [Tablero integrado y verificación de 0 huérfanos](08-integracion-vistas/informe.md)
- [Checklist normativo](06-normatividad/informe.md)
- [Matriz de riesgos arquitectónicos (7 dominios)](09-presentacion-final/matriz-riesgos.xlsx)
- [Plan de implementación y gestión del cambio](09-presentacion-final/plan-implementacion.md)
- [Plan de gobernanza, principios y métricas](09-presentacion-final/plan-gobernanza.md)
- [Procedimiento de actualización y registro de decisiones (ADR)](09-presentacion-final/procedimiento-cambios.md)
- [Vistas ArchiMate finales de Motivación y Migración](09-presentacion-final/vistas-finales/)
