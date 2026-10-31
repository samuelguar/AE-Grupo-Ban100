# 📄 Ficha de Caracterización del Cliente

**Nombre del Equipo:** Ban100 — Grupo de Arquitectura Empresarial
**Fecha:** 31 de octubre de 2026
**Nombre del Cliente:** Dato reservado / No disponible en fuentes públicas verificadas (Canal institucional: Relación con Inversionistas y Defensoría del Consumidor Financiero Ban100 S.A.)
**Rol/Organización:** Presidencia Ejecutiva — Ban100 S.A. (Bancien S.A.)

**Integrantes:** Santiago Barrera Rueda · Krish Purmessur Moros · Samuel Guerrero Arcos
**Curso:** Arquitectura Empresarial (AREM) — Universidad de La Sabana, Facultad de Ingeniería. Docente: Prof. Ing. César Augusto Vega Fernández.

## I. Información General del Negocio
- Nombre de la empresa o entidad: **Ban100 S.A.** (registrada de forma indistinta como **Bancien S.A. y/o Ban100 S.A.**). NIT `900.200.960-9`; Matrícula Mercantil `01775679` (Cámara de Comercio de Bogotá).
- Sector económico: servicios financieros — establecimiento bancario comercial (CIIU `6412`, bancos comerciales), vigilado por la Superintendencia Financiera de Colombia (SFC) y emisor de valores en el RNVE / SIMEV.
- Número de empleados / usuarios / clientes: **399 colaboradores** (55,3 % mujeres) y **202.235 clientes de crédito** activos (49 % mujeres y 51 % hombres; 85 % en estratos 1, 2 y 3).
- Ubicación principal (física o digital): Bogotá D.C. (domicilio principal); **10 oficinas físicas** para captación y canales digitales de punta a punta; cobertura de **965 municipios en 2024** y **más de 1.000 municipios en 2025** (90 % de los 1.101 municipios de Colombia).
- Tecnologías principales actuales:
  - Canales digitales: App móvil, Sucursal Virtual (web) y WhatsApp / Ban-I Bot Libranza, con biometría facial y firma electrónica en línea integradas con Truora S.A.S.
  - Plataforma de servicios en nube pública (Kubernetes): API Gateway y microservicio de Originación y Scoring, con Cliente 360 (MDM).
  - Core Bancario transaccional en centro de datos On-Premise y SOC 24/7 de monitoreo y ciberseguridad.

## II. Objetivos Estratégicos
1. **Inclusión financiera:** sostener y ampliar la cobertura en 1.000+ municipios (55 % de la cartera colocada en ciudades y municipios con menos de 500.000 habitantes) para la base de la pirámide y la *Silver Economy* (pensionados).
2. **Capital de confianza:** mantener la calificación **AAA con certificación ESG** de las titularizaciones de cartera de libranza (emisiones de COP $90.000 millones, COP $250.000 millones y COP $48.000 millones; dos programas aprobados por la SFC hasta por COP $1 billón).
3. **Originación inmediata:** reducir el ciclo de originación de libranza de **3–5 días a menos de 15 minutos**, con el 100 % de solicitudes y aprobaciones digitales.
4. **Cumplimiento y resiliencia:** cumplir la Circular Externa 008 de 2023 de la SFC, el MSPI, la Ley 1581 de 2012 y la Ley 527 de 1999, y converger de forma voluntaria con el MRAE v3.0 (Decreto 767 de 2022).

## III. Problemas o necesidades identificadas
> Descritos como síntomas del negocio, no como soluciones técnicas ya decididas.

- Problema #1: **Retraso de 3 a 5 días** en la validación de cupos y la visación de libranzas con pagadurías territoriales de baja madurez digital (850–880 municipios en los Grupos Territoriales 3, 4 y 5 del MRAE, con puntajes de arquitectura entre 40,5 y 56,3).
- Problema #2: **Concentración del negocio:** el 94 % de la colocación total es libranza y el 98,3 % de ese segmento se coloca entre pensionados y empleados de gobierno; cualquier demora o interrupción en una pagaduría afecta casi toda la originación.
- Problema #3: **Riesgo de suplantación y de incumplimiento** en una base de clientes con perfil vulnerable (pensionados, estratos 1–3) que contrata sin oficina: la identidad y el consentimiento deben quedar probados ante la SFC y la SIC.
- Problema #4: **Gobierno de arquitectura incompleto:** el diagnóstico de madurez MAE está en Nivel 3 (Gestionado) en transición a Nivel 4; no existe un repositorio unificado de AE bajo metamodelo MRAE ni métricas automatizadas.

