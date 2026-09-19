# 📚 Referencias Bibliográficas e Investigación Complementaria

**Taller 7 — Opportunities & Solutions: Diseño del TO-BE y Análisis de Brechas**  
*Caso de Estudio: Ban100 (Establecimiento Bancario Comercial)*  
**Equipo de Trabajo:** Santiago Barrera Rueda, Krish Purmessur Moros, Samuel Guerrero Arcos  
**Curso:**Arquitectura Empresarial — Universidad de La Sabana    
**Fecha:** 12 de Septiembre de 2026  

---

## 1. Patrones de Solución Arquitectural Investigados

Para fundamentar técnicamente las propuestas del estado objetivo (TO-BE), se investigaron los patrones arquitecturales líderes adoptados en la banca moderna y el sector financiero internacional:

### 1.1 Patrón Strangler Fig (Estrangulamiento Progresivo de Monolitos)
- **Fuente:** Fowler, M. (2004). *Strangler Fig Application*. MartinFowler.com.
- **Aplicación en Ban100:** Permite descomponer el Core Bancario Legacy on-premise de Bogotá de forma paulatina. En lugar de una reescritura total de alto riesgo ("Big Bang"), el API Gateway y una fachada anti-corrupción (*Anti-Corruption Layer - ACL*) interceptan progresivamente llamadas de cuentas de depósito y cartera, enrutándolas hacia los nuevos microservicios en Kubernetes hasta que el monolito sea retirado con cero impacto operacional.

### 1.2 Change Data Capture (CDC) y Arquitectura de Streaming de Eventos
- **Fuente:** Kleppmann, M. (2017). *Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems*. O'Reilly Media.
- **Aplicación en Ban100:** Soluciona el cuello de botella del batch nocturno (INF-2). Mediante conectores Debezium sobre los transaction logs (WAL) de la base de datos relacional del Core, los cambios se transmiten en sub-segundos a tópicos de Apache Kafka, manteniendo sincronizados en tiempo real el Master Data Management (MDM), el Lakehouse y el Directorio de Llaves Bre-B.

### 1.3 Resiliencia Activa-Activa Multi-Región con Kafka MirrorMaker 2
- **Fuente:** Confluent Inc. (2023). *Multi-Region Kafka Architectures: Active-Active and Disaster Recovery Patterns for Financial Services*. Confluent Developer Whitepapers.
- **Aplicación en Ban100:** Aborda la brecha de continuidad en pagos inmediatos Bre-B (INF-4 / NOR-2). La replicación bidireccional asíncrona de eventos de pago y estados de llaves entre Bogotá y Medellín garantiza que el RTO caiga a menos de 1 segundo con RPO = 0, evitando timeouts en la cámara de compensación del Banco de la República.

### 1.4 Autenticación FIDO2 / WebAuthn y Biometría Facial Pasiva (iBeta Nivel 2)
- **Fuente:** FIDO Alliance. (2022). *FIDO2: Moving the World Beyond Passwords*. FIDO Alliance Technical Specifications.
- **Aplicación en Ban100:** Mitiga la amenaza de suplantación STRIDE T1. Al registrar credenciales de clave pública respaldadas en hardware en el enclave seguro del smartphone del cliente y combinarlas con detección de vida pasiva certificada (Truora), se erradica el riesgo de fraude mediante inyección de video sintético o deepfakes.

### 1.5 Dynamic Data Masking (DDM) y Cifrado Transparente en Reposo (TDE)
- **Fuente:** Microsoft Learn & ISO/IEC 27040. (2023). *Dynamic Data Masking for Database Security and Storage Security Standards*.
- **Aplicación en Ban100:** Resuelve la brecha de exposición de datos sensibles en convenios con pagadurías (STR-4 / NOR-4). Las reglas de enmascaramiento se aplican dinámicamente en el motor relacional para usuarios operativos sin modificar las sentencias SQL de los microservicios ni alterar los esquemas de archivos de nómina.

