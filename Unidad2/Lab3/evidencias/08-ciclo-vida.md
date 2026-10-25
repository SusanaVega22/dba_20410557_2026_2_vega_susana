# Ciclo de vida del dato

**Situación:** una solicitud de cancelación fue autorizada por el área responsable. Antes de ejecutar un `DELETE` sobre la tabla principal, hay que revisar dónde más vive la información de esa persona.

## Análisis previo

- **¿Existen otras tablas relacionadas?** Sí. Pueden existir tablas de pedidos, facturas, tickets de soporte o direcciones que guardan el id o los datos del cliente. Hay que revisar las llaves foráneas y decidir qué se borra, qué se anonimiza y qué se debe conservar por ley.
- **¿Existen respaldos?** Sí. Cada respaldo periódico guarda una fotografía de la base tal como estaba ese día, con el cliente incluido.
- **¿Existen réplicas?** Sí. Los servidores espejo o de consulta repiten lo que hay en la base principal y pueden tardar en reflejar el borrado.
- **¿Existen registros de auditoría?** Sí. Las bitácoras guardan quién consultó o modificó al cliente, y a veces contienen el nombre, el correo o el id.
- **¿Existen copias utilizadas para analítica?** Sí. El almacén de datos y los tableros de BI pueden conservar la información del cliente aunque ya no esté en el sistema operativo.
- **¿Existen archivos exportados?** Sí. Hojas de Excel, CSV o PDF que alguien descargó para un reporte y que quedaron en computadoras, correos o carpetas compartidas.
- **¿Existen sistemas externos?** Sí. Herramientas de terceros como correo masivo, CRM, paquetería o facturación, que recibieron datos del cliente y los guardan por su cuenta.

## Mapa

```
clientes
   │
   ├── tablas relacionadas
   ├── respaldos
   ├── réplicas
   ├── bitácoras de auditoría
   ├── analítica (almacén de datos)
   ├── reportes
   ├── exportaciones
   └── sistemas externos
```

## Pregunta

**¿Por qué eliminar un registro de una tabla no necesariamente significa que toda la información relacionada con esa persona haya desaparecido de la organización?**

Porque el `DELETE` solo quita al cliente de un lugar: la tabla donde se ejecuta. Los datos de una persona no viven en un único sitio, sino que se van copiando a muchos otros durante su ciclo de vida: respaldos, réplicas, bitácoras, bases de analítica, archivos descargados y servicios de terceros. Ninguno de esos lugares se actualiza solo cuando se borra el registro original, así que la información sigue existiendo y puede volver a aparecer, por ejemplo al restaurar un respaldo. Por eso, atender una cancelación de forma completa requiere un procedimiento que identifique todas estas copias, borre o anonimice las que corresponda, avise a los terceros y conserve únicamente lo que la ley obliga a guardar, como los datos fiscales por 5 años.
