# 📚 Referencias Bibliográficas y Técnicas del Taller 8: Integración de Vistas

Este archivo contiene las fuentes académicas, estándares internacionales y marcos regulatorios consultados para el desarrollo del **Taller 8 (Integración de Vistas de Arquitectura)** aplicado a **Ban100**, incluyendo el marco metodológico de integración multicapa y las referencias técnicas de los componentes del estado objetivo (TO-BE).

**Taller 8 — Integración de Vistas de Arquitectura: Caso Ban100**  
*Curso de Arquitectura Empresarial (AREM) — Universidad de La Sabana*

---

## 1. Estándares y Marcos de Arquitectura Empresarial

1. **The Open Group. (2022).** *ArchiMate® 3.2 Specification: A Pocket Guide*. Van Haren Publishing. ISBN: 978-9401809054. URL: https://www.opengroup.org/archimate-forum/archimate-overview  
   > *Aporte Técnico al Taller:* Proporcionó la fundamentación formal para el modelado multicapa y las relaciones de servicio verticales (`Serving`, `Realization`, `Assignment`, `Access`) que conectan los procesos de la Capa de Negocio con los componentes de la Capa de Aplicaciones y los nodos de la Capa de Infraestructura Tecnológica, eliminando la ambigüedad en el trazado de hilos de negocio.

2. **The Open Group. (2022).** *The TOGAF® Standard, 10th Edition: Architecture Development Method (ADM) — Phases E, F & H*. The Open Group Standard. URL: https://www.opengroup.org/togaf  
   > *Aporte Técnico al Taller:* Guio la consolidación entre el estado actual (AS-IS) y la arquitectura objetivo (TO-BE), articulando las 20 brechas diagnosticadas en Talleres 4 a 7 dentro de un esquema estructurado de plateaus y dependencias de migración previo a la formulación de los paquetes de trabajo del Taller 9.

3. **International Organization for Standardization / International Electrotechnical Commission / IEEE. (2022).** *ISO/IEC/IEEE 42010:2022 — Systems and software engineering — Architecture description*. Geneva: ISO. URL: https://www.iso.org/standard/74427.html  
   > *Aporte Técnico al Taller:* Se adoptaron los principios de vistas y puntos de vista (*views and viewpoints*) para asegurar que cada perspectiva arquitectónica (Negocio, Datos, Aplicaciones, Infraestructura y Seguridad) responda a los *concerns* de los diferentes grupos de interés (*stakeholders* bancarios: Presidencia, VP Riesgos, CISO y Operaciones).

4. **Brown, Simon. (2023).** *The C4 Model for Visualising Software Architecture: Context, Containers, Components and Code*. Leanpub. URL: https://c4model.com/  
   > *Aporte Técnico al Taller:* Permitió mapear de forma inequívoca los 19 contenedores de la Vista C2 desarrollados en el Taller 3 y extenderlos con los nuevos componentes TO-BE (FIDO2, CDC Debezium, ARCO y Réplica Bre-B en Medellín).

5. **Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC). (2023).** *Marco de Referencia de Arquitectura Empresarial (MRAE v3.0) — Dominio Institucional, Sistemas de Información e Infraestructura*. Bogotá D.C., Colombia. URL: https://www.mintic.gov.co/  
   > *Aporte Técnico al Taller:* Marco rector del curso que sustentó la alineación entre las dimensiones de gestión (MGGTI y MGPTI), los lineamientos de interoperabilidad del Estado colombiano y la inclusión financiera en más de 900 municipios.

---

## 2. Seguridad, Ciberseguridad y Normatividad Bancaria

6. **Superintendencia Financiera de Colombia (SFC). (2023).** *Circular Externa 008 de 2023: Instrucciones relativas a la administración del riesgo de ciberseguridad, resiliencia operativa y autenticación robusta*. Bogotá D.C.  
   > *Aporte Técnico al Taller:* Fundamentó la incorporación obligatoria en el tablero de las pistas de auditoría inmutables bajo estándar WORM (`db_worm`), el encadenamiento criptográfico de bloques (Hash Chaining SHA-256), la autenticación adaptativa multifactor (MFA) y los esquemas de conmutación de contingencia en tiempo real.

