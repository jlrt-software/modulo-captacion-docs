# Historias de usuario

Las tres historias del módulo siguen el formato de la cátedra: enunciado “Como… quiero… para…”, criterios de aceptación y prioridad. Cada una se sigue en el tablero de GitHub Projects como un issue con sus tareas.

Tablero: https://github.com/orgs/jlrt-software/projects/1

## HU1

**Como persona interesada en un producto de JLRT, quiero dejar mi consulta en la landing del producto, para que me contacten sin tener que conocer a los socios.**

- **Prioridad:** Media
- **Tarea del Gantt (Entrega 2):** C3
- **Criterios de aceptación:** El formulario pide nombre, teléfono o correo, producto y mensaje, y una casilla de consentimiento obligatoria. Si falta un dato obligatorio, no se guarda y se indica qué falta. Si ya hay una consulta abierta del mismo contacto y producto, el mensaje se agrega a esa consulta. Si no, queda registrada en estado “nuevo”, con su fecha de alta.

**Tareas:**

- Modelar en BPMN el ingreso por formulario (diseño)
- Definir campos, validaciones y consentimiento del formulario (diseño)
- Desarrollar el formulario en la landing de Calibr.ar (C3) (desarrollo)

## HU2

**Como socio de JLRT, quiero recibir un aviso por correo cada vez que entra una consulta por el formulario, para tomarla y contactar al cliente en 3 horas o menos.**

- **Prioridad:** Alta
- **Tarea del Gantt (Entrega 2):** C4
- **Criterios de aceptación:** El aviso les llega a todos los usuarios activos en menos de 5 minutos desde el alta (M2) e incluye un enlace a la consulta. El panel registra quién la tomó y cuándo. Si pasan 3 horas sin pasar a “contactado”, la consulta queda marcada fuera de la meta M3.

**Tareas:**

- Modelar en BPMN el aviso y el temporizador de 3 horas (diseño)
- Definir los indicadores M2 y M3 y sus campos de medición (diseño)
- Desarrollar el aviso automático por correo (C4) (desarrollo)

## HU3

**Como socio de JLRT, quiero cargar desde el celular una consulta que surgió en una charla, para que no se pierda y quede en seguimiento.**

- **Prioridad:** Alta
- **Tarea del Gantt (Entrega 2):** C5
- **Criterios de aceptación:** La carga pide solo nombre, teléfono o correo y producto, y funciona desde el celular. La consulta queda en estado “contactado”, con quien la cargó como responsable. El consentimiento queda pendiente hasta que la persona lo acepte por escrito; si no lo acepta en 48 horas, sus datos se suprimen. El panel no permite cargar una consulta abierta duplicada y muestra la existente.

**Tareas:**

- Modelar en BPMN la carga manual (diseño)
- Definir la regla de consentimiento escrito y de duplicados (diseño)
- Desarrollar el panel con carga manual (C5) (desarrollo)

## Por qué las tareas de diseño avanzan antes que las de desarrollo

El módulo se programa en diciembre de 2026, según el Gantt de la Entrega 2. Por eso cada historia tiene tareas de diseño, que se hacen ahora y se cierran con los Pull Requests de este repositorio, y una tarea de desarrollo, que queda en “Por hacer” hasta diciembre. Las historias quedan en “En progreso”: su diseño está terminado y su desarrollo, planificado.
