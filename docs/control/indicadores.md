# Indicadores de control

El control sigue las cuatro etapas de la cátedra: establecer estándares, medir el desempeño real, compararlo con el estándar y aplicar una acción correctiva cuando el resultado no se acepta. Los estándares salen de las metas de la Entrega 2 y de las reglas de integridad del [diccionario de datos](../datos/diccionario-de-datos.md).

Los indicadores se revisan con frecuencia semanal, salvo el plazo (una vez) y el costo (mensual, con la facturación). La revisión está a cargo de Leandro Trabucco (Desarrollador Full Stack).

## Desempeño del proceso

| Indicador | Medición y fuente | Estándar | Acción correctiva |
|---|---|---|---|
| Tiempo de aviso (M2) | fecha_aviso − fecha_alta, en las consultas del formulario. | Menos de 5 minutos en todas. | Revisar la función de aviso y el proveedor de correo. |
| Primer contacto (M3) | Primer cambio a “contactado” en el Historial − fecha_alta, en las consultas del formulario. | 3 horas o menos por consulta. Se acepta por varianza mientras cumpla al menos el 90 % de las consultas del período. | Revisar por qué nadie la tomó y cómo nos repartimos las consultas. |
| Tasa de cierre ganado | Consultas ganadas / (ganadas + perdidas). | A definir con la línea de base de los primeros meses de uso. | Analizar en qué etapa del embudo se pierden las consultas. |
| Plazo (M1) | Fecha real de puesta en producción (se mide una vez). | Antes del 10/01/2027. | Replanificar el Gantt y reducir el alcance de la primera versión. |
| Costo (M4) | Facturación mensual de Supabase, Vercel y el proveedor de correo. | USD 0 por mes. | Revisar los límites de los planes gratuitos y el uso. |

## Auditoría técnica del sistema

| Indicador | Medición y fuente | Estándar | Acción correctiva |
|---|---|---|---|
| Disponibilidad del formulario | Días con el proyecto de Supabase pausado por inactividad. | Cero días. | Reactivar el proyecto y programar una actividad mínima periódica. |
| Integridad referencial (RI2) | Consultas o registros del Historial que apuntan a registros inexistentes. | Cero. | Corregir los datos y revisar la restricción que falló. |
| Transiciones de estado (RI9) | Registros del Historial con un cambio de estado no permitido. | Cero. | Revisar la función que valida los cambios de estado. |
| Consistencia de estados (RI10) | Consultas cuyo estado no coincide con el último registro del Historial. | Cero. | Revisar la operación que cambió el estado sin registrar el Historial. |
| Duplicados abiertos (RI12) | Consultas abiertas del mismo producto con el mismo teléfono o correo. | Cero. | Unificar las consultas y revisar los índices únicos. |
| Acceso a los datos (RI13) | Lecturas de consultas sin sesión o hechas por usuarios inactivos, según los registros de Supabase. | Cero. | Revisar las reglas de acceso por fila. |
| Supresión a tiempo (RI14) | Consultas cargadas a mano con el consentimiento vencido y los datos sin suprimir. | Cero. | Suprimir los datos y revisar la función de supresión. |

La tasa de cierre ganado no tiene estándar numérico todavía: no hay línea de base, porque hoy las consultas no se registran. Los primeros meses de uso del módulo la van a dar.
