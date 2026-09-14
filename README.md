# Arquitectura Empresarial — Ban100

**Cliente:** Ban100 (Establecimiento Bancario Comercial, antes Credifinanciera S.A.)  
**Equipo:** Santiago Barrera Rueda · Krish Purmessur Moros · Samuel Guerrero Arcos  
**Curso:** Arquitectura Empresarial (AREM) — Universidad de La Sabana  

---

## 📌 En una frase

Transformamos la plataforma de servicios financieros de Ban100 para que la solicitud y desembolso de créditos de libranza pase de 3 a 5 días a menos de 15 minutos, habilitamos pagos inmediatos 24/7 con el ecosistema Bre-B sin caídas de servicio, y blindamos los datos y la identidad de más de 250.000 clientes pensionados y microempresarios.

---

## 🩺 El problema

Hoy Ban100 atiende a más de 250.000 clientes en 900 municipios de Colombia, pero enfrenta cuatro barreras operativas críticas:
1. **Trámites lentos en libranzas:** La originación de créditos depende de validaciones manuales y papeleo con convenios de pagadurías, tardando entre 3 y 5 días hábiles en desembolsar.
2. **Información fragmentada:** Los datos de los clientes viven en silos separados por producto (crédito, cuentas, CDTs), sin una visión unificada 360° en tiempo real.
3. **Sistemas rígidos que frenan la innovación:** El sistema bancario transaccional principal exige procesos por lotes nocturnos (con 12 horas de desfase en saldos), lo que choca con la inmediatez que exige el nuevo sistema de pagos 24/7 Bre-B del Banco de la República.
4. **Riesgos de seguridad y exigencias normativas:** La dispersión tecnológica y el perfil vulnerable de los clientes (adultos mayores pensionados) exigen reforzar los controles contra suplantaciones de identidad y asegurar el cumplimiento de las circulares de ciberseguridad de la Superintendencia Financiera de Colombia y de protección de datos de la SIC.

---

## 💡 Lo que proponemos

Una arquitectura empresarial moderna, ágil y segura enfocada en el crecimiento del negocio:

- **Originación de libranzas 100% digital en minutos:** Integrar biometría facial pasiva y firma electrónica legalmente válida para que un pensionado solicite y reciba su crédito en menos de 15 minutos desde su celular o WhatsApp, sin pisar una oficina.
- **Pagos inmediatos 24/7/365 sin interrupciones:** Conectar a Ban100 con el riel nacional Bre-B mediante una infraestructura en nube de alta disponibilidad (Bogotá–Medellín), garantizando transferencias en menos de 3 segundos con disponibilidad del 99.99%.
- **Saldos y visión del cliente en tiempo real:** Eliminar los lotes nocturnos mediante sincronización continua de datos, permitiendo consultar saldos y movimientos al instante en cualquier canal.
- **Blindaje integral de identidad y datos personales:** Implementar autenticación reforzada contra fraudes y suplantaciones digitales, enmascaramiento de información sensible de mesadas pensionales y un módulo de autoservicio para que los clientes gestionen sus derechos de privacidad.
- **Hoja de ruta gradual y de bajo riesgo:** Un plan de modernización en 3 horizontes (inmediato, mediano y largo plazo) que transforma la tecnología por etapas, asegurando continuidad operativa sin traumatismos para los clientes actuales.

---

## 🗺️ Cómo se implementa

Para conocer los beneficios cuantitativos, las fases de ejecución en tres horizontes (H1 Quick Wins, H2 Ciberseguridad y Datos, H3 Modernización del Core) y los tiempos estimados, consulte el **[Resumen Ejecutivo](resumen-ejecutivo.md)**, diseñado especialmente para la alta dirección y los líderes de negocio.

---

## 📂 Si quiere ver el detalle técnico completo

Todo el análisis, modelos visuales y diagnósticos que sustentan esta propuesta están documentados taller por taller, siguiendo los estándares internacionales de arquitectura (MRAE v3.0 MinTIC, TOGAF ADM, C4 Model y STRIDE):

| Carpeta | Qué contiene | Estado |
|---|---|:---:|
| [`00-preliminary-vision/`](./00-preliminary-vision/) | Ficha de caracterización institucional, dolores de negocio y visión estratégica | **Completo** |
| [`01-bpmn/`](./01-bpmn/) | Modelado BPMN 2.0 del proceso misional de originación y desembolso digital de libranza | **Completo** |
| [`02-modelo-informacion/`](./02-modelo-informacion/) | Estructura de datos (ERD), catálogo de llaves Bre-B y diagrama de contexto organizacional | **Completo** |
| [`03-arquitectura-c4/`](./03-arquitectura-c4/) | Arquitectura de sistemas en modelo C4 (Contexto C1 y Contenedores C2 con 19 componentes) | **Completo** |
| [`04-infraestructura/`](./04-infraestructura/) | Mapa de infraestructura en nube híbrida multi-región y diagnóstico de 5 riesgos técnicos | **Completo** |
| [`05-seguridad-stride/`](./05-seguridad-stride/) | Análisis de amenazas de ciberseguridad STRIDE y diseño de arquitectura Zero Trust | **Completo** |
| [`06-normatividad/`](./06-normatividad/) | Diagnóstico de cumplimiento legal (Circular 008 SFC, Ley 1581 Habeas Data, ISO 27001) | **Completo** |
| [`07-opportunities-solutions/`](./07-opportunities-solutions/) | Arquitectura objetivo (TO-BE), matriz de 20 brechas y hoja de ruta en 3 horizontes | **Completo** |
| [`08-integracion-vistas/`](./08-integracion-vistas/) | Tablero integrado multicapa (5 capas conectadas de punta a punta con 0 huérfanos) | **Completo** |
| [`09-presentacion-final/`](./09-presentacion-final/) | Presentación ejecutiva, paquetes de trabajo, gobernanza y sustentación final | ⏳ *Pendiente* |

---

## 👥 Contacto del Equipo

Para dudas o consultas sobre esta propuesta de Arquitectura Empresarial:

- **Santiago Barrera Rueda** — `santiagobarrue@unisabana.edu.co`
- **Krish Purmessur Moros** — `krishpumo@unisabana.edu.co`
- **Samuel Guerrero Arcos** — `samuelguar@unisabana.edu.co`

*Facultad de Ingeniería — Universidad de La Sabana*

---

## 📄 Licencia

Este repositorio es de uso académico bajo licencia MIT. Desarrollado para el curso de Arquitectura Empresarial (AREM) — Universidad de La Sabana (2026).
