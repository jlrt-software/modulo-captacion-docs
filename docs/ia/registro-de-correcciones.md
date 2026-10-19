# Registro de correcciones sobre la IA

Este registro resume, entrega por entrega, qué propuso el asistente de IA (Claude) y qué corrigió o decidió el autor. Solo incluye hechos que ocurrieron. Se omiten datos comerciales y personales que no hacen falta para entender las correcciones.

## Entrega 1 — La organización y su enfoque sistémico

| Qué había en el borrador de la IA | Corrección del autor |
|---|---|
| Diagrama del sistema abierto sin flechas de interacción entre el ambiente y el sistema. | Pidió agregarlas explícitamente. |
| JLRT calificada como “sociedad de hecho”. | Se corrigió a sociedad no constituida regularmente, de la Sección IV de la Ley General de Sociedades. |
| Mención residual a un “roadmap de Calibr.ar” que venía de un borrador anterior. | Se eliminó. |

## Entrega 2 — Diagnóstico y planeación

| Qué propuso el asistente | Corrección o decisión del autor |
|---|---|
| Bajar la meta de primer contacto a 24 horas hábiles. | La rechazó y la fijó en 3 horas corridas: cualquier consulta tiene prioridad. |
| Un Gantt con Joaquín a cargo de seis tareas de ejecución. | Lo objetó: Joaquín no tiene ese tiempo. Quedó en dos controles (validar el modelo y revisar la seguridad). |
| Un repositorio del módulo con Pull Requests aprobados por Joaquín. | Primero lo aceptó y después lo descartó: la consigna no pide construir el módulo y Joaquín no tiene tiempo. |
| Ejecutar el plan en octubre y, después, desde el 7 de diciembre. | Lo ubicó del 1 al 30 de diciembre, cuando termina la cursada, con la meta al 10 de enero de 2027. |
| Roles con tareas genéricas; después, un rol del autor reducido a diseño e interfaz. | Corrigió dos veces la descripción con las tareas reales de cada socio y sumó la diferencia de experiencia que explica el reparto. |
| Un párrafo sobre feriados como días sin trabajo. | Lo eliminó por irreal: los feriados son los días en que más trabajan. |
| Una Declaración de IA extensa, con cada propuesta del asistente. | La redujo a las correcciones de fondo, porque el contenido y las decisiones eran suyos. |
| Citas del apunte con un formato distinto al de la Entrega 1. | Pidió unificarlas como “(UTN, 2026a)”. |
| Meta M2 (aviso en menos de 5 minutos), propuesta por el asistente. | La aceptó. |

Una auditoría con un segundo agente, pedida por el autor, detectó:

- un camino crítico incompleto;
- un paso de la cátedra mal citado;
- la restricción de uso no comercial del plan gratuito de Vercel sin mencionar;
- un interlineado distinto de 1,5.

Todo se corrigió.

## Entrega 3 — Estructura formal y diseño de datos

| Qué propuso el asistente | Corrección o decisión del autor |
|---|---|
| Opciones de organigrama: estructura actual, área de sistemas o propuesta para la SRL. | Eligió graficar la actual y la propuesta. |
| Ubicar al Desarrollador Full Stack debajo del Líder Técnico o al mismo nivel. | Decidió el mismo nivel: son socios iguales. |
| Incluir un contador como staff. | Aportó que no tienen contador. En la propuesta quedó como asesoría externa a incorporar. |
| Una tabla que afirmaba, sin base en el caso, que nadie controlaba los cobros. | La corrigió con cómo se cobra realmente. |
| Una Declaración de IA que presentaba como hallazgos de los agentes las correcciones del trabajo. | Pidió que reflejara que él dirigió las iteraciones de corrección. |
| Campo `resultado_cierre`, sugerido por un revisor. | Decidió sumarlo. |
| “Parecía un trámite”, en la conclusión. | Lo cambió por “parecía una tarea fácil” al exportar el PDF. |

El autor pidió tres revisiones con agentes independientes, una de los organigramas y dos del documento. Entre otros errores, encontraron:

- dos principios de organización analizados de forma forzada;
- el módulo descripto en presente;
- un consentimiento “verbal” que no cumplía la Ley 25.326;
- la falta de una regla de transiciones de estado.

## Entrega 4 — Procesos, trabajo colaborativo y control

| Qué propuso el asistente | Corrección o decisión del autor |
|---|---|
| Repositorio de documentación en la organización JLRT, GitHub Projects como tablero, historias de usuario con tareas de diseño que avanzan antes que las de desarrollo y BPMN generado como archivo `.bpmn`. | Aceptó el alcance. Eligió a Joaquín como revisor del Pull Request y fijó la entrega para el 20 de octubre. |
| Valores sugeridos para los indicadores y para el plazo del consentimiento. | Fijó los valores definitivos: primer contacto en 3 horas con al menos el 90 % de cumplimiento, revisión cada dos semanas a cargo del Desarrollador Full Stack (por el bajo número de consultas esperado) y 48 horas para aceptar el consentimiento. |
| Interpretación de las observaciones docentes sobre la Entrega 3. | Aceptó la propuesta: rectángulos con cargos y niveles directivo y operativo marcados en los organigramas, y una tabla de reglas de integridad clasificadas por tipo. |
| Resolver la revisión que le faltó al PR del modelo BPMN, integrado sin revisión al mergear la rama que salía de la suya, con un PR nuevo que corrige los enlaces a la organización y le pide a Joaquín revisar también el modelo. | Lo aceptó y le pidió a Joaquín una revisión breve. Joaquín pidió cambios: duplicados con envíos simultáneos y consultas que quedan abiertas si el cliente no contesta. |
| Soluciones para las observaciones: alta por formulario en una sola operación de la base, con índices sobre el correo y el teléfono normalizados (RI12), y cierre automático como “sin respuesta” tras 30 días sin actividad (RI15). | Las aceptó y confirmó el plazo de 30 días. |
| Commits con una línea que nombraba al asistente como coautor. | La rechazó: el uso de IA se declara en la Declaración de Uso de IA del README, no en el historial de Git. Se reescribió el commit. |
