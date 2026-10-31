# 📄 Informe Técnico del Taller

## Nombre del Taller
_Taller 1 - BPMN: Originación de Crédito de Libranza 100 % Digital y Visación B2G con Pagadurías_

## Integrantes del equipo
- Santiago Barrera Rueda
- Krish Purmessur Moros
- Samuel Guerrero Arcos

**Equipo:** Ban100 — Grupo de Arquitectura Empresarial · **Cliente:** Ban100 S.A.

## Descripción general del trabajo
Se modeló en BPMN 2.0 el proceso misional de Ban100: la **originación de crédito de libranza 100 % digital** y su **visación con pagadurías públicas**. El 94 % de la colocación de Ban100 es libranza y el 98,3 % de ese segmento se coloca entre pensionados y empleados de gobierno; por eso el proceso incluye de forma explícita el carril de la pagaduría y la bifurcación entre integración estandarizada (Grupos MRAE 1–2) y vía asíncrona (Grupos 3–5). La meta del negocio es reducir el ciclo de **3–5 días a menos de 15 minutos**.

## Proceso de desarrollo
Se siguieron los cinco pasos de la guía del taller:

1. **Actores y carriles.** Cuatro carriles (`swimlane`): *Pensionado / Empleado Público (Estratos 1-3)*; *Canales Digitales Ban100 (Sucursal Virtual / App / Ban-I Bot)*; *Motor de Originación, Scoring y Biometría (μS + Truora + Core)*; *Pagaduría Pública (Nacional G1-G2 / Territorial G1-G5)*.
2. **Evento de inicio y eventos de fin.** Exactamente un inicio (*Solicita crédito de libranza*, verde `#d5e8d4`) y tres fines (rojo `#f8cecc`, borde grueso): *Crédito desembolsado y libranza radicada*, *Solicitud rechazada por identidad/riesgo* y *Solicitud desistida / sin cupo en pagaduría*.
3. **Actividades en verbo de acción.** Doce tareas (recibir, autorizar, validar, calcular, consultar, visar, consolidar, presentar, firmar, desembolsar, registrar, notificar).
4. **Gateways con pregunta explícita.** Tres compuertas exclusivas (naranja `#ffe6cc`) con salidas `Sí`/`No` o con la condición nombrada.
5. **Conexión y validación.** Cada flujo de secuencia lleva etiqueta con el dato o hito que transporta; no hay elementos flotantes y el diagrama se lee de izquierda a derecha.

Las decisiones de modelado se validaron contra la Ficha del Taller 0 (síntoma: *retraso de 3 a 5 días en la validación de cupos y la visación de libranzas con pagadurías territoriales de baja madurez digital*).

## Análisis del modelo propuesto
- **Estructura.** El hilo principal recorre los cuatro carriles: solicitud del cliente → simulación en el canal → consentimiento y biometría → validación con Truora y SARLAFT → scoring y Cliente 360 → visación en pagaduría → oferta y firma electrónica → desembolso, radicación y descuento de nómina/mesada.
- **Cómo representa las necesidades del cliente.** La compuerta *¿Pagaduría tiene interoperabilidad API/X-Road (G1-G2) o requiere vía asíncrona (G3-G5)?* convierte la asimetría tecnológica de 850–880 municipios en una decisión explícita del proceso, que es el origen de la propuesta de integración de dos velocidades del Taller 7.
- **Supuestos.** (a) La validación biométrica y la firma se ejecutan con Truora; (b) la consulta de listas SARLAFT ocurre antes del scoring; (c) los grupos MRAE de cada pagaduría se conocen por convenio (`grupo_mrae_t1_t5` en el ERD); (d) ambas vías de visación convergen en la consolidación del cupo.

## Diagrama final entregado
[Ver diagrama en draw.io](./modelo-final.drawio)

## Tabla de actores, entidades o componentes

| Nombre del elemento | Tipo | Descripción | Responsable |
|---|---|---|---|
| Pensionado / Empleado Público (Estratos 1-3) | Actor (carril) | Solicita el crédito, autoriza datos, captura biometría y firma el pagaré | Cliente |
| Canales Digitales Ban100 | Actor (carril) | Sucursal Virtual, App móvil y Ban-I Bot: recibe, simula y presenta la oferta | Gerencia Digital |
| Motor de Originación, Scoring y Biometría | Actor (carril) | μS Originación y Scoring, Truora y Core: valida, calcula, consolida y desembolsa | TI / Riesgos |
| Pagaduría Pública | Actor (carril) | Visa el cupo de descuento y registra el descuento en nómina o mesada | Entidad pública |
| Solicita crédito de libranza | Evento de inicio | Disparador del proceso | Cliente |
| ¿Supera validación biométrica facial y listas SARLAFT? | Gateway exclusivo | Decide continuar o rechazar por identidad/riesgo | Cumplimiento |
| ¿Pagaduría tiene interoperabilidad API/X-Road (G1-G2) o requiere vía asíncrona (G3-G5)? | Gateway exclusivo | Selecciona la vía de visación | Convenios B2G |
| ¿Cupo de descuento nómina/mesada aprobado y pagaré firmado digitalmente? | Gateway exclusivo | Decide desembolso o desistimiento | Operaciones |
| Crédito desembolsado y libranza radicada | Evento de fin | Éxito del proceso | Operaciones |
| Solicitud rechazada por identidad/riesgo | Evento de fin | Rechazo por biometría, SARLAFT o riesgo | Cumplimiento |
| Solicitud desistida / sin cupo en pagaduría | Evento de fin | Sin cupo o sin firma | Canales |

## Investigación complementaria
### Tema investigado:
Buenas prácticas BPMN 2.0.2 y contraste con el caso base (agendamiento de citas) y con los lineamientos MRAE v3.0 de arquitectura institucional.

### Resumen:
El estándar BPMN 2.0.2 de OMG define eventos, actividades y compuertas con semántica ejecutable; se aplicaron sus reglas de un único evento de inicio, compuertas exclusivas con salidas etiquetadas y cierre de todos los caminos en eventos de fin. Frente al caso base de la clase (un solo flujo con dos carriles), el proceso de Ban100 introduce un carril de contraparte pública y una bifurcación por madurez tecnológica, lo que lo hace representativo de un modelo B2G.

En el MRAE v3.0 este modelo alimenta el dominio de **Arquitectura Institucional**: `MAE.LI.AIN.02` (mapa de capacidades), `AIN.03` (modelo operativo) y `AIN.04` (catálogo de servicios, con las cinco líneas de producto: libranza, microcrédito, consumo, ahorro y CDT). La meta de originación < 15 minutos se vincula con `MGGTI.LI.ES.07` (indicadores) y el uso de biometría y firma en línea con `PRI_01` (excelencia en los servicios) y `PRI_08` (seguridad digital).

### Vista ArchiMate equivalente
| Elemento BPMN | Elemento ArchiMate 3.2 | Relación |
|---|---|---|
| Carril *Pensionado / Empleado Público* | Business Actor | *asignado a* el proceso |
| Proceso completo | Business Process *Originación de Crédito de Libranza* | *realiza* el Goal *Originación 100% digital (< 15 min)* |
| Carril *Canales Digitales* | Application Component | *sirve a* el proceso |

## Referencias
Ver [`referencias.md`](./referencias.md).

---

_Este documento hace parte de la entrega del taller 1 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
