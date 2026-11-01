# Registro de Trabajo en Clase — Taller 8: Integración de Vistas

## Fecha de la sesión
31 de octubre de 2026

## Integrantes presentes
- Santiago Barrera Rueda
- Krish Purmessur Moros
- Samuel Guerrero Arcos

## Actividades realizadas en clase

Se trabajó el caso base **FarmApp** siguiendo la metodología de 5 pasos de la guía del taller, antes de aplicar lo mismo al cliente real.

**Qué se discutió.** La diferencia entre un tablero integrado y cinco diagramas pegados. El punto de partida fue reconocer que ya teníamos las cinco vistas de FarmApp enunciadas en el README del taller, pero sueltas: el trabajo no era dibujar nada nuevo, sino decidir qué conecta con qué y por qué.

**Decisiones de modelado tomadas.**

1. **Una sola banda por capa, apiladas verticalmente.** Se descartó la alternativa de distribuirlas en columnas porque la dirección de las relaciones —de negocio hacia tecnología— se lee mejor de arriba hacia abajo.
2. **Trazar un hilo de negocio a la vez.** Se eligió *Compra Online* porque es el proceso que atraviesa las cinco capas y el que la guía desarrolla como ejemplo. *Prescripción* y *Despacho* quedaron identificados pero sin trazar, para evitar la saturación que advierte el Paso 3.
3. **Mostrar los elementos fuera del hilo en gris** en lugar de eliminarlos del tablero. Así se ve que el inventario está completo y que lo no trazado es una decisión de alcance, no un olvido.
4. **Usar la notación ArchiMate desde el principio.** Siguiendo la sección final de la guía, se rotularon los elementos con sus estereotipos (*Business Process*, *Application Component*, *Data Object*, *Node*, *Requirement*) y las relaciones con los nombres del metamodelo: *realizado por*, *accede a*, *asignado a*, *protege*. La guía indica que así el tablero del Taller 8 ya es la vista ArchiMate final y no hay que redibujar nada dos veces.
5. **Agregar relaciones que el ejemplo de la guía no traza.** En el Paso 5 de la guía las entidades de información quedan marcadas con "—" hacia abajo. Se decidió conectar *Producto*, *Cliente*, *Pedido* y *Descuento* con la *Base de Datos Replicada* mediante *almacenado en*, de modo que ningún elemento del hilo quede sin conexión hacia abajo. Es una desviación deliberada del ejemplo, tomada para cumplir el criterio de cero huérfanos de la checklist.

**Herramientas usadas.** draw.io (app.diagrams.net) para el tablero; la página interactiva `visualizacion-integracion-vistas.html` del repositorio del taller como referencia para contrastar nuestras conexiones con las del docente.

**Hasta dónde se llegó.** Se completaron los cinco pasos sobre FarmApp: las dos vistas del tablero (capas sueltas e hilo trazado) y la tabla de verificación de huérfanos.

## Boceto inicial del modelo

El tablero quedó en [`tablero-farmapp.drawio`](./tablero-farmapp.drawio), con dos páginas que corresponden a dos pasos de la metodología:

- **Página 1 — "Paso 2: Capas sueltas"**: los 17 elementos de las cinco vistas ubicados en su banda, sin ninguna conexión.
- **Página 2 — "Paso 3: Hilo Compra Online"**: el mismo tablero con las 15 relaciones del hilo trazadas de punta a punta, y los elementos de otros hilos atenuados.

### Hilo trazado

`Compra Online` → `Plataforma E-commerce` y `App Móvil` → `Producto`, `Cliente`, `Pedido`, `Descuento` → `Nube Híbrida` → `Base de Datos Replicada`, con `Cifrado de datos personales` y `Monitoreo de fraude` protegiendo la plataforma.

### Narrativa de coherencia (Paso 4)

El proceso de Compra Online se apoya en la Plataforma E-commerce y en la App Móvil porque la mayoría de las compras de FarmApp ya ocurren desde dispositivos móviles. Ambas comparten las mismas entidades de información para evitar inconsistencias de inventario entre el canal digital y el punto físico: si la App y el POS consultaran copias distintas de *Producto*, un medicamento podría venderse dos veces. Corren sobre la Nube Híbrida con Base de Datos Replicada, decisión del Taller 4 para tolerar los picos de demanda de las campañas promocionales. El cifrado de datos personales y el monitoreo de fraude se aplican sobre la Plataforma E-commerce, y no sobre el POS, porque es el componente que procesa el pago electrónico, el activo más sensible identificado en el Taller 5.

### Verificación de huérfanos (Paso 5)

| Elemento | Capa | ¿Conectado hacia arriba? | ¿Conectado hacia abajo? |
|---|---|---|---|
| Compra Online | Negocio | — (capa más alta) | Plataforma E-commerce, App Móvil |
| Plataforma E-commerce | Aplicaciones | Compra Online | Producto, Cliente, Pedido, Descuento, Nube Híbrida, Cifrado, Monitoreo de fraude |
| App Móvil | Aplicaciones | Compra Online | Nube Híbrida |
| Producto | Información | Plataforma E-commerce | Base de Datos Replicada |
| Cliente | Información | Plataforma E-commerce | Base de Datos Replicada |
| Pedido | Información | Plataforma E-commerce | Base de Datos Replicada |
| Descuento | Información | Plataforma E-commerce | Base de Datos Replicada |
| Nube Híbrida | Infraestructura | Plataforma E-commerce, App Móvil | Base de Datos Replicada |
| Base de Datos Replicada | Infraestructura | Nube Híbrida, Producto, Cliente, Pedido, Descuento | — |
| Cifrado de datos personales | Seguridad | Plataforma E-commerce | — (capa más baja) |
| Monitoreo de fraude | Seguridad | Plataforma E-commerce | — (capa más baja) |

**Resultado del hilo Compra Online:** 11 elementos verificados · **0 huérfanos**.

Los elementos *Prescripción*, *Despacho*, *Sistema POS*, *CRM*, *Servidores Regionales* y *Control de acceso por rol* permanecen en el tablero en gris: pertenecen a los otros dos hilos de negocio, que se trazarían con el mismo método.

## Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|----------------|-------------|----------------|
| Tablero integrado del cliente en draw.io (5 capas + TO-BE del Taller 7) | Samuel Guerrero | 31/10 |
| Narrativa de coherencia y tabla de verificación de huérfanos del cliente | Santiago Barrera | 31/10 |
| Investigación complementaria y referencias | Krish Purmessur | 31/10 |
| Revisión cruzada de nombres contra los entregables de los Talleres 1–7 | Equipo completo | 31/10 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 8 en el curso AREM - Universidad de La Sabana._
