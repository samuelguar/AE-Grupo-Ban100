# Arquitectura Empresarial — Ban100 S.A. (Bancien S.A.)

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · Santiago Barrera Rueda, Krish Purmessur Moros, Samuel Guerrero Arcos
**Curso:** Arquitectura Empresarial — Universidad de La Sabana (Prof. Ing. César Augusto Vega Fernández)

---

## 📌 En una frase

Rediseñamos cómo Ban100 conecta a sus pensionados, sus canales digitales y las pagadurías públicas, para que un crédito de libranza pase de **3–5 días a menos de 15 minutos**, sin importar qué tan avanzada esté la tecnología de cada pagaduría, y con los datos y la identidad de los clientes protegidos.

## 🩺 El problema

Ban100 atiende a **202.235 clientes de crédito**, el 85 % en estratos 1, 2 y 3, y llega a más de 1.000 municipios con solo 10 oficinas. El **94 % de lo que presta es libranza** y el **98,3 % de esa libranza se coloca entre pensionados y empleados de gobierno**, así que el banco depende de que cada pagaduría confirme el cupo de descuento. En unos 850 a 880 municipios esas pagadurías aún tienen sistemas poco modernizados, lo que retrasa la aprobación. Además, el banco debe probar la identidad y el consentimiento de clientes que contratan sin ir a una oficina, y cumplir las exigencias de la Superintendencia Financiera y de protección de datos.

## 💡 Lo que proponemos

- **Dos velocidades para conectar con las pagadurías:** una conexión directa y estándar con las entidades más avanzadas, y un canal asíncrono con portal de autogestión para las demás, de modo que ninguna frene al resto.
- **Un servicio que no se detenga cuando el sistema central está en mantenimiento:** separar la originación del sistema central con sincronización casi inmediata y recuperación automática.
- **Un asistente digital seguro:** que atienda por WhatsApp y app, consulte cupos y simule créditos, proteja los datos personales y pase a una persona las decisiones importantes.
- **Cumplimiento verificable:** autogestión de la revocatoria de datos, borde preparado para IPv6 y un repositorio de arquitectura con indicadores.
- **Un plan en cuatro fases** (0–1 mes, 1–3 meses, 3–6 meses y 6–12 meses), empezando por lo más urgente y de menor costo.

## 🗺️ Cómo se implementa

Ver el **[Resumen Ejecutivo](resumen-ejecutivo.md)** — ahí está el detalle de beneficios esperados, fases de implementación y tiempos, en un solo documento pensado para el negocio, no para el equipo técnico.

## 📂 Si quiere ver el detalle técnico completo

Todo el análisis que sustenta esta propuesta está documentado carpeta por carpeta. Todos los diagramas son archivos `.drawio` que se abren en [app.diagrams.net](https://app.diagrams.net).

| Carpeta | Qué contiene |
|---|---|
| [`00-preliminary-vision/`](./00-vision-preliminar/) | Contexto del cliente (ficha), visión de la solución y mapa conceptual |
| [`01-bpmn/`](./01-bpmn/) | Cómo funciona el proceso de originación de libranza y su visación con pagadurías |
| [`02-modelo-informacion/`](./02-modelo-informacion/) | Qué información maneja el negocio y cómo fluye (modelo de datos y contexto) |
| [`03-arquitectura-c4/`](./03-arquitectura-c4/) | Los sistemas actuales y cómo están construidos |
| [`04-infraestructura/`](./04-infraestructura/) | Dónde corre todo hoy, qué riesgos técnicos tiene y cómo se estima el plazo de las pagadurías |
| [`05-seguridad-stride/`](./05-seguridad-stride/) | Análisis de seguridad del flujo de libranza (8 amenazas priorizadas) |
| [`06-normatividad/`](./06-normatividad/) | Cumplimiento legal y normativo (15 criterios, 6 brechas) |
| [`07-opportunities-solutions/`](./07-oportunidades-soluciones/) | La solución propuesta y las brechas que cierra |
| [`08-integracion-vistas/`](./08-integracion-vistas/) | Cómo se conecta todo lo anterior en una sola arquitectura (0 elementos huérfanos) |

## Contacto

- **Santiago Barrera Rueda** — `santiagobarru@unisabana.edu.co`
- **Krish Purmessur Moros** — `krishpumo@unisabana.edu.co`
- **Samuel Guerrero Arcos** — `samuelguar@unisabana.edu.co`

*Facultad de Ingeniería — Universidad de La Sabana*

---

## 📄 Licencia

Este repositorio es de uso académico bajo licencia MIT. Desarrollado para el curso de Arquitectura Empresarial — Universidad de La Sabana (2026).
