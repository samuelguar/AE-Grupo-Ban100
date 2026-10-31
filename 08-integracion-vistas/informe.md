# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 8 - Integración de Vistas: Tablero integrado de 5 capas para Ban100_

## 👥 Integrantes del equipo
- Santiago Barrera Rueda (santiagobarrue@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A. (Bancien S.A.)

## 🧠 Descripción general del trabajo
Se integraron las vistas de los Talleres 1 a 7 en un único tablero de **cinco capas** (Negocio, Aplicaciones, Información, Infraestructura, Seguridad y Cumplimiento) sobre el hilo conductor **Originación Digital de Libranza y Recaudo B2G**. El tablero reúne el AS-IS y las adiciones TO-BE del Taller 7 (marcadas con 🆕) y termina con una verificación explícita de que ningún elemento queda huérfano.

## 🔧 Proceso de desarrollo
1. **Capas.** Cinco bandas apiladas, una debajo de otra, con el color estándar de ArchiMate 3.2.
2. **Elementos.** Se ubicó cada elemento de los talleres anteriores en su capa con **el mismo nombre** que en su entregable de origen (por ejemplo *μS Originación y Scoring*, *Cliente 360 (MDM)*, *Core Bancario*, *Nube Pública (Kubernetes)*).
3. **Relaciones verticales** trazadas proceso por proceso, de punta a punta: proceso → aplicación → dato → infraestructura → control de seguridad.
4. **Narrativa** del porqué de cada conexión y del taller que la originó.
5. **Verificación de huérfanos** con la tabla de la sección siguiente.

## 🧩 Análisis del modelo propuesto
### Hilo conductor
*Pensionado / Empleado Público* → **Canales Digitales y Ban-I Bot** → **API Gateway (Activo-Activo)** → **μS Originación y Scoring** → **Truora** (identidad y firma) y **Adaptador B2G de Dos Velocidades** → **Core Bancario** → *Descuento de Nómina* en la pagaduría.

### Narrativa de coherencia (el porqué de cada conexión)
- **Negocio ← Aplicaciones (*sirve a*).** Cada proceso depende de componentes concretos porque en el Taller 1 el carril de *Canales Digitales* y el de *Motor de Originación* son quienes ejecutan las tareas del pensionado y de la pagaduría. *Truora* sirve a la Originación porque sin biometría y firma la compuerta de identidad del BPMN no puede resolverse; el *Adaptador B2G* y el *Portal Web de Autogestión* sirven a *Pagaduría Pública* y al *Recaudo* porque el Taller 4 mostró que 850–880 municipios (Grupos MRAE 3–5) no tienen API.
- **Aplicaciones → Información (*accede a*).** *μS Originación* accede a *Cliente 360 (MDM)* porque el scoring consolida el perfil del cliente (Taller 2); el *Adaptador* y el *Portal* acceden a *Convenio SECOP II* porque el cupo se valida contra el convenio; el *Core* accede a *Descuento de Nómina* porque concilia el recaudo por periodo; *Truora* se vincula con el *Pagaré Digital* porque su firma electrónica es la evidencia de no repudio (Ley 527 de 1999).
- **Infraestructura → Aplicaciones (*aloja*).** El *Borde Dual-Stack IPv6/IPv4 y WAF* aloja los canales y el gateway; la *Nube Pública (Kubernetes)* aloja μS Originación y el Portal; el *Centro de Datos On-Premise* aloja el Core. El *Bus de Eventos y CDC* sirve al Adaptador porque desacopla la originación del Core (riesgo R2 del Taller 4).
- **Seguridad → Infraestructura (*satisface*).** Cada requisito se realiza en un elemento tecnológico: CE 008/2023 y MSPI en el borde (Taller 6, ítem 4–5); Interoperabilidad MRAE e IPv6 en el borde (`MGGTI.LI.ST.14`); Guardrails DLP y Human-in-the-Loop y la Ley 1581/527 en la nube (T4, T7 y T3 del Taller 5); continuidad y BCP/DRP en el bus; control de acceso en el Core (T6). El *SOC 24/7* monitorea la nube pública.
- **Decisión transversal.** La seguridad no es una capa aparte sin conexiones: cada requisito proviene de una amenaza T1–T8 o de un parcial del checklist y cada uno está anclado a un elemento de infraestructura concreto.

### Tabla de Verificación de 0 Elementos Huérfanos
Cada elemento debe tener al menos una conexión hacia arriba y una hacia abajo, excepto la capa más alta y la más baja (—).

| Elemento | Capa | ¿Conectado hacia arriba? | ¿Conectado hacia abajo? |
|---|---|---|---|
| Pensionado / Empleado Público | Negocio | — (capa más alta) | ✅ Canales Digitales y Ban-I Bot |
| Originación Digital de Crédito de Libranza (< 15 min) | Negocio | — (capa más alta) | ✅ API Gateway (Activo-Activo), μS Originación y Scoring, Truora Biometría y Firma (externo) |
| Pagaduría Pública (G1–G5) | Negocio | — (capa más alta) | ✅ Portal Web de Autogestión de Pagadurías |
| Recaudo B2G y Descuento de Nómina/Mesada | Negocio | — (capa más alta) | ✅ Adaptador B2G de Dos Velocidades, Core Bancario |
| Canales Digitales y Ban-I Bot | Aplicaciones | ✅ Pensionado / Empleado Público | ✅ Borde Dual-Stack IPv6/IPv4 y WAF |
| API Gateway (Activo-Activo) 🆕 | Aplicaciones | ✅ Originación Digital de Crédito de Libranza (< 15 min) | ✅ Solicitud de Libranza, Borde Dual-Stack IPv6/IPv4 y WAF |
| μS Originación y Scoring | Aplicaciones | ✅ Originación Digital de Crédito de Libranza (< 15 min) | ✅ Cliente 360 (MDM), Nube Pública (Kubernetes) |
| Truora Biometría y Firma (externo) | Aplicaciones | ✅ Originación Digital de Crédito de Libranza (< 15 min) | ✅ Pagaré Digital |
| Portal Web de Autogestión de Pagadurías 🆕 | Aplicaciones | ✅ Pagaduría Pública (G1–G5) | ✅ Convenio SECOP II, Nube Pública (Kubernetes) |
| Adaptador B2G de Dos Velocidades 🆕 | Aplicaciones | ✅ Recaudo B2G y Descuento de Nómina/Mesada | ✅ Convenio SECOP II, Bus de Eventos y CDC (< 500 ms) |
| Core Bancario | Aplicaciones | ✅ Recaudo B2G y Descuento de Nómina/Mesada | ✅ Descuento de Nómina, Centro de Datos On-Premise |
| Solicitud de Libranza | Información | ✅ API Gateway (Activo-Activo) | ✅ Nube Pública (Kubernetes) |
| Cliente 360 (MDM) | Información | ✅ μS Originación y Scoring | ✅ Centro de Datos On-Premise |
| Pagaré Digital | Información | ✅ Truora Biometría y Firma (externo) | ✅ Nube Pública (Kubernetes) |
| Convenio SECOP II | Información | ✅ Adaptador B2G de Dos Velocidades, Portal Web de Autogestión de Pagadurías | ✅ Nube Pública (Kubernetes) |
| Descuento de Nómina | Información | ✅ Core Bancario | ✅ Centro de Datos On-Premise |
| Borde Dual-Stack IPv6/IPv4 y WAF 🆕 | Infraestructura | ✅ Canales Digitales y Ban-I Bot, API Gateway (Activo-Activo) | ✅ Cumplir CE 008/2023 SFC y MSPI, Interoperabilidad MRAE v3.0 e IPv6 (MGGTI.LI.ST.14) |
| Nube Pública (Kubernetes) | Infraestructura | ✅ μS Originación y Scoring, Portal Web de Autogestión de Pagadurías, Solicitud de Libranza, Pagaré Digital, Convenio SECOP II | ✅ Guardrails DLP y Human-in-the-Loop, Ley 1581 (revocatoria) y Ley 527 (no repudio), SOC 24/7 (Monitoreo y Ciberseguridad) |
| Bus de Eventos y CDC (< 500 ms) 🆕 | Infraestructura | ✅ Adaptador B2G de Dos Velocidades | ✅ Continuidad y recuperación del Core (BCP/DRP) |
| Centro de Datos On-Premise | Infraestructura | ✅ Core Bancario, Cliente 360 (MDM), Descuento de Nómina | ✅ Control de acceso y segregación de funciones (ISO/IEC 27001:2022) |
| Cumplir CE 008/2023 SFC y MSPI | Seguridad y Cumplimiento | ✅ Borde Dual-Stack IPv6/IPv4 y WAF | — (capa más baja) |
| Ley 1581 (revocatoria) y Ley 527 (no repudio) | Seguridad y Cumplimiento | ✅ Nube Pública (Kubernetes) | — (capa más baja) |
| SOC 24/7 (Monitoreo y Ciberseguridad) | Seguridad y Cumplimiento | ✅ Nube Pública (Kubernetes) | — (capa más baja) |
| Guardrails DLP y Human-in-the-Loop 🆕 | Seguridad y Cumplimiento | ✅ Nube Pública (Kubernetes) | — (capa más baja) |
| Interoperabilidad MRAE v3.0 e IPv6 (MGGTI.LI.ST.14) | Seguridad y Cumplimiento | ✅ Borde Dual-Stack IPv6/IPv4 y WAF | — (capa más baja) |
| Continuidad y recuperación del Core (BCP/DRP) | Seguridad y Cumplimiento | ✅ Bus de Eventos y CDC (< 500 ms) | — (capa más baja) |
| Control de acceso y segregación de funciones (ISO/IEC 27001:2022) | Seguridad y Cumplimiento | ✅ Centro de Datos On-Premise | — (capa más baja) |

**Resultado:** 27 elementos verificados · **0 huérfanos**.

## 📈 Diagrama final entregado
[Ver tablero integrado en draw.io](./tablero-integrado-cliente.drawio)

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Pensionado / Empleado Público | Business Actor | Actor final del proceso | Cliente |
| Originación Digital de Crédito de Libranza (< 15 min) | Business Process | Proceso modelado en el Taller 1 | Gerencia de Crédito |
| Recaudo B2G y Descuento de Nómina/Mesada | Business Process | Visación y descuento con la pagaduría | Convenios B2G |
| Capas de Aplicación, Información e Infraestructura | Capas | Componentes, datos y nodos de los Talleres 2, 3, 4 y 7 | TI |
| Capa de Seguridad y Cumplimiento | Capa | Requisitos de los Talleres 5 y 6 | Seguridad y Cumplimiento |

## 🔍 Investigación complementaria
### Tema investigado:
Documentación de vistas arquitectónicas con ArchiMate 3.2 y TOGAF 10 (ADM, fases B–D y vistas por stakeholder).

### Resumen:
TOGAF organiza la arquitectura en dominios (negocio, datos, aplicaciones, tecnología) y propone vistas por interesado; ArchiMate aporta el lenguaje común para conectarlos con relaciones semánticas (sirve a, accede a, asignado a, realiza). El tablero aplica ambos: las relaciones usadas son las del metamodelo, y la capa de seguridad se expresa con *Requirements* realizados por elementos tecnológicos. El MRAE v3.0 respalda el ejercicio en `MAE.LI.PA.05` (definición de la AE As-Is/To-Be/Gap), `PA.08` (repositorio de AE) y `MAE.LI.UA.01–02` (uso y apropiación de AE).

**Reflexión crítica sobre la coherencia.** El tablero revela dos tensiones que ninguna vista aislada mostraba: (1) la mayoría de los requisitos de seguridad terminan anclados al borde y a la nube, mientras que el Core On-Premise solo recibe un control (acceso y segregación de funciones), lo que sugiere reforzar su monitoreo en la Fase 3; y (2) el dato *Convenio SECOP II* depende de un adaptador que solo existe en el TO-BE, es decir, hoy esa trazabilidad se hace de forma manual. Ambas se reflejan en los Work Packages WP2 y WP3.

## 📚 Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 8 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
