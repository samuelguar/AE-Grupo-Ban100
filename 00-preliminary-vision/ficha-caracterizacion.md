# Ficha de Caracterización del Cliente: Ban100

**Nombre del Equipo:** Equipo de Arquitectura Empresarial Ban100  
**Integrantes:**
- Santiago Barrera Rueda
- Krish Purmessur Moros
- Samuel Guerrero Arcos

**Fecha:** 21 de Agosto de 2026  
**Nombre del Cliente:** Héctor Chaves (Presidencia Ejecutiva) / Representación Institucional  
**Rol/Organización:** Presidencia Ejecutiva — Ban100 (Finanza Inversiones S.A.S.)

---

## I. Información General del Negocio

- **Nombre de la empresa o entidad:** Ban100 (Anteriormente Banco Credifinanciera S.A. / C.A. Credifinanciera).
- **Sector económico:** Sector Financiero y Bancario Colombiano — Establecimiento Bancario Comercial enfocado en Inclusión Financiera y Cartera de Consumo/Microcrédito.
- **Número de empleados / usuarios / clientes:** 
  - Más de 250.000 clientes activos en el territorio nacional.
  - Cobertura presencial y digital en más de 900 municipios de Colombia.
  - Estructura patrimonial robusta con calificaciones crediticias de grado de inversión otorgadas por Fitch Ratings ('AA-(col)' de largo plazo y 'F1+(col)' de corto plazo) y BRC Ratings - S&P Global ('AA-' y 'BRC 1+').
- **Ubicación principal (física o digital):** 
  - Sede Principal: Bogotá D.C., con presencia de sedes regionales y oficinas comerciales en nodos urbanos e intermedios (Cali, Medellín, Barranquilla, Bucaramanga, etc.).
  - Plataforma Digital: Portal transaccional web, Aplicación Móvil Ban100 y Canal Conversacional WhatsApp (Bot transaccional integrado).
- **Tecnologías principales actuales:**
  - **Core Bancario Tradicional:** Sistema transaccional monolítico centralizado para la administración de depósitos, cartera y captaciones.
  - **Plataformas de Identidad y Firma:** Integración API con **Truora** (Reconocimiento facial, biometría, validación OCR de documento de identidad y firma electrónica desmaterializada bajo Ley 527 de 1999).
  - **Canales de Contacto:** WhatsApp Business API integrado para trámites conversacionales de captación y consulta.
  - **Infraestructura de Cómputo:** Esquema híbrido (Centro de Datos principal On-Premise con servicios específicos aprovisionados en nube pública).
  - **Custodia y Titularización:** Conexión con Deceval para custodia de pagarés y plataformas de titularización con BTG Pactual y la Sociedad Titularizadora.

---

## II. Objetivos Estratégicos

1. **Escalar la Inclusión Financiera Multicanal:** Expandir la colocación de productos de crédito de libranza y microcrédito en más de 900 municipios, logrando una originación 100% digital que reduzca las barreras geográficas para pensionados y microempresarios.
2. **Interoperabilidad y Habilitación de Pagos Inmediatos 24/7:** Integrarse de manera nativa al Sistema de Pagos Inmediatos Interoperables (**Bre-B**) del Banco de la República, soportando transferencias en tiempo real mediante "Llaves" (celular, cédula, correo, código alfanumérico) y códigos QR bajo estándar ISO 20022.
3. **Optimización de Eficiencia Operativa y Automatización:** Reducir los costos y tiempos de ciclo en captaciones (CDT) y colocaciones (Libranzas), automatizando el 100% de la consulta de convenios con pagadurías y minimizando la intervención manual.
4. **Cumplimiento Regulatorio y Resiliencia en Ciberseguridad:** Adecuar la infraestructura tecnológica y los procesos al 100% de las directrices de la **Circular Externa 008 de 2023 de la Superintendencia Financiera de Colombia (SFC)** y adoptar una arquitectura Zero Trust con alta disponibilidad (99.99%).

---

## III. Problemas o Necesidades Identificadas

*Los problemas se describen a continuación como síntomas operativos y de negocio experimentados por la entidad y sus clientes:*

