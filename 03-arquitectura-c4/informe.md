# Taller 3 — Arquitectura C4: Vista de Contexto (C1) y Vista de Contenedores (C2)

## Equipo: Ban100 — Grupo de Arquitectura Empresarial

**Asignatura:** Arquitectura Empresarial (AREM) — Universidad de La Sabana  
**Integrantes:** Santiago Barrera Rueda, Krish Purmessur Moros, Samuel Guerrero Arcos  
**Fecha de entrega:** Agosto 2026  
**Marco metodológico:** MRAE v3.0 MinTIC + TOGAF ADM  
**Modelo de referencia:** C4 Model — Simon Brown

---

## 1. Proceso de Modelado

### 1.1 Metodología Aplicada

Se siguió la guía de 4 pasos definida en el material de clase para cada nivel del modelo C4:

| Paso | C1 — Vista de Contexto | C2 — Vista de Contenedores |
|------|------------------------|---------------------------|
| 1 | Identificar actores (personas que interactúan con el sistema) | Descomponer el sistema en contenedores por responsabilidad |
| 2 | Identificar el sistema en alcance y los sistemas externos | Ubicar la infraestructura de soporte compartida |
| 3 | Trazar relaciones directas entre actores, sistema y externos | Trazar relaciones entre contenedores, actores y sistemas externos |
| 4 | Etiquetar relaciones (verbo + información + protocolo) y validar | Etiquetar tecnologías y protocolos de comunicación, y validar |

### 1.2 Fuentes de Información

- Visión arquitectónica preliminar (`00-preliminary-vision/`)
- Modelo BPMN de originación de libranza (`01-bpmn/`)
- Modelo de información y ERD (`02-modelo-informacion/`)
- Documentación regulatoria: Circular Externa 008/2023 SFC, Ley 527/1999, Ley 1581/2012
- Documentación técnica: ISO 20022 (Bre-B), Truora API, WhatsApp Business API

---

## 2. C1 — Vista de Contexto del Sistema

### 2.1 Sistema en Alcance

**Plataforma Digital Ban100**: Plataforma bancaria omnicanal que gestiona originación de créditos de libranza, microcrédito, CDTs digitales, cuentas de depósito y pagos inmediatos Bre-B (ISO 20022). Incluye API Gateway, Core Bancario desacoplado en microservicios, MDM con visión 360° del cliente y SOC antifraude con IA predictiva.

### 2.2 Actores (Personas)

| Actor | Descripción | Interacción Principal |
|-------|-------------|----------------------|
| **Pensionados y Empleados** | Clientes con convenio de pagaduría | Solicitan libranzas, consultan saldos, realizan transferencias Bre-B |
| **Microempresarios e Independientes** | Clientes de inclusión financiera | Acceden a microcrédito productivo y servicios de ahorro digital |
| **Inversionistas CDT** | Clientes de captación | Constituyen y renuevan CDTs digitales por App, Web o WhatsApp |

### 2.3 Sistemas Externos

| Sistema Externo | Tipo | Relación con Ban100 |
|----------------|------|---------------------|
| **Truora S.A.S.** | Aliado tecnológico | Biometría facial (FIDO), OCR de cédulas, firma electrónica Ley 527, estampado cronológico |
| **Banco de la República (Bre-B)** | Infraestructura financiera nacional | Directorio Central de Llaves, cámara de pagos inmediatos 24/7, mensajería ISO 20022 |
| **Pagadurías Institucionales** | Entidades de convenio | Validación de cupos de descuento y capacidad de libranza |
| **Deceval** | Infraestructura de mercado de valores | Custodia de pagarés desmaterializados |
| **BTG Pactual & Titularizadora** | Aliado financiero | Titularización de cartera de libranzas (>$500kM COP) |
| **ResponsAbility Investments AG** | Fondeador internacional | Líneas de crédito para microfinanzas |
| **SFC** | Ente regulador | Supervisión, auditoría y cumplimiento Circular 008/2023 |
| **WhatsApp Business API** | Canal externo | Flujos conversacionales de autogestión financiera |