### 1.6 Almacenamiento Inmutable WORM (Write Once, Read Many) y Hash Chaining
- **Fuente:** NIST SP 800-92. (2006). *Guide to Computer Security Log Management*. National Institute of Standards and Technology.
- **Aplicación en Ban100:** Mitiga el repudio y borrado de logs por insiders (STR-8 / Circular 008 SFC). Al depositar trazas transaccionales en almacenamiento cloud bloqueado por políticas de cumplimiento WORM y encadenadas mediante hashes criptográficos SHA-256 continuos, se garantiza valor probatorio pleno ante juzgados y entes de control.

---

## 2. Marco Normativo y Regulatorio Colombiano Consultado

1. **Superintendencia Financiera de Colombia (SFC).** *Circular Externa 008 de 2023: Instrucciones relativas a la gestión de la seguridad de la información y la ciberseguridad, y actualización de las directrices para la prestación de servicios financieros a través de canales e infraestructuras tecnológicas*. Bogotá D.C., 2023.
   - *Justificación técnica:* Fundamento de los requerimientos de DRP activo-activo (RTO/RPO), autenticación robusta adaptativa, monitoreo SOC 24/7 y custodia inmutable de pistas de auditoría.

2. **Congreso de la República de Colombia.** *Ley Estatutaria 1581 de 2012: Por la cual se dictan disposiciones generales para la protección de datos personales (Habeas Data)*. Diario Oficial No. 48.587, 2012.
   - *Justificación técnica:* Soporte legal para el diseño del Módulo de Autoservicio de Derechos ARCO (NOR-1), la actualización del inventario en el RNBD (NOR-3) y las políticas de retención temporal y purga TTL (NOR-7).

3. **Banco de la República de Colombia.** *Circular Reglamentaria Externa DSP-2023: Reglamentación del Sistema de Pagos Inmediatos Interoperables (Bre-B) y Adopción del Estándar ISO 20022*. Bogotá D.C., 2023.
   - *Justificación técnica:* Parámetros mandatorios de disponibilidad 24/7/365, mensajería `pacs.008`, `pacs.002` y validación indisoluble de Llaves telefónicas para la solución Bre-B multi-región.

4. **Congreso de la República de Colombia.** *Ley 527 de 1999: Por medio de la cual se define y reglamenta el acceso y uso de los mensajes de datos, del comercio electrónico y de las firmas digitales*. Diario Oficial No. 43.673, 1999.
   - *Justificación técnica:* Sustento de plena validez jurídica ejecutiva para la desmaterialización de pagarés con firma electrónica y estampado cronológico custodiados en DECEVAL (STR-3).

5. **Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC).** *Marco de Referencia de Arquitectura Empresarial (MRAE v3.0) — Dominios de Negocio, Información, Aplicaciones, Tecnología y Seguridad*. Bogotá D.C., 2023.
   - *Justificación técnica:* Estructura metodológica para la articulación entre los plateaus AS-IS y TO-BE en el marco del Estado colombiano.

---

## 3. Estándares Técnicos Internacionales Aplicados

1. **The Open Group.** *TOGAF® Standard, 10th Edition — Phase E: Opportunities and Solutions*. The Open Group Standard, 2022. URL: https://pubs.opengroup.org/architecture/togaf10-doc/arch-dev-method/chap07.html
2. **The Open Group.** *ArchiMate® 3.2 Specification — Implementation and Migration Layer (Plateaus, Gaps and Work Packages)*. The Open Group, 2022. URL: https://pubs.opengroup.org/architecture/archimate32-doc/
3. **OWASP Foundation.** *OWASP Top 10:2021 — The Ten Most Critical Web Application Security Risks*. Open Web Application Security Project, 2021. URL: https://owasp.org/Top10/
4. **W3C.** *Content Security Policy Level 3*. World Wide Web Consortium Recommendation, 2023. URL: https://www.w3.org/TR/CSP3/
5. **NIST.** *Special Publication 800-207: Zero Trust Architecture*. National Institute of Standards and Technology, 2020. URL: https://doi.org/10.6028/NIST.SP.800-207

---

_Este documento complementa y sustenta la entrega del Taller 7 del curso AREM — Universidad de La Sabana._
