# 📄 Informe Técnico del Taller

## Nombre del Taller
_Taller 2 - Modelo de Información (ERD) y Diagrama de Contexto de Negocio_

## Integrantes del equipo
- Santiago Barrera Rueda
- Krish Purmessur Moros
- Samuel Guerrero Arcos

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A.

## Descripción general del trabajo
Se construyó el modelo de información del flujo de **originación, recaudo B2G y titularización de libranza** (ERD en tercera forma normal con 8 entidades) y el **diagrama de contexto de negocio** que sitúa a Ban100 frente a sus actores y sistemas externos. Ambos derivan del proceso BPMN del Taller 1: cada dato que cruza un carril aparece como atributo o como flujo etiquetado.

## Proceso de desarrollo
**ERD.** (1) Entidades a partir de los datos del BPMN (cliente, solicitud, crédito, pagaré, pagaduría, convenio, descuento y emisión); (2) atributos y clave primaria subrayada (`PK`) más claves foráneas (`FK`); (3) relaciones nombradas con un verbo; (4) cardinalidad `1:1` o `1:N` en cada extremo. **Contexto.** (1) Actores y sistemas externos; (2) límite organizacional con cuatro sistemas internos; (3) flujos; (4) etiquetado de cada flujo con el dato intercambiado y borde punteado para terceros.

## Análisis del modelo propuesto
### A. Modelo entidad-relación (3FN)
| Relación | Verbo | Cardinalidad |
|---|---|---|
| CLIENTE — SOLICITUD_LIBRANZA | radica | 1:N |
| PAGADURIA_PUBLICA — SOLICITUD_LIBRANZA | certifica cupo de | 1:N |
| PAGADURIA_PUBLICA — CONVENIO_SECOP | suscribe | 1:N |
| SOLICITUD_LIBRANZA — CREDITO_LIBRANZA | origina | 1:1 |
| CREDITO_LIBRANZA — PAGARE_DIGITAL | se instrumenta en | 1:1 |
| CREDITO_LIBRANZA — DESCUENTO_NOMINA | se recauda mediante | 1:N |
| CONVENIO_SECOP — DESCUENTO_NOMINA | ampara | 1:N |
| CREDITO_LIBRANZA — TITULARIZACION_ESG | se cede a | 1:N |

- **Normalización.** Cada atributo depende de la clave, de toda la clave y solo de la clave: los datos de la pagaduría (NIT, municipio DANE, clúster y grupo MRAE, modalidad de integración) viven solo en `PAGADURIA_PUBLICA`; el contrato SECOP II y el RUP `719325524` solo en `CONVENIO_SECOP`; el hash biométrico solo en `CLIENTE`.
- **Resolución de N:N.** La relación real entre créditos y series de emisión es muchos a muchos; se resuelve porque `TITULARIZACION_ESG` actúa como **entidad asociativa**: cada fila es la cesión de un crédito (`FK num_operacion_core`) a una emisión del RNVE (`PK id_emision_rnve`, serie, monto, calificación y sello ESG). Análogamente, `DESCUENTO_NOMINA` resuelve la relación entre créditos y convenios. No queda ninguna relación N:N sin resolver.
- **Trazabilidad con el negocio.** `tiempo_aprobacion_min` en `SOLICITUD_LIBRANZA` permite medir la meta de < 15 minutos; `cluster_mrae_1_2_3` y `grupo_mrae_t1_t5` clasifican a cada pagaduría según el MRAE; `hash_sha256_ley527` y `timestamp_firma_electronica` soportan el no repudio (Ley 527 de 1999).