### 2.4 Diagrama C1

📁 Archivo: [`c1-contexto-ban100.drawio`](./c1-contexto-ban100.drawio)

---

## 3. C2 — Vista de Contenedores

### 3.1 Descomposición en Contenedores

El sistema se descompone en **5 capas** con **19 contenedores**:

#### Capa 1: Canales Digitales (Frontend)

| Contenedor | Tecnología | Responsabilidad |
|-----------|-----------|----------------|
| **App Móvil Ban100** | iOS / Android | Autogestión financiera, Bre-B QR, libranza y CDT |
| **Portal Transaccional Web** | SPA React | Gestión de cuentas, consultas y operaciones web |
| **Canal WhatsApp Bot** | WhatsApp Business API / Truora Bot | Flujos conversacionales de autogestión |

#### Capa 2: Perímetro y Seguridad

| Contenedor | Tecnología | Responsabilidad |
|-----------|-----------|----------------|
| **API Gateway Institucional** | API Gateway / K8s Ingress | mTLS, JWT, throttling, rate limiting, políticas Open Banking |
| **SOC & Motor Antifraude IA** | SIEM / ML Pipeline | Monitoreo 24/7, detección predictiva, logs inmutables SFC 008 |

#### Capa 3: Microservicios (Backend)

| Contenedor | Tecnología | Responsabilidad |
|-----------|-----------|----------------|
| **μS Originación de Libranza & Scoring** | Microservicio / K8s Pod | Orquesta solicitud, scoring, validación biométrica, firma y desembolso |
| **μS Validación de Convenios con Pagadurías** | Microservicio / K8s Pod | Consulta cupos disponibles y valida capacidad de descuento |
| **μS Módulo Bre-B & ISO 20022** | Microservicio / K8s Pod | Gestor de llaves, generación QR, transferencias inmediatas (pacs.008, pacs.002, pain.001) |
| **μS CDT Digital & Renovación** | Microservicio / K8s Pod | Constitución, renovación automática y liquidación de CDTs |
| **Core Bancario Desacoplado** | Microservicios Transaccionales / K8s | Cuentas de depósito, cartera, captaciones y contabilidad HA |
| **Master Data Management (MDM)** | Plataforma MDM / Golden Record | Visión 360° de clientes, productos y datos maestros unificados |
| **Event Streaming / Lakehouse** | Kafka / Spark / Event Store | Procesamiento en tiempo real, reemplaza batch nocturno |

#### Capa 4: Datos y Almacenamiento

| Contenedor | Tecnología | Responsabilidad |
|-----------|-----------|----------------|
| **BD Master Data Clientes** | RDBMS | Datos maestros unificados de clientes |
| **BD Core Transaccional** | RDBMS HA | Operaciones transaccionales del core bancario |
| **BD Llaves & Txn ISO 20022** | RDBMS + JSON Store | Directorio de llaves Bre-B y mensajes ISO 20022 |
| **Logs Auditoría SFC 008** | Immutable Append-Only Store | Pistas de auditoría forense con hash inmutable |
| **Lakehouse / Event Store** | Data Lakehouse | Eventos de negocio en tiempo real |

#### Capa 5: Infraestructura

| Contenedor | Tecnología | Responsabilidad |
|-----------|-----------|----------------|
| **Kubernetes Cluster (K8s)** | Nube Híbrida Multi-Región | Orquestación, auto-escalado, HA 99.99% |
| **CDN & VPN IPsec** | Comunicaciones | Baja latencia nacional, enlaces dedicados, túneles seguros |
| **DRP Activo-Activo** | Resiliencia | RTO < 5 min, RPO = 0 para Bre-B, contingencia multi-región |

### 3.2 Protocolos de Comunicación