- **Problema #1: Tiempos de respuesta lentos y fricción en la originación de libranzas.**
  - *Síntoma:* La verificación manual de convenios con pagadurías institucionales y la recolección física de soportes retrasan el desembolso de los créditos durante varios días, generando insatisfacción en el cliente pensionado y pérdida de oportunidades comerciales frente a neobancos.
- **Problema #2: Fragmentación de la información del cliente y procesamiento por lotes (Batch).**
  - *Síntoma:* La existencia de silos de datos independientes por producto (libranza, CDT, cuentas de ahorro) impide tener una visión unificada 360° del cliente en tiempo real. La liquidación y actualización de saldos depende de procesos nocturnos por lotes, generando latencia operativa.
- **Problema #3: Rigidez del Core Monolítico e Integraciones Punto a Punto.**
  - *Síntoma:* La interconexión directa y no estandarizada entre aplicaciones dificulta la rápida integración con nuevos ecosistemas financieros (como Bre-B o banca abierta), elevando los costos de mantenimiento de TI y limitando la elasticidad ante picos de demanda.
- **Problema #4: Vulnerabilidad ante ventanas de mantenimiento y requerimientos reforzados de seguridad.**
  - *Síntoma:* La dependencia de infraestructura física on-premise obliga a programar ventanas de indisponibilidad técnica. Adicionalmente, el esquema de monitoreo perimetral tradicional requiere modernizarse frente a las exigencias de autenticación adaptativa y analítica antifraude continua exigidas por la SFC.

---

## IV. Procesos Clave del Negocio

1. **Originación y Desembolso Digital de Crédito de Libranza:** Flujo integral que comprende captura de solicitud, validación biométrica con Truora, verificación automática de capacidad y cupo en pagaduría, emisión/firma de pagaré desmaterializado y desembolso inmediato. *(Proceso seleccionado para modelado BPMN en Taller 1)*.
2. **Evaluación y Colocación de Microcrédito Productivo:** Proceso mixto (remoto/asistido) para evaluación de riesgo crediticio y financiamiento a microempresarios e independientes.
3. **Apertura y Renovación Digital de Certificados de Depósito a Término (CDT):** Proceso desmaterializado vía web, app o WhatsApp para captación de recursos e inversión.
4. **Procesamiento de Transferencias y Pagos Inmediatos Interoperables (Bre-B):** Registro de Llaves, enrutamiento, liquidación y notificación de transferencias 24/7 bajo ISO 20022.
5. **Gestión de Convenios con Pagadurías Institucionales:** Administración y conciliación de libranzas con entidades públicas, fondos de pensiones y empresas privadas.

---

## V. Expectativas Frente a la Solución

- Disponer de un marco estructurado de Arquitectura Empresarial (MRAE v3.0 MinTIC) que sincronice la estrategia de negocio con las inversiones en tecnología.
- Lograr una arquitectura desacoplada basada en Microservicios y APIs RESTful que facilite la conexión con aliados estratégicos y el Banco de la República.
- Garantizar la continuidad operativa 24/7/365 con un SLA de disponibilidad del 99.99% sin ventanas de mantenimiento que interrumpan el servicio.
- Asegurar la trazabilidad e inmutabilidad de los registros transaccionales para auditorías de la Superintendencia Financiera.

**Restricciones:**
- **Regulatoria Obligatoria:** Cumplimiento estricto de la Circular Externa 008 de 2023 de la SFC, Ley 527 de 1999 (validez de firma electrónica y mensajes de datos), Ley 1581 de 2012 (Habeas Data) y reglamentación Bre-B del Banco de la República.
- **Operativa:** El proceso de transformación debe convivir con la operación diaria de los 250.000 clientes actuales sin suspender los canales transaccionales.
- **Topológica:** Las soluciones deben desplegarse en un esquema de Nube Híbrida Multi-Región que asegure soberanía de datos y contingencia activa-activa.

---

## VI. Persona de Contacto

- **Nombre del contacto:** Comité de Transformación Digital y Arquitectura Empresarial Ban100 (Patrocinador: Presidencia Ejecutiva / Vicepresidencia de TI y Operaciones).
- **Correo electrónico / teléfono:** contacto.arquitectura@ban100.com.co / PBX (601) 307-8060.
- **Rol o vínculo con la solución:** Dirección Estratégica y Gobierno de TI para la implementación de la hoja de ruta de transformación digital institucional.

---

_Este documento hace parte de la entrega del Taller 0 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._

