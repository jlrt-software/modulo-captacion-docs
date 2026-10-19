# Diccionario de datos del módulo de captación

El diccionario se armó en la etapa de diseño (Entrega 3 del trabajo integrador) y se amplió en la Entrega 4 con las reglas de integridad. Los tipos son genéricos; los nombres de los campos van en minúscula y sin tildes, como se van a escribir en la base (Supabase / PostgreSQL).

Relaciones: un producto tiene muchas consultas; un usuario es responsable de muchas consultas; cada consulta tiene muchos registros en su Historial, cada uno hecho por un usuario.

## Producto

Los productos por los que alguien puede consultar.

| Campo | Tipo | Descripción funcional | Valores permitidos y restricciones |
|---|---|---|---|
| id_producto | Integer | Identificador único del producto. | Clave primaria, autonumérico. |
| nombre | String | Nombre comercial del producto. | Obligatorio y único, hasta 50 caracteres (hoy: Chacra, Calibr.ar y Agile). |
| rubro | String | Rubro de las PyMEs a las que apunta. | Obligatorio: agro, talleres mecánicos o kioscos. |
| url_landing | String | Dirección de la landing donde está el formulario o la mención a JLRT. | Opcional, hasta 255 caracteres: vacío si el producto todavía no tiene landing. |
| activo | Boolean | Indica si el producto se ofrece y aparece en el formulario. | Por defecto, verdadero. |

## Usuario

Las personas que reciben los avisos y toman las consultas. Hoy son los dos socios; cuando exista el área Comercial y Marketing, sus integrantes se cargan acá con otro rol.

| Campo | Tipo | Descripción funcional | Valores permitidos y restricciones |
|---|---|---|---|
| id_usuario | Integer | Identificador único del usuario. | Clave primaria, autonumérico. |
| nombre | String | Nombre y apellido. | Obligatorio, hasta 100 caracteres. |
| email | String | Correo al que llega el aviso de cada consulta nueva. | Obligatorio, único, hasta 254 caracteres y con formato de correo válido. |
| rol | String | Rol en JLRT, el mismo del organigrama. | Obligatorio: Líder Técnico, Desarrollador Full Stack o Comercial y Marketing. |
| es_socio | Boolean | Indica si el usuario es socio de JLRT; distingue a los socios del personal que se incorpore a Comercial y Marketing. | Obligatorio. Hoy, verdadero en los dos usuarios. |
| activo | Boolean | Indica si recibe avisos y puede tomar consultas. | Por defecto, verdadero. |

## Lead

La entidad central: cada consulta, venga del formulario o de una charla.

| Campo | Tipo | Descripción funcional | Valores permitidos y restricciones |
|---|---|---|---|
| id_lead | Integer | Identificador único de la consulta. | Clave primaria, autonumérico. |
| nombre_contacto | String | Nombre de quien consulta. | Obligatorio, hasta 100 caracteres. Solo queda vacío si se suprimieron los datos (RI14). |
| telefono | String | Teléfono del contacto; habilita el enlace directo de WhatsApp. | Hasta 20 caracteres, con código de área. Obligatorio si no hay correo: tiene que haber al menos uno de los dos. |
| email | String | Correo del contacto. | Opcional, hasta 254 caracteres; si se carga, con formato válido. |
| empresa | String | Nombre del negocio: taller, kiosco o campo. | Opcional, hasta 100 caracteres. |
| mensaje | String | Texto de la consulta o resumen de la charla. | Opcional, hasta 1000 caracteres. |
| id_producto | Integer | Producto por el que consulta. | Obligatorio; referencia a Producto, para que no haya consultas huérfanas. |
| origen | String | Por dónde llegó la consulta. | Obligatorio: “formulario” o “carga manual”. |
| estado | String | Etapa del embudo comercial en la que está la consulta. | Obligatorio: nuevo, contactado, demo, propuesta o cerrado. Al crearse: “nuevo” si entra por formulario y “contactado” si se carga a mano. Desde “nuevo” solo se puede pasar a “contactado”; después, solo hacia adelante. |
| id_responsable | Integer | Usuario que tomó la consulta (el “tomado por” del panel). | Referencia a Usuario; vacío solo mientras el estado es “nuevo”. En la carga manual, el usuario que la carga. |
| fecha_alta | DateTime | Momento en que se registró la consulta. Es el punto de partida para medir M2 y M3. | Obligatorio; lo completa el sistema. Formato: fecha y hora con zona horaria (Argentina, UTC−3). |
| resultado_cierre | String | Cómo terminó la consulta al cerrarse. | Obligatorio cuando el estado es “cerrado”: “ganado”, “perdido” o “descartado” (datos suprimidos por falta de consentimiento); vacío en los demás estados. |
| fecha_toma | DateTime | Momento en que un usuario tomó la consulta. | Lo completa el sistema al asignar el responsable; en la carga manual, igual a fecha_alta. |
| fecha_aviso | DateTime | Momento en que se envió el correo a los usuarios activos. | Lo completa el sistema; vacío en la carga manual, que no genera aviso. Meta M2: menos de 5 minutos después de fecha_alta. |
| consentimiento | Boolean | Aceptación del tratamiento de los datos personales (Ley N.° 25.326, 2000). | Obligatorio. Verdadero para enviar el formulario; en la carga manual, falso hasta que la persona acepte por escrito. |
| medio_consentimiento | String | Cómo se obtuvo el consentimiento. | Vacío mientras el consentimiento sea falso; después, “formulario” (casilla marcada por el titular) o “mensaje” (aceptación escrita). |
| fecha_consentimiento | DateTime | Momento en que se aceptó el tratamiento de los datos. | Vacío mientras el consentimiento sea falso; en el formulario lo completa el sistema y en la carga manual, el usuario. |
| fecha_supresion | DateTime | Momento en que se suprimieron los datos personales, a pedido del titular o por falta de consentimiento. | Vacío si no hubo supresión; lo completa el sistema (RI14). |