| Origen | Destino | Protocolo | Descripción |
|--------|---------|-----------|-------------|
| Actores → Canales | App / Web / WhatsApp | HTTPS/JSON | Acceso del usuario a la plataforma |
| Canales → API Gateway | Gateway | HTTPS / Webhook | Centralización del tráfico entrante |
| API Gateway → μServicios | Microservicios Backend | HTTPS/JWT | Enrutamiento autenticado y autorizado |
| μS Originación → Truora | Truora S.A.S. | API REST / HTTPS | Validación biométrica y firma electrónica |
| μS Bre-B → Banco de la República | Bre-B | ISO 20022 (pacs.008, pacs.002) | Registro de llaves y pagos inmediatos |
| μS Pagadurías → Pagadurías | Institucionales | REST / Web Services | Consulta de cupos de libranza |
| μS Originación → Deceval | Deceval | API REST | Registro de pagarés desmaterializados |
| Core Bancario → BTG | BTG Pactual | API REST | Cesión de cartera para titularización |
| SOC → SFC | SFC | API Regulatoria | Transmisión de pistas de auditoría |
| Core → Event Streaming | Lakehouse | Kafka / Eventos | Publicación de eventos de negocio |
| μServicios → BDs | Bases de datos | SQL / JSON | Persistencia de operaciones |

### 3.3 Diagrama C2

📁 Archivo: [`c2-contenedores-ban100.drawio`](./c2-contenedores-ban100.drawio)

---

## 4. Equivalencia con ArchiMate

| Concepto C4 | Equivalente ArchiMate | Ejemplo Ban100 |
|------------|----------------------|----------------|
| Persona (Actor) | Business Actor | Pensionado, Microempresario, Inversionista |
| Sistema en Alcance | Application Component (agregado) | Plataforma Digital Ban100 |
| Contenedor | Application Component | μS Originación, API Gateway, Core Bancario |
| Relación C1 (verbo) | Serving / Association | "Solicita libranzas" |
| Relación C2 (protocolo) | Flow / Serving con tecnología | "HTTPS/JWT", "ISO 20022" |
| Sistema Externo | External Application Component | Truora, Bre-B, SFC |
| Base de datos | Technology Service / Data Object | BD Core Transaccional |

---

## 5. Debilidades y Riesgos Identificados

| # | Debilidad | Riesgo Asociado | Mitigación Propuesta |
|---|----------|----------------|---------------------|
| 1 | Dependencia crítica de Truora para todo el flujo de identidad | Single Point of Failure en verificación biométrica | Evaluar proveedor alternativo; implementar circuit breaker |
| 2 | Complejidad de integración ISO 20022 con Bre-B | Errores de formato en mensajería pueden bloquear pagos | Test suite con mensajes de prueba del BanRep; sandbox dedicado |
| 3 | Core Bancario en proceso de desacoplamiento | Período de transición con riesgo de inconsistencia | Migración gradual con patrón Strangler Fig; doble escritura temporal |
| 4 | Volumen de pagadurías distribuidas con APIs heterogéneas | Latencia y fallos en validación de cupos | Patrón adaptador por pagaduría; caché de cupos con TTL |
| 5 | Logs inmutables deben cumplir SFC 008 estrictamente | Incumplimiento regulatorio por fallos de escritura | Escritura sincrónica con retry exponencial; alerta SOC ante fallo |

---

## 6. Referencias

- Brown, S. (2023). *The C4 Model for Visualising Software Architecture*. https://c4model.com/
- MinTIC Colombia. *MRAE v3.0 — Marco de Referencia de Arquitectura Empresarial*. https://www.mintic.gov.co/
- Superintendencia Financiera de Colombia. *Circular Externa 008 de 2023*. Ciberseguridad y gestión de riesgos.
- Banco de la República. *Bre-B: Sistema de Pagos Inmediatos*. Mensajería ISO 20022.
- Truora S.A.S. *API Documentation — Identity Verification & Electronic Signature*.
- ISO. *ISO 20022: Universal Financial Industry Message Scheme*.
- Congreso de la República de Colombia. *Ley 527 de 1999 — Comercio Electrónico y Firma Digital*.
- Congreso de la República de Colombia. *Ley 1581 de 2012 — Protección de Datos Personales (Habeas Data)*.
