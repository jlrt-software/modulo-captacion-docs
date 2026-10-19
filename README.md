# JLRT Software — Módulo de captación y gestión comercial

Documentación técnica del módulo de captación y gestión comercial de **JLRT Software**. Este repositorio es parte del Trabajo Práctico Integrador de *Organización Empresarial* (Tecnicatura Universitaria en Programación a Distancia, Universidad Tecnológica Nacional, 2026).

> El módulo está planificado para diciembre de 2026. Este repositorio documenta su diseño. El código de los productos de JLRT está en repositorios privados.

## El sistema

JLRT Software desarrolla sistemas de gestión para PyMEs de tres rubros: **Chacra** (agro), **Calibr.ar** (talleres mecánicos) y **Agile** (kioscos). Hasta ahora sus clientes llegaron de palabra, y las consultas que surgen en una charla no quedan registradas en ningún lado.

El módulo de captación resuelve eso:

- Registra cada consulta, llegue por el formulario de la landing de un producto o la cargue un socio desde el celular después de una charla.
- Avisa a los socios por correo en menos de 5 minutos.
- Permite tomar cada consulta y seguirla por sus estados: nuevo → contactado → demo → propuesta → cerrado.
- Mide las metas del proyecto, como el primer contacto en 3 horas o menos.
- Cumple la Ley 25.326 de protección de datos personales: pide consentimiento y suprime los datos cuando corresponde.

## Integrantes

| Integrante | Rol en JLRT | Participación en este repositorio |
|---|---|---|
| Leandro Agustín Trabucco Bustos | Desarrollador Full Stack | Autor de la documentación, ramas, commits y Pull Requests |
| Joaquín R. | Líder Técnico | Revisión de pares del Pull Request del modelo BPMN |

## Enlaces

- **Tablero de gestión (GitHub Projects):** https://github.com/orgs/jlrt-software/projects/1
- **Proceso en BPMN 2.0:** [docs/procesos](docs/procesos/README.md)
- **Diccionario de datos y reglas de integridad:** [docs/datos/diccionario-de-datos.md](docs/datos/diccionario-de-datos.md)
- **Historias de usuario:** [docs/backlog/historias-de-usuario.md](docs/backlog/historias-de-usuario.md)
- **Indicadores de control:** [docs/control/indicadores.md](docs/control/indicadores.md)
- **Estructura de la organización:** [docs/organizacion](docs/organizacion/README.md)

## Estructura del repositorio

```
README.md                         portada y Declaración de Uso de IA
docs/
  organizacion/                   sistema abierto y organigramas (actual y propuesto)
  datos/diccionario-de-datos.md   entidades, campos y reglas de integridad
  procesos/                       proceso de captación en BPMN (.bpmn, .svg, .png)
  backlog/historias-de-usuario.md las tres historias de usuario y sus tareas
  control/indicadores.md          indicadores y estándares de desempeño
  ia/registro-de-correcciones.md  detalle de las correcciones sobre la IA
```

## Cómo se trabaja

- La rama `main` está protegida: solo recibe cambios por Pull Request.
- Cada bloque de documentación se trabaja en una rama propia, por ejemplo `docs/proceso-bpmn`.
- Los mensajes de commit indican el tipo de cambio y lo que cambia, en presente. Por ejemplo: `docs: agrega el modelo BPMN del proceso de captación`.
- Cada Pull Request cierra los issues de diseño que resuelve, y el tablero los pasa a “Listo”.

## Declaración de Uso de IA

### Herramienta y propósito

Durante las cuatro entregas se usó **Claude** (Anthropic) como asistente para:

- ordenar cada entrega según su consigna;
- redactar borradores a partir de la información y las decisiones del autor;
- generar las figuras: la matriz FODA, el Gantt, los organigramas y el archivo BPMN 2.0;
- verificar en fuentes oficiales los datos sobre servicios externos y normativa (planes gratuitos de Vercel y Supabase, API de WhatsApp, Ley 25.326, art. 157 de la Ley 19.550);
- auditar cada entrega con un segundo agente que no había participado de la redacción.

La IA **no** aportó los datos del caso: el equipo, los productos, los clientes, las horas disponibles, las metas y cómo funciona hoy la atención de las consultas salieron del autor. Las decisiones de fondo también fueron del autor.

