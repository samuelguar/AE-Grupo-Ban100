# 📚 Referencias Bibliográficas del Taller

## Taller
_Taller 5 — Evaluación de Seguridad con STRIDE: Caso Ban100_

---

## Referencias Utilizadas

1. Shostack, A. *Threat Modeling: Designing for Security*. John Wiley & Sons, 2014. ISBN: 978-1-118-80999-0.
   > Obra fundamental sobre la metodología de modelado de amenazas, definición del marco STRIDE y aplicación sistemática sobre diagramas de flujo de datos (DFD) y límites de confianza.

2. Superintendencia Financiera de Colombia (SFC). *Circular Externa 008 de 2023: Instrucciones relativas a la administración del riesgo de ciberseguridad, autenticación robusta, gestión de incidentes y control interno*. Bogotá D.C., 2023.
   > Marco regulatorio vinculante para entidades vigiladas en Colombia. Establece requisitos de autenticación multifactor adaptativa, monitoreo transaccional continuo contra fraude y auditoría inmutable aplicados en el análisis STRIDE de Ban100.

3. Banco de la República de Colombia. *Reglamentación del Sistema de Pagos Inmediatos Interoperables (Bre-B) y Adopción del Estándar ISO 20022*. Circular Reglamentaria Externa DSP-2023. Bogotá D.C., 2023.
   > Especificación normativa y técnica del sistema de pagos inmediatos 24/7/365 en Colombia, que sustenta el análisis de amenazas de alteración (Tampering) en mensajería `pacs.008` y secuestro de "Llaves".

4. National Institute of Standards and Technology (NIST). *SP 800-207: Zero Trust Architecture*. NIST Special Publication, Agosto 2020. [Enlace](https://csrc.nist.gov/publications/detail/sp/800-207/final).
   > Estándar de referencia para el diseño de seguridad basada en el principio de "nunca confiar, siempre verificar", que fundamenta los controles de autenticación mTLS, re-evaluación en servidor y microsegmentación en Kubernetes.

5. Open Web Application Security Project (OWASP). *OWASP Top 10:2021 — The Ten Most Critical Web Application Security Risks*. OWASP Foundation, 2021. [Enlace](https://owasp.org/Top10/).
   > Clasificación estándar de vulnerabilidades web (A01: Broken Access Control, A02: Cryptographic Failures, A03: Injection, A07: Identification and Authentication Failures) mapeadas contra las amenazas STRIDE del canal digital y API Gateway.

6. Open Web Application Security Project (OWASP). *OWASP Application Security Verification Standard (ASVS) Version 4.0.3*. OWASP Foundation, 2021. [Enlace](https://owasp.org/www-project-application-security-verification-standard/).
   > Guía técnica de verificación de controles de seguridad para aplicaciones bancarias y de misión crítica (Nivel 3: Aplicaciones de alto riesgo financiero).

7. Congreso de la República de Colombia. *Ley 527 de 1999: Por medio de la cual se define y reglamenta el acceso y uso de los mensajes de datos, del comercio electrónico y de las firmas digitales, y se establecen las entidades de certificación*. Diario Oficial No. 43.673, Agosto 1999.
   > Fundamento jurídico colombiano para mitigar el no repudio (Repudiation) en pagarés desmaterializados y transacciones de originación digital de libranza.

8. Congreso de la República de Colombia. *Ley Estatutaria 1581 de 2012: Por la cual se dictan disposiciones generales para la protección de datos personales (Habeas Data)*. Diario Oficial No. 48.587, Octubre 2012.
   > Marco legal para la mitigación de divulgación no autorizada de información (Information Disclosure) sobre datos financieros, saldos y mesadas pensionales en Ban100.

9. International Organization for Standardization (ISO). *ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection — Information security management systems — Requirements*. Ginebra, Suiza, 2022.
   > Estándar internacional para la gestión de la seguridad de la información, gestión de riesgos y pistas de auditoría inmutables en entidades bancarias.

10. Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC). *Marco de Referencia de Arquitectura Empresarial (MRAE v3.0) — Dominio de Seguridad*. Bogotá D.C., Colombia, 2023.
    > Estándar gubernamental colombiano que alinea la gestión de ciberseguridad, privacidad por diseño y continuidad operativa dentro del ciclo de Arquitectura Empresarial.

---

## Recomendaciones

- Se utilizó formato IEEE / APA para la referenciación de normas técnicas y artículos de seguridad.
- Las fuentes normativas de la Superintendencia Financiera de Colombia y del Banco de la República corresponden a circulares emitidas durante 2023 de obligatorio cumplimiento para el sistema bancario.
- Fuente asistida por IA: Google Gemini (Antigravity), septiembre 2026, utilizada como apoyo analítico para la estructuración metodológica del informe técnico y la formulación del modelo STRIDE.

---

_Este archivo forma parte de la entrega académica del curso AREM - Universidad de La Sabana._