7. **Congreso de la República de Colombia. (2012).** *Ley Estatutaria 1581 de 2012: Régimen General de Protección de Datos Personales (Habeas Data)*. Diario Oficial No. 48.587.  
   > *Aporte Técnico al Taller:* Justificó la creación del Módulo de Derechos ARCO (`cnt_arco`) para la revocatoria digital de autorizaciones, el registro de bases de datos ante el RNBD de la SIC (`norm_rnbd`) y las rutinas de depuración automática con políticas TTL de 30 días para datos biométricos desistidos (`norm_ttl`).

8. **Congreso de la República de Colombia. (1999).** *Ley 527 de 1999: Por medio de la cual se define y reglamenta el acceso y uso de los mensajes de datos, del comercio electrónico y de las firmas digitales*. Diario Oficial No. 43.673.  
   > *Aporte Técnico al Taller:* Respaldó la validez probatoria y ejecutiva de los pagarés desmaterializados con estampado cronológico (*time-stamping*) custodiados en DECEVAL, blindando el proceso de originación de libranza contra el riesgo de repudio judicial (`STR-3`).

9. **FIDO Alliance. (2022).** *FIDO2: WebAuthn & Client to Authenticator Protocol (CTAP) Implementation Guidelines*. FIDO Alliance Technical Specifications. URL: https://fidoalliance.org/specs/fido-v2.1-ps-20210615/  
   > *Aporte Técnico al Taller:* Especificó la arquitectura de autenticación asimétrica hardware-backed implementada en el servidor FIDO2 (`cnt_fido`) integrado con la biometría iBeta Nivel 2 de Truora para neutralizar ataques de suplantación facial mediante deepfakes sintéticos (`STR-1`).

---

## 3. Patrones Tecnológicos y Sistemas de Información Financiera

10. **Banco de la República de Colombia. (2023).** *Reglamentación del Sistema de Pagos Inmediatos Interoperables (Bre-B) y Catálogo de Mensajería ISO 20022*. Circular Reglamentaria Externa DSP-2023. Bogotá D.C.  
    > *Aporte Técnico al Taller:* Estableció los requerimientos de SLA (99.99%), latencia máxima (< 3s) y estructura de mensajes XML/JSON (`pacs.008` para transferencias, `pacs.002` para confirmaciones y `pain.001` para iniciación) que rigen el Módulo Bre-B en Bogotá y Medellín.

11. **Fowler, Martin. (2020).** *Strangler Fig Application*. MartinFowler.com. URL: https://martinfowler.com/bliki/StranglerFigApplication.html  
    > *Aporte Técnico al Taller:* Proporcionó el patrón de descomposición evolutiva para aislar progresivamente las capacidades de cuentas y cartera del Core Bancario monolítico on-premise hacia microservicios en Kubernetes, mitigando el riesgo operativo de una migración "Big Bang" (`INF-1`).

12. **Debezium Authors & Red Hat. (2023).** *Debezium: Change Data Capture for Event-Driven Architectures*. Debezium Documentation. URL: https://debezium.io/documentation/reference/stable/  
    > *Aporte Técnico al Taller:* Sustentó la arquitectura del pipeline CDC sobre los registros WAL de la base transaccional de Ban100, logrando propagar eventos a Apache Kafka en menos de 500 ms y erradicando el proceso batch nocturno de 12 horas (`INF-2`).

13. **Apache Software Foundation. (2023).** *Apache Kafka MirrorMaker 2.0: Multi-Cluster Replication and Cross-Region Disaster Recovery*. Kafka Documentation. URL: https://kafka.apache.org/documentation/#georeplication  
    > *Aporte Técnico al Taller:* Fundamentó la replicación síncrona/asimétrica activa-activa entre los clusters de Bogotá y Medellín, garantizando un RTO < 1 segundo y RPO = 0 para las transacciones inmediatas de Bre-B (`INF-4`).

14. **DAMA International. (2017).** *DAMA-DMBOK: Data Management Body of Knowledge (2nd Edition)*. Technics Publications. ISBN: 978-1634622349.  
    > *Aporte Técnico al Taller:* Guió el diseño de la gobernanza de datos maestros en el Master Data Management (MDM), la creación del "Golden Record" del cliente unificado y las reglas de enmascaramiento dinámico (DDM) para preservar la reserva bancaria.

---

_Este archivo hace parte integral de la entrega del Taller 8 del curso de Arquitectura Empresarial (AREM) — Universidad de La Sabana._
