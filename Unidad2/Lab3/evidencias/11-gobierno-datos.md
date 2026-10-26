# Gobierno de datos

| Dato | Finalidad | Responsable | Usuarios autorizados | Protección | Retención | Acción al finalizar |
|---|---|---|---|---|---|---|
| nombre | Identificar al cliente y brindarle atención y facturación | Atención al Cliente | Atención al Cliente, Facturación, DBA | Control de acceso por rol, cifrado en base de datos y bitácora de consultas | Mientras el cliente siga activo | Eliminar o anonimizar al cancelar, conservando solo lo exigido por ley |
| correo | Comunicación, soporte y notificaciones | Atención al Cliente | Atención al Cliente, DBA | Control de acceso por rol, cifrado y enmascarado en reportes | Mientras el cliente siga activo | Eliminar al cancelar y retirar de listas de envío y sistemas externos |
| telefono | Contacto directo y soporte técnico | Atención al Cliente | Atención al Cliente, DBA | Control de acceso por rol, cifrado y enmascarado en reportes | Mientras el cliente siga activo | Eliminar al cancelar y retirar de sistemas externos |
| rfc | Facturación y obligaciones fiscales | Facturación | Facturación, DBA | Acceso restringido, cifrado y registro de cada consulta | 5 años por ley | Eliminar de forma segura al cumplirse el plazo, incluyendo respaldos |
| edad | Análisis y segmentación demográfica | Analítica | Analítica, DBA | Uso en grupos o rangos de edad, sin vincularla al nombre | Mientras el cliente siga activo | Eliminar al cancelar o conservar solo de forma anonimizada |
| ciudad | Ubicación y estadísticas geográficas | Analítica | Atención al Cliente, Analítica, DBA | Control de acceso por rol y reportes agrupados por zona | Mientras el cliente siga activo | Eliminar al cancelar o conservar solo de forma anonimizada |
| codigo_postal | Cobertura logística y estadísticas de zona | Operaciones | Operaciones, Logística, Analítica | Control de acceso por rol y reportes agrupados por zona | Mientras el cliente siga activo | Eliminar al cancelar o conservar solo de forma anonimizada |
