# Reflexión Individual

## Nombre del Estudiante

Samuel Guerrero Arcos

## Rol en el equipo

Mi rol fue de coordinación y consolidación documental. Al inicio del semestre armé el repositorio: la estructura de carpetas por taller, las plantillas de informe y referencias, y la primera versión de la visión preliminar y la ficha de caracterización de Ban100. Mientras Krish se encargaba de casi toda la parte gráfica, yo me concentré en que los informes contaran la misma historia que los diagramas y en que cada taller retomara lo que había dejado el anterior.

Ese rol pesó más al final. En el Taller 8 redacté el informe de integración de vistas y la tabla de verificación de cero elementos huérfanos del tablero de cinco capas. En el Taller 9 consolidé la matriz de 12 riesgos, el plan de implementación en cuatro fases, el plan de gobernanza con sus cinco principios y tres métricas, el procedimiento de cambios con las ADR-01 y ADR-02, el formato de retroalimentación del cliente y el resumen ejecutivo.

## Aprendizajes Clave

- Aprendí que la arquitectura empresarial sirve para decidir el orden de las cosas, no solo para dibujar el estado actual. En el roadmap, el riesgo más alto era R1 (la contraparte B2G, nivel 12), pero la Fase 1 terminó siendo la regulatoria porque las brechas de la Ley 1581 y de DLP bloqueaban el resto. De ahí salió el principio P4, «cumplir antes de escalar».
- Comprendí mejor el valor de la trazabilidad entre artefactos. Cuando armé la matriz de riesgos me impuse que ningún riesgo ni ninguna fase se inventara para la entrega: cada uno tenía que salir de un taller anterior (R1 del Taller 4, R3 y R4 de las amenazas STRIDE, R2 de las brechas del checklist). Al final esa trazabilidad fue lo que le dio peso a la propuesta frente al cliente.
- Entendí que un principio arquitectónico tiene que poder descartar algo. Arrastrábamos «nube como primera opción» del MRAE como si fuera absoluto, y la evidencia del Taller 4 mostró que el cuello de botella de los 3 a 5 días estaba en las pagadurías y no en dónde corre el Core. Retirar ese principio y documentar por qué me enseñó más que formular los nuevos.
- Practiqué escribir para lectores distintos. Un mismo análisis tuvo que quedar como informe técnico para el profesor, como resumen ejecutivo para la Junta Directiva de Ban100 y como ADR para un futuro comité de arquitectura.

## Retos Superados

- Al principio me costó que los entregables no se contradijeran entre sí, porque cada taller se hacía en semanas distintas y los nombres de los componentes cambiaban de un archivo a otro. Lo resolví en el Taller 8 obligándome a usar en el tablero integrado el mismo nombre que cada elemento tenía en su entregable de origen, y en la capa de información a anotar la entidad exacta del modelo ER del Taller 2. Así cualquiera puede verificar la conexión sin abrir el otro archivo.
- Otro reto fue convertir una propuesta técnica en algo que un banco aprobaría. Las fases tenían sentido en el papel, pero faltaba pensar en las personas: los analistas de visación cuya tarea desaparece con el RPA, las pagadurías sin personal de TI y el equipo del Core que podía frenar el Bus CDC. La sección de gestión del cambio salió de preguntarme quién perdía algo con cada fase.
- Aprendí que es importante definir cómo se mantiene viva la arquitectura después del proyecto. El procedimiento de cambios existe para que el TO-BE de 2027 no se convierta en el AS-IS rígido de 2029, y eso me hizo ver la gobernanza como un trabajo continuo.
- También usé herramientas de IA como apoyo para redactar y revisar documentos. Aprendí a tratar lo que producían como un borrador que había que contrastar con los datos del proyecto, porque si no lo hacía aparecían cifras o nombres que no salían de ningún taller.

## Áreas por Mejorar

- Me gustaría reforzar mi conocimiento de ArchiMate más allá de las vistas que hicimos, sobre todo los puntos de vista de estrategia y de capacidades, y de cómo se conecta TOGAF ADM con un repositorio de arquitectura real como el que propusimos para la Fase 4.
- Reconozco que debo mejorar en repartir mejor la carga a lo largo del semestre. Concentré buena parte de la consolidación en los talleres 8 y 9, y si hubiera ido integrando desde antes habríamos corregido las inconsistencias más temprano y con menos presión.
- También quiero mejorar en hacer más concisos los documentos. Tiendo a escribir mucho detalle y para la presentación de 10 minutos tuvimos que recortar bastante.

## Contribución Personal

Siento que mi mayor aporte al equipo fue convertir el trabajo de los talleres en una propuesta coherente para Ban100. Me encargué de que los riesgos, las fases, los principios y las métricas apuntaran a lo mismo y se pudieran rastrear hasta la entrevista con el cliente y los diagramas de mis compañeros, de modo que la presentación final pudiera defender cada decisión con evidencia del propio proyecto.

---

_Esta reflexión individual hace parte de la entrega final del curso AREM - Arquitectura Empresarial - Universidad de La Sabana._
