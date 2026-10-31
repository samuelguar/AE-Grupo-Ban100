# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 5 - Seguridad: Modelado de amenazas STRIDE del flujo de Originación Digital y Desembolso de Libranza_

## 👥 Integrantes del equipo
- Santiago Barrera Rueda (santiagobarrue@unisabana.edu.co)
- Krish Purmessur Moros (krishpumo@unisabana.edu.co)
- Samuel Guerrero Arcos (samuelguar@unisabana.edu.co)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A. (Bancien S.A.)

## 🧠 Descripción general del trabajo
Se modelaron las amenazas del flujo **Originación Digital y Desembolso de Libranza** con STRIDE: un diagrama de flujo de datos (DFD) con tres fronteras de confianza más un límite externo, ocho amenazas (T1–T8) que cubren las seis categorías, su priorización por impacto y probabilidad y el vínculo con el MRAE v3.0 y la Circular Externa 008 de 2023 de la SFC. Se añadió una sección sobre riesgos de sistemas agénticos (MITRE ATLAS) porque el TO-BE incorpora un asistente con modelo de lenguaje.

## 🔧 Proceso de desarrollo
1. **DFD** del flujo con elementos numerados en correspondencia 1:1 con `tabla-stride-cliente.xlsx`.
2. **Tabla de elementos** (entidades, procesos, almacenes y flujos).
3. **STRIDE** aplicado a elementos concretos, no de forma genérica.
4. **Impacto, probabilidad, controles existentes y mitigación** de cada amenaza.
5. **Priorización** de mayor a menor riesgo en la hoja `Priorizacion_STRIDE`.

**Regla de oro cumplida:** la columna *Controles de Seguridad Existentes* se basa en **reconocimiento pasivo autorizado** (información pública del banco, documentación y arquitectura AS-IS). **No se ejecutó ninguna prueba activa** (inyección, manipulación de solicitudes o acceso no autorizado) contra sistemas reales de Ban100.

## 🧩 Análisis del modelo propuesto
### Elementos del DFD
| ID | Elemento | Tipo |
|---|---|---|
| E1 | Pensionado / Empleado Público | Entidad externa |
| E2 | Truora (biometría y firma) | Entidad externa |
| E3 | Pagaduría Pública (G1–G5) | Entidad externa |
| P1 | Canales Digitales y Ban-I Bot | Proceso |
| P2 | API Gateway | Proceso |
| P3 | μS Originación y Scoring | Proceso |
| P4 | Core Bancario | Proceso |
| D1 | Cliente 360 (MDM) | Almacén de datos |
| D2 | Expediente de solicitud y Pagaré Digital | Almacén de datos |
| D3 | Cartera de libranzas (Core) | Almacén de datos |
| F1 – F10 | Flujos entre los elementos (véase `Elementos_DFD` en el Excel) | Flujo |

**Fronteras de confianza:** Límite 1 *Internet Público / Dispositivo del Pensionado* (E1); Límite 2 *DMZ y Nube Pública Kubernetes Ban100* (P1, P2, P3, D2); Límite 3 *Red Interna On-Premise Core Bancario* (P4, D1, D3); Límite Externo *APIs de Truora y Pagadurías Públicas* (E2, E3).

### Matriz STRIDE (resumen)
| ID | Tipo STRIDE | Componente / Activo | Nivel de riesgo |
|---|---|---|---|
| T1 | Spoofing | P1 / F1 — suplantación biométrica del pensionado | Crítico |
| T2 | Tampering | P3 / F3 — alteración de monto, plazo o cuota | Alto |
| T3 | Repudiation | D2 / F4 — repudio de la firma del pagaré | Alto |
| T4 | Information Disclosure | D1 / F5 — exposición de PII en Cliente 360 | Crítico |
| T5 | Denial of Service | P2 / F2 — saturación del API Gateway y del bot | Alto |
| T6 | Elevation of Privilege | P4 / F8 — escalamiento de privilegios en el Core | Crítico |
| T7 | Information Disclosure | P1 / F1 — prompt injection y fuga de PII al LLM | Alto |
| T8 | Tampering | E3 / F6 — archivo de visación falsificado (pagadurías G3–G5) | Alto |

El detalle completo (descripción, escenario de ataque, impacto, probabilidad, controles existentes, mitigación, responsable y estado) está en las **12 columnas obligatorias** de la hoja `Plantilla_STRIDE`.