## IV. Procesos clave del negocio
- Originación de crédito de libranza 100 % digital y visación B2G con pagadurías (proceso modelado en el Taller 1).
- Recaudo mediante descuento directo de nómina o mesada pensional bajo convenios SECOP II (por ejemplo, contratos `CO1.PCCNTR.6460767` y `CO1.PCCNTR.4097470` con la Gobernación del Caquetá, RUP `719325524`).
- Colocación de microcrédito (COP $500.000 a COP $100 millones; ticket promedio de COP $6 millones) y crédito de consumo.
- Captación mediante cuentas de ahorro y CDT (10 oficinas y canales digitales).
- Titularización de cartera de libranza con calificación AAA ESG.

## V. Expectativas frente a la solución
- Identificar qué brechas cerrar primero para originar libranza en menos de 15 minutos sin depender de la madurez digital de cada pagaduría.
- Recibir una arquitectura que permita crecer en municipios y productos sin rehacer el Core Bancario.
- Contar con un diagnóstico de riesgos y de cumplimiento (SFC, SIC, MRAE) trazable hasta un plan por fases.

**Restricciones:**
- Ban100 **no es sujeto obligado directo** del MRAE v3.0 ni reporta el subíndice de Arquitectura en el FURAG; la operación B2G está sujeta a los plazos MRAE de sus contrapartes (40–47 meses en los Grupos Territoriales 3 a 5).
- Ventanas de mantenimiento programadas de máximo 30 minutos nocturnos (por ejemplo, domingos de 10:00 p. m. a 10:30 p. m.).
- Toda decisión debe respetar la supervisión de la SFC (Circular Básica Contable y Financiera 100 de 1995, Circular Externa 008 de 2023, SARLAFT) y el reconocimiento pasivo autorizado (sin pruebas activas sobre sistemas reales).

## VI. Persona de contacto
- Nombre del contacto: Dato reservado / No disponible en fuentes públicas verificadas (Canal institucional: Relación con Inversionistas y Defensoría del Consumidor Financiero Ban100 S.A.)
- Correo electrónico / teléfono: Dato reservado / No disponible en fuentes públicas verificadas (Canal institucional: Relación con Inversionistas y Defensoría del Consumidor Financiero Ban100 S.A.)
- Rol o vínculo con la solución: patrocinio de la Presidencia Ejecutiva sobre los objetivos estratégicos (stakeholder de la capa de Motivación).

---

## Anexo A — Caracterización societaria, financiera y regulatoria

### A.1 Evolución histórica y naturaleza jurídica
| Hito | Fecha | Detalle |
|---|---|---|
| Constitución | 8 de febrero de 2008 (inscrita el 19 de febrero de 2008) | **Banco ProCredit Colombia S.A.**, filial de *ProCredit Holding AG & Co KGaA* |
| Fusión inversa | 3 de enero de 2020 | Adquisición y fusión con **Credifinanciera S.A. Compañía de Financiamiento**; nace **Banco Credifinanciera S.A.** |
| Cambio de identidad | 2 de febrero de 2023 | Razón social **Ban100 S.A.** (reformas estatutarias inscritas en mayo y junio de 2023) |

Naturaleza jurídica: sociedad anónima de derecho privado; establecimiento bancario comercial vigilado por la SFC; emisor de valores en el RNVE / SIMEV. Revisoría Fiscal externa: **EY Audit S.A.S.**

### A.2 Composición accionaria (100 % privada)
| Accionista | Participación | Acciones |
|---|---:|---:|
| Finanza Inversiones S.A.S. | **94,50 %** | 168.152.187 |
| Inversiones y Consultoría Tributaria S.A.S. | 3,50 % | 6.226.740 |
| Alciento S.A.S. / Direcciones de Negocio S.A.S. | 1,00 % | 1.779.384 |
| Asesorías Financieras y Corporativas | 1,00 % | 1.779.384 |
| Asistencia de Comercio S.A.S. | 0,00 % | 1.106 |

Respaldo internacional de fondos de capital privado en mercados emergentes como *Gramercy* (activos bajo administración entre USD 5.300 millones y USD 5.800 millones) y fondeadores de impacto como *ResponsAbility Investments AG*.

### A.3 Magnitud patrimonial, financiera y mercado de capitales
| Indicador | Valor |
|---|---|
| Patrimonio base de liquidación SFC | COP $227.768 millones |
| Activos registrados | COP $2,82 billones |
| Utilidad antes de impuestos (cierre 2024) | COP $10.448 millones |
| Calificación de riesgo emisor | Largo plazo **AA-** · Corto plazo **BRC1+ / F1+** |
| Titularizaciones de libranza (Sustainable Fitch) | **AAA con certificación ESG (Sostenible)**: COP $90.000 millones, COP $250.000 millones y COP $48.000 millones; dos programas aprobados por la SFC hasta COP $1 billón |

