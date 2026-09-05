# 📚 Referencias Bibliográficas del Taller

## 🔖 Taller
_Taller 4 - Mapa de Infraestructura y Diagnóstico Técnico: Caso Ban100_

---

## 📚 Referencias Utilizadas

1. Fowler, M. *Strangler Fig Application*. martinfowler.com, 2004. [Enlace](https://martinfowler.com/bliki/StranglerFigApplication.html). Fecha de consulta: 05/09/2026.
   > Referencia fundamental sobre el patrón de migración incremental de sistemas monolíticos a microservicios, aplicado al Core Bancario Legacy de Ban100.

2. Microsoft Azure. *Multi-region deployment for high availability*. Azure Architecture Center, 2024. [Enlace](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/app-service-web-app/multi-region). Fecha de consulta: 05/09/2026.
   > Arquitectura de referencia para despliegues multi-región activo-activo con failover automático, aplicada a la estrategia de Nube Híbrida Multi-Región de Ban100.

3. National Institute of Standards and Technology (NIST). *SP 800-207: Zero Trust Architecture*. NIST Special Publication, 2020. [Enlace](https://csrc.nist.gov/publications/detail/sp/800-207/final). Fecha de consulta: 05/09/2026.
   > Marco de referencia para la implementación del modelo de seguridad Zero Trust ("nunca confiar, siempre verificar") adoptado en el Dominio de Seguridad de Ban100.

4. Superintendencia Financiera de Colombia (SFC). *Circular Externa 008 de 2023: Instrucciones relativas a la administración del riesgo de ciberseguridad, autenticación robusta, gestión de incidentes y control interno*. Bogotá D.C., 2023.
   > Normativa obligatoria que establece los controles de seguridad informática, autenticación multifactor reforzada y supervisión de pasarelas de pago que determinan los requerimientos del SOC y la capa de ciberseguridad del mapa.

5. Banco de la República de Colombia. *Reglamentación del Sistema de Pagos Inmediatos Interoperables (Bre-B) y Adopción del Estándar ISO 20022*. Circular Reglamentaria Externa DSP-2023. Bogotá D.C., 2023.
   > Marco normativo y operativo del sistema de pagos inmediatos que obliga a Ban100 a conectarse a la infraestructura central para procesar transferencias en tiempo real las 24 horas, determinando los requerimientos de disponibilidad 99.99% y latencia < 3 segundos del módulo Bre-B.

6. Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC). *Marco de Referencia de Arquitectura Empresarial (MRAE v3.0) — Dominio Tecnológico: Infraestructura y Servicios*. Bogotá D.C., 2023.
   > Modelo conceptual gubernamental colombiano que organiza las capacidades de infraestructura tecnológica en el contexto de la Arquitectura Empresarial. Aplicado como marco estructurador de las 7 zonas del mapa de Ban100.

7. Burns, B., Beda, J. & Hightower, K. *Kubernetes: Up and Running*. O'Reilly Media, 3ra edición, 2022.
   > Referencia técnica para la orquestación de contenedores y el auto-escalado horizontal (HPA) utilizado en los clusters Kubernetes de las regiones principal y de contingencia de Ban100.

8. Confluent. *Kafka MirrorMaker 2.0 and Cross-Cluster Replication*. Confluent Documentation, 2024. [Enlace](https://docs.confluent.io/platform/current/multi-dc-deployments/). Fecha de consulta: 05/09/2026.
   > Documentación técnica sobre replicación geo-distribuida de Event Streaming con Kafka, aplicada a la sincronización del estado del Directorio de Llaves Bre-B entre la región principal y la de contingencia.

9. Amazon Web Services (AWS). *Best Practices for Building Resilient Financial Services Applications on AWS*. AWS Whitepaper, 2023. [Enlace](https://docs.aws.amazon.com/whitepapers/latest/financial-services-resilience/). Fecha de consulta: 05/09/2026.
   > Guía de buenas prácticas para la construcción de aplicaciones financieras resilientes en la nube, incluyendo patrones de alta disponibilidad, recuperación ante desastres y cumplimiento normativo.

10. Richardson, C. *Microservices Patterns: With examples in Java*. Manning Publications, 2019.
    > Referencia sobre patrones de diseño de microservicios (API Gateway, Event Sourcing, CQRS, Saga) aplicados en la descomposición del Core Bancario y la arquitectura de integración de Ban100.

---

## 📌 Recomendaciones

- Se utilizó formato IEEE para las citas bibliográficas.
- Las fuentes normativas colombianas (SFC y Banco de la República) se referenciaron directamente desde las circulares oficiales.
- Fuente asistida por IA: Google Gemini (Antigravity / Claude Opus), septiembre 2026, utilizada para la estructuración del informe técnico y la generación del mapa de infraestructura en Draw.io.

---

_Este archivo forma parte de la entrega académica del curso AREM - Universidad de La Sabana._