### Priorización
| Prioridad | ID | Tipo STRIDE | Componente / Activo | Nivel de Riesgo |
|---|---|---|---|---|
| 1 | T1 | Spoofing | Canales Digitales y Ban-I Bot (P1) | Crítico |
| 2 | T4 | Information Disclosure | Cliente 360 (D1) | Crítico |
| 3 | T6 | Elevation of Privilege | Core Bancario (P4) | Crítico |
| 4 | T7 | Information Disclosure | Ban-I Bot (P1) | Alto |
| 5 | T8 | Tampering | Pagaduría Pública (E3) | Alto |
| 6 | T2 | Tampering | μS Originación y Scoring (P3) | Alto |
| 7 | T3 | Repudiation | Pagaré Digital (D2) | Alto |
| 8 | T5 | Denial of Service | API Gateway (P2) | Alto |

### Reto práctico (OWASP Juice Shop) vinculado a la tabla
| Reto | Categoría STRIDE | ¿Qué control faltaba? | Mitigación real que lo hubiera evitado |
|---|---|---|---|
| Cesta de otro usuario por IDOR (`/rest/basket/N`) | Information Disclosure (T4) | Verificar que el identificador del recurso pertenece a la sesión autenticada | Autorización por objeto y control de acceso por atributos en Cliente 360, con auditoría de consultas masivas |

## 📈 Diagrama final entregado
[Ver DFD en draw.io](./dfd-originacion-libranza.drawio) · Tabla: [`tabla-stride-cliente.xlsx`](./tabla-stride-cliente.xlsx)

## 📋 Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Oficial de Seguridad de la Información (CISO) | Rol | Responde por T1 y T7 | Seguridad |
| Oficial de Protección de Datos | Rol | Responde por T4 | Cumplimiento |
| Líder de Infraestructura y SOC | Rol | Responde por T5 | Infraestructura |
| Líder del Core Bancario | Rol | Responde por T6 | TI |
| Líder de Convenios B2G | Rol | Responde por T8 | Operaciones |

## 🔍 Investigación complementaria
### Tema investigado:
STRIDE (Shostack, 2014), Zero Trust (NIST SP 800-207), OWASP Top 10 y riesgos de IA agéntica (MITRE ATLAS).

### Resumen:
STRIDE clasifica amenazas por violación de una propiedad de seguridad (autenticidad, integridad, no repudio, confidencialidad, disponibilidad y autorización). Se aplicó sobre cada elemento del DFD y se priorizó por impacto × probabilidad. Los principios Zero Trust de NIST SP 800-207 (no confiar por ubicación de red, mínimo privilegio, verificación continua) orientan las mitigaciones de T2, T4 y T6.

**Riesgos agénticos (MITRE ATLAS y patrón de sistemas agénticos).** STRIDE no cubre bien: alucinación, inyección de prompt (*LLM Prompt Injection*), autonomía sin supervisión, costo descontrolado, fuga de PII por el contexto y falta de explicabilidad. T7 documenta el caso crítico (fuga de PII hacia el proveedor de LLM); los seis riesgos se mitigan con seis *Requirements* en la vista [`vista-sistema-agentico-ban-i-bot.drawio`](../../archimate-transversal/vista-sistema-agentico-ban-i-bot.drawio).

### Homologación normativa y MRAE v3.0
- **Circular Externa 008 de 2023 (SFC):** monitoreo continuo (SOC 24/7), gestión de incidentes, seguridad en la nube y continuidad.
- **MAE (Arquitectura de Seguridad):** `MAE.LI.AS.01` (catálogo de servicios de seguridad/ciberseguridad), `AS.02` (Análisis de Impacto del Negocio, BIA), `AS.03` (Arquitectura de Seguridad) y `AS.04` (Ciberseguridad consolidada).
- **MGGTI (Gestión de Seguridad):** `GS.01` (implementación MSPI), `GS.02` (matriz y plan de tratamiento de riesgos: la tabla STRIDE), `GS.03` (controles) y `GS.04` (monitoreo continuo).
- **ISO/IEC 27001:2022** como marco de controles (vía MSPI) y **Ley 1581 de 2012** para T4 y T7.

### Vista ArchiMate equivalente
Cada mitigación es un *Requirement* en la capa de Motivación que *influye* sobre el componente que protege (por ejemplo, el filtro DLP sobre el Orquestador Agéntico).

## 📚 Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 5 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