## Historial de estados

Cada cambio de estado de una consulta. Es el que permite medir cuándo se llegó a cada estado.

| Campo | Tipo | Descripción funcional | Valores permitidos y restricciones |
|---|---|---|---|
| id_historial | Integer | Identificador único del cambio. | Clave primaria, autonumérico. |
| id_lead | Integer | Consulta a la que pertenece el cambio. | Obligatorio; referencia a Lead. |
| estado_anterior | String | Estado antes del cambio. | Igual al Lead.estado vigente al momento del cambio; vacío solo en el registro de alta. |
| estado_nuevo | String | Estado después del cambio. | Obligatorio; mismos valores que Lead.estado. |
| fecha_cambio | DateTime | Momento del cambio. | Obligatorio; lo completa el sistema. Meta M3: en los leads del formulario, el primer cambio a “contactado” tiene que estar a 3 horas o menos de fecha_alta. |
| id_usuario | Integer | Usuario que hizo el cambio. | Referencia a Usuario; vacío solo en el alta automática por formulario. |
| nota | String | Comentario del usuario: qué se habló y cuál es el próximo paso. | Opcional, hasta 500 caracteres. |

## Reglas de integridad

Las reglas se agrupan por tipo: de entidad (identificación de cada registro), referenciales (vínculos entre tablas), de dominio (valores que acepta cada campo) y de negocio (condiciones que surgen del proceso). Se suman las de duplicados, acceso y supresión de datos personales. La columna de la derecha dice cómo se aplica cada una en la base.

| ID | Tipo | Regla | Cómo se aplica |
|---|---|---|---|
| RI1 | De entidad | Cada registro se identifica con su clave primaria, que no puede repetirse ni quedar vacía. | Clave primaria autonumérica en las cuatro tablas. |
| RI2 | Referencial | Toda consulta apunta a un producto existente y, si tiene responsable, a un usuario existente; todo registro del Historial apunta a una consulta existente. | Claves foráneas. Productos y usuarios no se borran: se desactivan con el campo activo, para no dejar consultas huérfanas. |
| RI3 | De dominio | estado, origen, resultado_cierre, medio_consentimiento, rol y rubro solo aceptan los valores de su lista. | Restricción de valores permitidos en cada campo. |
| RI4 | De dominio | El correo tiene formato válido; el teléfono lleva código de área y solo admite dígitos y el signo +, hasta 20 caracteres. | Validación en el formulario y restricción en la base. |
| RI5 | De negocio | Toda consulta tiene al menos un medio de contacto, salvo que sus datos se hayan suprimido. | Restricción que exige teléfono o correo mientras fecha_supresion esté vacía. |
| RI6 | De negocio | Una consulta del formulario solo se guarda con consentimiento verdadero. Una cargada a mano puede guardarse sin él, y entonces medio_consentimiento y fecha_consentimiento quedan vacíos. | Restricción que combina origen, consentimiento, medio y fecha del consentimiento. |
| RI7 | De negocio | El responsable está vacío solo en estado “nuevo”, y resultado_cierre se completa solo en estado “cerrado”. | Restricción sobre la combinación de campos. |
| RI8 | De negocio | fecha_aviso, fecha_toma, fecha_consentimiento, fecha_supresion y cada fecha_cambio del Historial son iguales o posteriores a fecha_alta. | Restricción en Lead y función de control al insertar en el Historial. |
| RI9 | De negocio | Desde “nuevo” solo se pasa a “contactado”; después, solo hacia adelante, y “cerrado” es definitivo. | Función que valida cada cambio de estado antes de guardarlo. |
| RI10 | De negocio | Todo cambio de Lead.estado genera, en la misma operación, su registro en el Historial, así que el estado de la consulta coincide siempre con el último estado_nuevo. | Disparador (trigger) sobre la tabla Lead. |
| RI11 | De negocio | Los registros del Historial no se modifican ni se borran: son la evidencia con la que se miden las metas. | Reglas de acceso que solo permiten agregar registros. |
| RI12 | Duplicados | No puede haber dos consultas abiertas del mismo producto con el mismo teléfono o el mismo correo. Si llega una por el formulario, su mensaje se agrega al Historial de la existente. | Índices únicos limitados a las consultas que no están cerradas. |
| RI13 | De acceso | El formulario solo puede crear consultas, nunca leerlas, y solo los usuarios activos ven y modifican las consultas. | Reglas de acceso por fila (RLS) de Supabase. |
| RI14 | De supresión (Ley 25.326) | Si el titular pide que se borren sus datos, se vacían nombre, teléfono, correo, empresa y mensaje, pero la consulta se conserva con sus fechas y su Historial. Si la supresión se debe a que no aceptó el consentimiento en 48 horas, la consulta además se cierra como “descartado”. | Función de supresión que vacía los datos, completa fecha_supresion y registra el cambio en el Historial. |

Los indicadores de auditoría técnica ([docs/control/indicadores.md](../control/indicadores.md)) controlan el cumplimiento de estas reglas.

## Metas que se miden con estos datos

- **M2 (aviso en menos de 5 minutos):** `fecha_aviso − fecha_alta` de cada consulta del formulario.
- **M3 (primer contacto en 3 horas o menos):** primer registro del Historial con `estado_nuevo = contactado` menos `fecha_alta`, en las consultas del formulario.