### Los prompts y por qué se estructuraron así

| Entrega | Prompt | Por qué se armó así |
|---|---|---|
| 1 | No se guardó un archivo de contexto. El trabajo se armó conversando con el asistente. | De esa entrega quedaron errores típicos de un borrador sin revisar: el primer diagrama no tenía las flechas de interacción con el ambiente, el texto usaba “sociedad de hecho” (una categoría sin regulación propia desde 2015) y había quedado una mención a un “roadmap” de un borrador anterior. Eso llevó a cambiar la forma de pedir. |
| 2 | Un archivo de contexto con el caso, la consigna, los criterios de la cátedra (no definiciones genéricas), los errores de la Entrega 1 que no había que repetir y reglas explícitas: **no inventar datos, preguntar antes de suponer cualquier fecha, hora o número de las metas, y llevar un registro de las correcciones reales**. | La rúbrica castiga lo genérico y los errores de la IA cuentan como errores del alumno. Con esas reglas, el asistente hizo catorce preguntas antes de redactar (roles, fechas, horas disponibles, números de las metas) en lugar de completarlas solo. |
| 3 | El mismo formato, más una lista de **decisiones que el asistente tenía que preguntar antes de redactar** (qué estructura dibujar, quién va arriba, qué entidades usar) y la obligación de **auditar el trabajo con un segundo agente** antes de cerrar. | En la Entrega 2 el asistente había tomado decisiones que hubo que revertir. Por ejemplo, cargó a Joaquín con tareas que no puede asumir y redujo el rol del autor a diseño e interfaz. En la Entrega 3 esas decisiones se pidieron como preguntas. |
| 4 | La consigna, las observaciones de los docentes y las respuestas del autor a las decisiones que planteó el asistente (repositorio, tablero, historias de usuario, formato del BPMN). | La entrega final consolida las anteriores, así que el prompt empezó por las observaciones docentes y el alcance, antes que por el contenido. |
| Auditorías | “Revisá el trabajo con un agente en paralelo”. El agente recibía la consigna, la rúbrica, los apuntes, las entregas anteriores y el registro de correcciones, con la instrucción de no inventar problemas. | Un agente que no escribió el texto no tiende a darlo por bueno. Encontró errores reales en cada entrega. |

### Qué sesgos del asistente se detectaron y cómo se corrigieron

- **Sobrecargar el plan.** El primer Gantt le daba a Joaquín seis tareas de ejecución, y el asistente propuso un repositorio con Pull Requests que él tendría que revisar seguido. El autor lo rechazó: Joaquín no tiene ese tiempo. Su participación quedó en dos controles puntuales.
- **“Corregir” decisiones del equipo hacia lo que parecía más realista.** El asistente propuso bajar la meta de primer contacto a 24 horas hábiles. El autor la fijó en 3 horas corridas, porque ambos socios priorizan cualquier consulta.
- **Afirmar sin base en el caso.** Un borrador decía que nadie controlaba los cobros. El autor lo corrigió con cómo se cobra realmente.
- **Describir como existente lo que es un plan.** Partes del texto hablaban del módulo en presente. Se pasaron a futuro, porque el módulo se construye en diciembre.
- **Simplificar los roles.** Un borrador reducía el rol del autor a diseño e interfaz, cuando también desarrolla implementaciones grandes. Otro describía el trabajo de infraestructura de Joaquín con un ejemplo demasiado literal. El autor corrigió las dos descripciones.
- **Darse mérito.** La primera Declaración de la Entrega 2 detallaba cada propuesta del asistente. El autor la consideró desproporcionada, porque el contenido y las decisiones eran suyos, y se redujo.
- **Errores propios que encontraron las auditorías:**
  - un camino crítico incompleto en el Gantt;
  - un paso del FODA de la cátedra mal citado;
  - un consentimiento “verbal” que no cumplía la forma escrita que exige la Ley 25.326;
  - el interlineado del documento, que no era 1,5.

El detalle, entrega por entrega, está en [docs/ia/registro-de-correcciones.md](docs/ia/registro-de-correcciones.md).

### Responsabilidad

La asistencia de IA no exime al autor de la veracidad ni de la coherencia del trabajo: cualquier error que haya quedado es del autor.
