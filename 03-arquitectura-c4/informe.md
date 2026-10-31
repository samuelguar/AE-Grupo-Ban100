# 📄 Informe Técnico del Taller

## Nombre del Taller
_Taller 3 - Arquitectura C4: Contexto (C1) y Contenedores (C2) de la Plataforma Digital de Libranza y Banca Inclusiva Ban100_

## Integrantes del equipo
- Santiago Barrera Rueda
- Krish Purmessur Moros
- Samuel Guerrero Arcos

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A.

## Descripción general del trabajo
Se documentó la arquitectura de aplicaciones **AS-IS** con el modelo C4: el **C1** muestra la plataforma como una única caja con sus actores y sistemas externos, y el **C2** descompone esa caja en ocho contenedores propios, más la infraestructura de soporte, con la tecnología de cada contenedor y el protocolo de cada integración.

## Proceso de desarrollo
1. **C1.** Tres personas (*Analista de Operaciones y Pagadurías*, *Pensionado / Empleado Público*, *Microempresario / Ahorrador CDT*); sistema en alcance `#08427b` como **caja única** sin contenedores internos; cinco sistemas externos en gris `#8a8a8a`: Pagadurías Públicas Nacionales y Territoriales, Truora, Centrales de Riesgo TransUnion/DataCrédito, SFC / RNVE-SIMEV y Bre-B.
2. **C2.** Se descompuso la caja en contenedores `#438dd5` con tecnología entre corchetes, se agregó la infraestructura de soporte `#6b6b6b` (Balanceador y WAF, bases de datos) y se mantuvieron los actores y externos del C1.
3. **Protocolos.** Cada flecha indica `HTTPS/JSON REST`, `SOAP/XML`, `SFTP/Batch` o `JDBC/TLS`; las integraciones con terceros se dibujan punteadas.

## Análisis del modelo propuesto
### Contenedores del C2
| Contenedor | Tecnología | Responsabilidad |
|---|---|---|
| Sucursal Virtual Responsive | SPA Web HTTPS | Consulta y gestión para clientes y analistas |
| App Móvil Ban100 | iOS / Android | Solicitud de libranza y servicios |
| Ban-I Bot Libranza | Asistente Conversacional Omnicanal | Atención y simulación por WhatsApp |
| API Gateway | Kong / Reverse Proxy TLS 1.3 | Punto único de entrada y enrutamiento |
| μS Originación y Scoring | Microservicio en Kubernetes | Orquesta validación, scoring y visación |
| Módulo de Pagos en Línea y Actualización de Datos | Servicio Web | Pagos y actualización de datos del cliente |
| Cliente 360 MDM | Repositorio Maestro de Datos | Dato maestro del cliente |
| Core Bancario Transaccional | Sistema Central On-Premise | Cartera, desembolso y contabilidad |

### Protocolos principales
| Origen → Destino | Protocolo |
|---|---|
| Canales → Balanceador y WAF → API Gateway | `HTTPS/JSON REST` |
| API Gateway → μS Originación / Módulo de Pagos | `HTTPS/JSON REST` |
| μS Originación → Cliente 360 MDM / Módulo de Pagos → MDM | `JDBC/TLS` |
| μS Originación → Core Bancario | `SOAP/XML` (síncrono) |
| μS Originación → Pagadurías | `SFTP/Batch` |
| μS Originación → Truora | `HTTPS/JSON REST` |
| μS Originación → Centrales de Riesgo | `SOAP/XML` |
| Core → SFC / RNVE-SIMEV | `SFTP/Batch` |
| Core → Bre-B | `HTTPS/JSON REST` |

### Diferencias con el caso base y decisiones
- **Frente al caso base (RedExpress):** el sistema de Ban100 tiene dos externos críticos que no existen en el caso base — las pagadurías públicas (contraparte B2G con madurez desigual) y el regulador (SFC / RNVE-SIMEV).
- **Decisión 1.** El Core permanece como contenedor On-Premise con acoplamiento síncrono desde μS Originación; se documenta como debilidad AS-IS (se resuelve en el Taller 7).
- **Decisión 2.** La integración con pagadurías se dibuja como un único flujo `SFTP/Batch` porque hoy no existe un adaptador por tipo de pagaduría.
- **Supuestos.** Los protocolos y la tecnología de infraestructura (motor relacional, Kong) provienen de la arquitectura documentada del equipo y de la línea base ArchiMate; no se probaron de forma activa.

## Diagrama final entregado
- [Ver C1 en draw.io](./c1-contexto-final.drawio)
- [Ver C2 en draw.io](./c2-contenedores-final.drawio)

## Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Plataforma Digital de Libranza y Banca Inclusiva Ban100 | Sistema en alcance | Caja única del C1 | Gerencia Digital |
| Analista de Operaciones y Pagadurías | Persona | Concilia convenios y descuentos de nómina | Operaciones |
| Pensionado / Empleado Público | Persona | Solicita libranza | Cliente |
| Microempresario / Ahorrador CDT | Persona | Solicita microcrédito y abre CDT | Cliente |
| Balanceador y WAF | Infraestructura | Cluster HA Activo-Pasivo en el borde | Infraestructura |
| Base de Datos MDM / Base de Datos del Core | Infraestructura | Motores relacionales | Datos / TI |
| Truora, Centrales de Riesgo, Pagadurías, SFC / RNVE-SIMEV, Bre-B | Sistema externo | Terceros con borde punteado | Contratos |

## Investigación complementaria
### Tema investigado:
Modelo C4 de Simon Brown y patrones de migración desde un Core monolítico (Strangler Fig).

### Resumen:
El modelo C4 propone cuatro niveles de abstracción; el equipo aplicó C1 y C2 y reservó C3/C4 para etapas posteriores. La literatura de microservicios (Richardson, 2018) y el patrón Strangler Fig recomiendan encapsular el Core con una fachada de eventos antes de modificarlo, idea que sustenta el desacoplamiento del Taller 7.

Homologación MRAE v3.0: `MAE.LI.ASI.01` (arquitecturas de referencia: C4 como notación), `ASI.02` (arquitecturas de solución, 0,98 %: el C2) y `ASI.03` (catálogo de sistemas de información: tabla de contenedores). En MGGTI: `SI.01` (metodología de software), `SI.04` (tres ambientes desarrollo/pruebas/producción), `SI.06` (CI/CD y DevOps), `SI.10` (mantenimiento con terceros bajo ANS y penalidades) y `SI.14` (Arquitectura de Software, nuevo en v3.0). `PRI_07` (interoperabilidad) y `PRI_10` (neutralidad tecnológica) orientan la elección de protocolos abiertos.

### Vista ArchiMate equivalente
Contenedor C2 = Application Component; integración = Application Service / Flow; externo = Application Service (externo) con borde punteado.

## Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 3 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
