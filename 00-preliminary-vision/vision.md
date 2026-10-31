# 📄 Documento de Visión de Arquitectura

## 🔖 Cliente
**Ban100 S.A. (Bancien S.A.)** — establecimiento bancario comercial, NIT `900.200.960-9`, Bogotá D.C.

## 👥 Integrantes del equipo
- Santiago Barrera Rueda (santiagobarrue@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

## 🗺️ Mapa conceptual de alto nivel

El mapa conceptual está modelado de forma nativa en draw.io: cuatro dominios (Negocio, Datos, Aplicaciones y Tecnología) conectados a los cuatro objetivos estratégicos de la Ficha y a los tres vectores de convergencia con el MRAE v3.0.

[Ver diagrama en draw.io](./mapa-conceptual-vision.drawio)

La capa de Motivación se detalla en una vista ArchiMate 3.2 (stakeholders, driver, goals, requirement y constraint):

[Ver vista ArchiMate de Motivación en draw.io](./vista-archimate-motivacion.drawio)

## 🚀 Beneficios esperados

| Objetivo estratégico (Ficha) | Beneficio esperado | Cómo se mide |
|---|---|---|
| **O1** Inclusión financiera en 1.000+ municipios | Sostener la cobertura del 90 % de los 1.101 municipios con una red liviana de 10 oficinas, atendiendo también a los municipios donde la pagaduría tiene baja madurez digital. | Municipios con originación digital activa (línea base: 965 en 2024; > 1.000 en 2025). |
| **O2** Calificación AAA ESG en titularizaciones | Conservar la calificación AAA con sello ESG de las emisiones de libranza (programas hasta COP $1 billón) mediante calidad y trazabilidad de la cartera. | Calificaciones vigentes de Sustainable Fitch; tasa de conciliación de descuentos por convenio (`estado_conciliacion`). |
| **O3** Originar libranza en < 15 minutos | Pasar de 3–5 días a menos de 15 minutos sin depender de la madurez digital de cada pagaduría (integración B2G de dos velocidades). | `tiempo_aprobacion_min` de cada solicitud (campo del ERD); porcentaje de solicitudes < 15 min. |
| **O4** Cumplimiento SFC, SIC y MRAE | Cerrar los seis parciales del checklist normativo y llevar el MAE de Nivel 3 a Nivel 4–5 con repositorio unificado. | Ítems "✅ Cumple" del checklist (línea base 9 de 15); nivel MAE del instrumento de 300 ítems. |

## 🧭 Alcance

| En alcance | Fuera de alcance |
|---|---|
| Proceso de originación de crédito de libranza 100 % digital y visación B2G con pagadurías (Nacional G1–G2 y Territorial G1–G5). | Cambio del Core Bancario transaccional por un producto nuevo. |
| Dominios de AE: Negocio, Datos, Aplicaciones, Tecnología y Seguridad del flujo de libranza. | Productos de ahorro, CDT, microcrédito y consumo (se usan solo como contexto del Cliente 360). |
| Asistente conversacional Ban-I Bot Libranza bajo el patrón de sistemas agénticos. | Implementación o pruebas activas sobre sistemas reales de Ban100 (solo reconocimiento pasivo autorizado). |
| Homologación con el MRAE v3.0 (MAE, MGGTI, MGPTI) y con la Circular Externa 008 de 2023. | Obligaciones de reporte FURAG (Ban100 no es sujeto obligado directo). |
| Horizonte de transición 2026 → 2027 en cuatro fases. | Rediseño de la estructura societaria, tarifas o política comercial. |

## 💡 Justificación

La visión responde al problema central de la Ficha: **el 94 % de la colocación es libranza y el 98,3 % de ese segmento depende de pagadurías públicas**, de modo que el tiempo de originación queda determinado por la contraparte más lenta. Los grupos territoriales 3, 4 y 5 del MRAE agrupan a 850–880 municipios donde Ban100 opera y cuyos plazos de adopción llegan a 40–47 meses; por eso la arquitectura objetivo separa dos velocidades: interfaces estandarizadas para los grupos avanzados y un adaptador asíncrono con portal de autogestión para los demás.

El segundo eje es la **confianza regulatoria y de mercado de capitales**. Una base de pensionados y de estratos 1–3 exige validar identidad y consentimiento sin oficina, y las titularizaciones AAA ESG exigen cartera trazable. Por eso la visión integra biometría y firma electrónica (Ley 527 de 1999), protección de datos (Ley 1581 de 2012), monitoreo SOC 24/7 y la Circular Externa 008 de 2023, y propone un asistente agéntico con guardrails y supervisión humana.

Frente a las restricciones declaradas, Ban100 no está obligado por el Decreto 767 de 2022, pero converge con el MRAE por tres vectores (Grupo de Interés y PNID, dependencia B2G y homologación frente a la SFC). Usar el MRAE como marco de referencia permite un diagnóstico verificable (MAE Nivel 3→4, MGGTI Nivel 4, MGPTI Nivel 4) y una hoja de ruta con ventanas de mantenimiento acotadas a 30 minutos y sin cambiar el Core.

---

_Este documento hace parte de la entrega del Taller 0 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
