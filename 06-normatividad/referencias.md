# 📚 Referencias Bibliográficas del Taller

## Taller
_Taller 6 — Checklist de Cumplimiento Normativo: Caso Ban100_  
*Dominio de Seguridad y Cumplimiento del MAE (MRAE v3.0 MinTIC): Auditoría Legal, Habeas Data, Ciberseguridad Financiera y Estándares de Interoperabilidad*

---

## Referencias Utilizadas

1. **Superintendencia Financiera de Colombia (SFC).** *Circular Externa 008 de 2023: Instrucciones relativas a la administración del riesgo de ciberseguridad, autenticación robusta multifactor, gestión de incidentes y control interno*. Bogotá D.C., 2023. [Enlace oficial](https://www.superfinanciera.gov.co). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Constituye el marco regulatorio vinculante principal para Ban100 como establecimiento bancario comercial. Establece los estándares mandatorios para la implementación de mecanismos de autenticación multifactor (MFA) adaptativa/contextual en canales móviles, la obligación de disponer de pistas de auditoría forense inmutables (WORM con sincronización horaria NTP), el monitoreo continuo 24/7/365 contra fraudes transaccionales y la resiliencia operativa en planes de recuperación ante desastres (DRP). Aplicada directamente en los controles 5, 7, 8, 9, 17 y 19 del checklist.

2. **Congreso de la República de Colombia.** *Ley Estatutaria 1581 de 2012: Por la cual se dictan disposiciones generales para la protección de datos personales (Habeas Data)*. Diario Oficial No. 48.587, 18 de octubre de 2012. [Enlace oficial](http://www.secretariasenado.gov.co/senado/basedoc/ley_1581_2012.html). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Régimen general de protección de datos personales en Colombia. Fundamenta la obligatoriedad de recabar el consentimiento previo, expreso e informado de los más de 250.000 clientes, el tratamiento reforzado de datos biométricos sensibles (Art. 6) capturados en el flujo de validación facial con Truora, la garantía efectiva de los derechos ARCO y el Registro Nacional de Bases de Datos (RNBD) administrado por la SIC. Aplicada en los controles 1, 2, 4, 13, 14 y 21.

3. **Congreso de la República de Colombia.** *Ley Estatutaria 1266 de 2008: Por la cual se dictan las disposiciones generales del hábeas data y se regula el manejo de la información contenida en bases de datos personales, en especial la financiera, crediticia, comercial, de servicios y la proveniente de terceros países*. Diario Oficial No. 47.219, 31 de diciembre de 2008. [Enlace oficial](http://www.secretariasenado.gov.co/senado/basedoc/ley_1266_2008.html). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Regulación especial para la información crediticia y financiera procesada por Ban100. Gobierna la autorización expresa requerida para la consulta del historial crediticio del solicitante de libranza y microcrédito ante operadores como TransUnion y Datacrédito/Experian, así como los términos máximos de caducidad del dato negativo de mora. Aplicada en el control 3 del checklist.

4. **Congreso de la República de Colombia.** *Ley 527 de 1999: Por medio de la cual se define y reglamenta el acceso y uso de los mensajes de datos, del comercio electrónico y de las firmas digitales, y se establecen las entidades de certificación*. Diario Oficial No. 43.673, 23 de agosto de 1999. [Enlace oficial](http://www.secretariasenado.gov.co/senado/basedoc/ley_0527_1999.html). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Otorga pleno valor probatorio, ejecutivo y legal a los pagarés desmaterializados originados 100% digitalmente en la colocación de libranzas. Exige el uso de firmas electrónicas certificadas, sellado cronológico acreditado (*Time-stamping*) y garantiza la equivalencia funcional del documento digital custodiado en DECEVAL frente al pagaré tradicional en papel físico. Aplicada en los controles 12 y 20.

5. **Presidencia de la República de Colombia.** *Decreto 1377 de 2013: Por el cual se reglamenta parcialmente la Ley 1581 de 2012*. Diario Oficial No. 48.834, 27 de junio de 2013. [Enlace oficial](http://www.suin-juriscol.gov.co/viewDocument.asp?ruta=Decretos/1414445). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Reglamenta las políticas de tratamiento de información, el contenido mínimo del aviso de privacidad y las condiciones para la recolección de datos personales en canales electrónicos. Sustenta los criterios de evaluación del consentimiento en el onboarding web y móvil de Ban100.

6. **Presidencia de la República de Colombia.** *Decreto 2364 de 2012: Por medio del cual se reglamenta el artículo 7° de la Ley 527 de 1999, sobre firma electrónica y se dictan otras disposiciones*. Diario Oficial No. 48.622, 22 de noviembre de 2012. [Enlace oficial](http://www.suin-juriscol.gov.co/viewDocument.asp?ruta=Decretos/1514781). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Establece los requisitos de confiabilidad y atributos técnicos que debe cumplir la firma electrónica para garantizar la identificación del firmante y la integridad inalterable del título de deuda crediticia.

7. **Banco de la República de Colombia.** *Circular Reglamentaria Externa DSP-2023: Reglamentación de los Sistemas de Pago de Bajo Valor Inmediatos e Interoperables (Sistema Bre-B)*. Bogotá D.C., 2023. [Enlace oficial](https://www.banrep.gov.co). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Marco mandatorio para la liquidación bruta en tiempo real (LBTR) de pagos de bajo valor 24/7/365 en Colombia. Exige la adopción estricta del estándar internacional ISO 20022 (`pacs.008`, `pacs.002`, `pain.001`), la interconexión mediante canales VPN IPsec dedicados con mTLS y la custodia del catálogo de llaves bancarias. Aplicada directamente en los controles 8 y 22.

8. **International Organization for Standardization (ISO) / International Electrotechnical Commission (IEC).** *ISO/IEC 27001:2022: Information security, cybersecurity and privacy protection — Information security management systems — Requirements*. Ginebra, Suiza, 2022. [Enlace oficial](https://www.iso.org/standard/27001). Fecha de consulta: 12/09/2026.
   > **Anotación técnica:** Estándar internacional rector del Sistema de Gestión de Seguridad de la Información (SGSI) adoptado por Ban100. Fundamenta los controles de seguridad criptográfica (A.8.24), gestión de accesos privilegiados (A.5.15 a A.5.18), prevención de fugas de datos - DLP (A.8.12), enmascaramiento dinámico (A.8.11) y continuidad operativa. Aplicada en los controles 5, 6, 7, 8 y 16.

9. **Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC).** *Marco de Referencia de Arquitectura Empresarial para el Estado Colombiano (MRAE v3.0)*. Dirección de Gobierno Digital, Bogotá D.C., Mayo de 2023.
   > **Anotación técnica:** Marco metodológico nacional que estructura los 5 dominios de Arquitectura Empresarial (Institucional, Información, Sistemas de Información, Tecnología y Seguridad). En particular, se incorporó el principio `PRI_08` (*Seguridad y Privacidad Digital desde el Diseño*) y los lineamientos del Modelo de Gestión y Gobierno de TI (MGGTI) para asegurar que el diagnóstico normativo trascienda la evaluación puntual y se integre a la gobernanza corporativa de TI de Ban100.

10. **Superintendencia Financiera de Colombia (SFC).** *Circular Básica Jurídica (Circular Externa 029 de 2014) — Parte I, Título V: Reglas relativas a la gestión del riesgo operativo, seguridad de la información y calidad en la prestación de servicios financieros a través de canales no tradicionales*. Bogotá D.C., 2014. [Enlace oficial](https://www.superfinanciera.gov.co). Fecha de consulta: 12/09/2026.
    > **Anotación técnica:** Disposiciones que regulan la operación de la banca móvil, portales de internet y canales asistidos, exigiendo cifrado robusto de extremo a extremo, prevención de ataques de intermediario (*Man-in-the-Middle*) y alta disponibilidad en los convenios con pagadurías e instituciones pagadoras de pensiones.

11. **Superintendencia Financiera de Colombia (SFC).** *Circular Externa 027 de 2020: Modificación Integral al Sistema de Administración del Riesgo de Lavado de Activos y Financiación del Terrorismo (SARLAFT 4.0)*. Bogotá D.C., 2020.
    > **Anotación técnica:** Marco de debida diligencia intensificada que impone el conocimiento digital del cliente y la verificación biométrica no presencial obligatoria durante la apertura remota de cuentas de depósito y vinculación crediticia. Sustenta el control 10 del checklist.

12. **National Institute of Standards and Technology (NIST).** *Special Publication 800-207: Zero Trust Architecture*. Computer Security Division, Information Technology Laboratory, Gaithersburg, MD, 2020. [Enlace](https://doi.org/10.6028/NIST.SP.800-207). Fecha de consulta: 12/09/2026.
    > **Anotación técnica:** Marco de arquitectura de seguridad que orienta el principio "nunca confiar, siempre verificar" implementado en la capa de microservicios de Ban100 (mTLS obligatorio inter-servicios, tokens JWT asimétricos RS256 y backend-authoritative), sustentando los controles 6 y 11 del checklist.

13. **FIDO Alliance.** *Biometric Certification Program Requirements — Presentation Attack Detection (PAD) Level 2 (iBeta / ISO 30107-3)*. Beaverton, OR, 2021. [Enlace oficial](https://fidoalliance.org). Fecha de consulta: 12/09/2026.
    > **Anotación técnica:** Estándar internacional para la certificación de resistencia de motores biométricos ante ataques de presentación (máscaras de silicona, fotografías de alta resolución, videos inyectados y deepfakes). Sustenta la justificación técnica de cumplimiento del control 10 en la alianza tecnológica con Truora.

14. **OWASP Foundation.** *OWASP Top 10:2021 — The Ten Most Critical Web Application Security Risks*. 2021. [Enlace](https://owasp.org/Top10/). Fecha de consulta: 12/09/2026.
    > **Anotación técnica:** Guía rectora para la prevención de fallas como Inyección (A03), Exposición de Datos Sensibles (A02), Insecure Direct Object References - IDOR (A01) y Falla en la Configuración de Seguridad - Cabeceras CSP (A05). Utilizada para respaldar los controles 15 y 18 del checklist.

---

## Recomendaciones de Consulta y Aplicación

- Las citas a leyes y decretos corresponden a las versiones oficiales vigentes compiladas en el Sistema Único de Información Normativa (SUIN-Juriscol) del Ministerio de Justicia y del Derecho.
- Las directrices de la Superintendencia Financiera de Colombia (SFC) y de la Superintendencia de Industria y Comercio (SIC) fueron contrastadas con sus respectivas circulares externas y doctrinas unificadas a corte de septiembre de 2026.
- Cada referencia bibliográfica cuenta con su correspondiente párrafo de justificación y anotación técnica, demostrando su trazabilidad directa con los controles evaluados en la arquitectura de Ban100.

---

_Este archivo forma parte integral de la entrega académica del Taller 6 en el curso de Arquitectura Empresarial (AREM) — Universidad de La Sabana._