### B. Diagrama de contexto
- **Límite:** *Ban100 S.A.* con *Canales Digitales y Ban-I Bot*, *Motor de Originación y Scoring*, *Cliente 360 MDM* y *Core Bancario y Cartera*.
- **Actores:** Pensionado / Empleado Público, Microempresario, Oficial de Cumplimiento / Analista Operativo.
- **Sistemas externos (borde punteado):** Pagadurías Públicas Nacionales y Territoriales, Truora Biometría y Firma, Centrales de Riesgo TransUnion/DataCrédito, SFC / RNVE-SIMEV y Bre-B Banco de la República.
- **Supuestos.** El Oficial de Cumplimiento interactúa con el Cliente 360 para revisar alertas SARLAFT; los descuentos de nómina retornan por la misma interfaz de las pagadurías.

## Diagrama final entregado
- [Ver ERD en draw.io](./modelo-final-er.drawio)
- [Ver Diagrama de Contexto en draw.io](./diagrama-contexto-final.drawio)

## Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| CLIENTE | Entidad | Pensionado, empleado público o microempresario (estrato, género, hash biométrico Truora) | Gerencia Comercial |
| SOLICITUD_LIBRANZA | Entidad | Solicitud con canal, monto, puntaje de scoring y tiempo de aprobación | Originación |
| CREDITO_LIBRANZA | Entidad | Operación en el Core (`num_operacion_core`) con tasa, plazo, cuota y estado de cartera | Operaciones |
| PAGADURIA_PUBLICA | Entidad | Entidad pagadora (NIT, municipio DANE, clúster y grupo MRAE, modalidad API/RPA) | Convenios B2G |
| CONVENIO_SECOP | Entidad | Contrato SECOP II con RUP `719325524`, vigencia y estado | Jurídica |
| DESCUENTO_NOMINA | Entidad | Recaudo por periodo de nómina y estado de conciliación | Tesorería |
| PAGARE_DIGITAL | Entidad | Pagaré desmaterializado con hash SHA-256 y custodia | Cumplimiento |
| TITULARIZACION_ESG | Entidad asociativa | Cesión de créditos a emisiones RNVE con calificación AAA y sello ESG | Mercado de Capitales |
| Canales Digitales y Ban-I Bot | Sistema interno | App, Sucursal Virtual y asistente conversacional | Gerencia Digital |
| Motor de Originación y Scoring | Sistema interno | μS que valida, califica y orquesta la solicitud | TI |
| Cliente 360 MDM | Sistema interno | Repositorio maestro del cliente | Datos |
| Core Bancario y Cartera | Sistema interno | Sistema transaccional de cartera y desembolso | TI |

## Investigación complementaria
### Tema investigado:
Gobierno de datos (DAMA-DMBOK) y homologación con los lineamientos de información del MRAE v3.0.

### Resumen:
DAMA-DMBOK define la modelación de datos como disciplina que parte de entidades, atributos y relaciones con reglas de negocio explícitas; se aplicó su guía de normalización hasta 3FN y de identificación de entidades asociativas. El MRAE v3.0 traduce ese enfoque en el dominio de **Arquitectura de Información**.

Homologación MRAE: `MAE.LI.AI.01` (catálogo de flujos: los 12 flujos del diagrama de contexto), `AI.02` (inventario de activos de información: las 8 entidades), `AI.03` (intercambio interinstitucional, 1,03 % del esfuerzo: pagadurías, SFC, RNVE y Bre-B) y `AI.04` (Modelo de Información Institucional, nuevo en v3.0: este ERD). En el pilar MGGTI: `GI.01` (gobierno de datos), `GI.02` (calidad), `GI.03` (documentos electrónicos: pagaré digital), `GI.05` (publicación de servicios de intercambio), `GI.06` (ANS de intercambio) y `GI.08` (analítica descriptiva, predictiva y prospectiva, nuevo en v3.0, aplicable al scoring).

### Vista ArchiMate equivalente
| Elemento del taller | Elemento ArchiMate 3.2 |
|---|---|
| Entidad del ERD | Data Object |
| Sistema interno del contexto | Application Component |
| Sistema externo punteado | Application Service (externo) |
| Flujo etiquetado | Flow / Access |

## Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 2 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