### A.4 Huella comercial y portafolio
| Indicador | Valor |
|---|---|
| Clientes de crédito | 202.235 (85 % estratos 1–3; 49 % mujeres / 51 % hombres) |
| Cartera en municipios < 500.000 habitantes | 55 % |
| Cobertura municipal | 77 % (2022) → 965 municipios (2024) → más de 1.000 (2025) = 90 % de 1.101 |
| Peso de la libranza | 94 % de la colocación; 98,3 % de la libranza en pensionados y empleados de gobierno |
| Créditos originados digitalmente (2024) | 95 % (100 % en solicitudes y aprobaciones de libranza) |
| Reducción del uso de papel (2024) | 29 % (`PRI_09`, `MGGTI.LI.GI.03`) |
| Capacitación (2024) | 94,7 % de cobertura (+8,4 pp vs. 2023); 5.853 horas; 91,3 % en la escuela de liderazgo; 82,2 % en categoría "sobresaliente" |

Cinco líneas de producto (`MAE.LI.AIN.04`): Crédito de Libranza, Microcrédito, Crédito de Consumo, Cuentas de Ahorro y CDT.

### A.5 Estatus regulatorio frente al Decreto 767 de 2022 y al MRAE v3.0
Al contrastar el directorio SIGEP de la matriz oficial de plazos del MinTIC (`articles-204807_recurso_5.xlsx`) con las entidades vigiladas por la SFC, **Ban100 S.A. no es sujeto obligado directo**: no integra la Administración Pública (art. 39 de la Ley 489 de 1998) ni cumple funciones administrativas delegadas (art. 2.2.9.1.1.2 del Decreto 1078 de 2015, subrogado por el Decreto 767 del 16 de mayo de 2022). En contraste, el *Banco Agrario de Colombia S.A.* (SIGEP 6193), la *Financiera de Desarrollo Nacional* (SIGEP 1321) y *Fiducoldex S.A.* (SIGEP 6389) son sujetos obligados del Clúster 3 del Orden Nacional (10–12 meses al 40 %, 17–20 al 70 % y 23–27 al 100 %).

Los **tres vectores de convergencia** con el MRAE v3.0:
1. **Grupo de Interés y PNID:** el parágrafo del art. 2.2.9.1.2.1 del Decreto 1078 de 2015 incluye al sector privado como Grupo de Interés de la Política de Gobierno Digital; `PRI_04` y el Plan Nacional de Infraestructura de Datos promueven la interoperabilidad público-privada.
2. **Dependencia operativa B2G por libranza:** convenios en SECOP II con entidades territoriales (contratos `CO1.PCCNTR.6460767`, periodo 2024–2026, y `CO1.PCCNTR.4097470`, periodo 2022–2024, con la Gobernación del Caquetá, RUP `719325524`).
3. **Homologación técnica frente a la SFC:** el MRAE integra TOGAF, CMMI, GAO, Gartner ITScore, PMI OPM3, ITIL e ISO/IEC 27001 (vía MSPI), útiles como marco de auditoría para la Circular Básica Contable y Financiera 100 de 1995, la Circular Externa 008 de 2023, SARLAFT y riesgo operativo.

### A.6 Estructura del MRAE v3.0 y diagnóstico de madurez
| Pilar | Lineamientos | Peso del esfuerzo | Horas (Opt. / Pes.) |
|---|---:|---:|---|
| MAE — Modelo de Arquitectura Empresarial | 29 | 34,03 % | 772 h / 1.953,84 h |
| MGGTI — Modelo de Gestión y Gobierno de TI | 63 | 58,10 % | 1.320 h / 3.332,20 h |
| MGPTI — Modelo de Gestión de Proyectos de TI | 14 | 7,87 % | 179 h / 448,0 h |
| **Total** | **106** | 100 % | 2.271 h / 5.734 h |

Instrumento de madurez (`articles-204807_recurso_4.xlsx`, **300 ítems**): MAE 60 elementos (GAO + CMMI) → **Nivel 3 (Gestionado / Etapa 4 GAO) en transición a Nivel 4**; MGGTI 202 criterios sobre 70 elementos (Gartner ITScore + CMMI) → **Nivel 4 (Diferenciador / Manejado)** con atributos en Nivel 5; MGPTI 38 elementos (PMI OPM3 + CMMI) → **Nivel 4 (Gestionado / Manejado)**.

---

_Este documento hace parte de la entrega del Taller 0 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
