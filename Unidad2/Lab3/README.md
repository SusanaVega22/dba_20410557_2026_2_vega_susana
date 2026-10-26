# Laboratorio de privacidad en bases de datos

## 1. Introducción

Este laboratorio trata el problema de recolectar de más, guardar datos para siempre y dar accesos sin control a la información personal dentro de las bases de datos. Muchas organizaciones acumulan datos sin fecha de término o dan permisos amplios para trabajar más fácil. Esto crea vulnerabilidades serias, puede incumplir las leyes de privacidad y aumenta el daño en caso de una fuga de información.

## 2. Inventario de datos

Los datos de la plataforma se agrupan según su sensibilidad y su función:

- **Identificación y contacto:** nombre, correo, telefono.
- **Fiscales y contables:** rfc.
- **Demográficos y estadísticos:** edad, ciudad, codigo postal.

## 3. Finalidades

Cada dato debe tener un propósito operativo o legal concreto:

- **nombre, correo, telefono:** identificar al usuario, permitirle entrar a su cuenta y darle soporte técnico.
- **rfc:** emitir comprobantes fiscales y cumplir con las obligaciones ante el SAT.
- **edad, ciudad, codigo postal:** hacer estadísticas de la audiencia, organizar entregas y calcular la cobertura del servicio.

## 4. Minimización

- **Datos que se deben limitar o quitar:** campos como edad u ocupacion no deberían ser obligatorios en el registro inicial si no son necesarios para el servicio principal.
- **Justificación:** el principio de minimización indica que solo se debe pedir lo estrictamente necesario. En la zona de analítica se quitan los datos que identifican directamente a la persona y se trabaja solo con información agregada o anónima.

## 5. Control de acceso

Los permisos siguen el principio de menor privilegio:

- **Atención al cliente:** solo ve los datos de contacto que necesita para dar soporte.
- **Facturación:** es la única área con acceso a los datos fiscales y al historial de pagos.
- **Analítica:** trabaja únicamente con datos anónimos o agregados.
- **DBA:** administra la infraestructura sin tener que revisar datos personales en texto plano.
- **Dirección:** consulta reportes consolidados, sin entrar a la base operativa para ver cliente por cliente.

## 6. Derechos ARCO

Desde el punto de vista técnico, atender las solicitudes de Acceso, Rectificación, Cancelación u Oposición (ARCO) requiere:

- Saber en qué tablas y réplicas se guarda la información de la persona.
- Preparar scripts seguros que eliminen o anonimicen los datos sin dañar la integridad referencial de la base.
- Llevar una bitácora de la solicitud atendida, sin conservar los datos que ya fueron cancelados.

## 7. Retención

El tiempo de conservación se define a partir de tres factores:

- **Requisitos legales:** los plazos que la ley obliga a respetar.
- **Duración de la relación con el cliente:** mientras su cuenta siga activa.
- **Plazos de prescripción:** un tiempo razonable después de la cancelación para atender aclaraciones o reclamaciones antes de borrar definitivamente.

## 8. Gobierno de datos

| Rol | Responsabilidad principal |
|---|---|
| Propietario del dato (Negocio) | Decide para qué se usa la información y autoriza quién puede consultarla. |
| Responsable de Privacidad / Oficial de Datos | Vigila el cumplimiento de la normativa y se encarga de las solicitudes ARCO. |
| Área Jurídica | Fija los plazos legales de retención y analiza los riesgos normativos. |
| DBA (Administrador de BD) | Aplica en el sistema los controles de seguridad, cifrado, roles y tareas de borrado. |

## 9. Evaluación integral

Los riesgos más importantes que se encontraron en el escenario fueron:

- El personal de analítica consulta directamente datos identificables de 50,000 clientes.
- La información lleva más de 12 años guardada sin una política formal de retención.
- Los entornos de prueba y desarrollo usan bases con datos reales de clientes.
- Se usan los correos en campañas promocionales sin el consentimiento previo del usuario.
- No hay bitácoras que muestren quién consulta la tabla principal de clientes.

## 10. Conclusiones

La privacidad no se agrega al final como un parche, sino que debe ser una decisión de diseño desde el modelado de la base de datos. Una base bien administrada no solo se protege de los ciberataques, sino que asegura que los datos se usen solo para lo acordado, por el personal autorizado y durante el tiempo justo.

---

## Preguntas de reflexión

### 1. ¿Una base de datos técnicamente segura necesariamente cumple con todos los requisitos de privacidad?

No. La seguridad protege la confidencialidad, pero la privacidad exige más: tener derecho a recolectar los datos, contar con el consentimiento del usuario, usarlos solo para la finalidad acordada y borrarlos a tiempo. Una base muy cifrada y con firewall puede violar la privacidad si guarda datos innecesarios o sin justificación.

### 2. ¿Por qué el principio de mínimo privilegio también contribuye a la privacidad?

Porque si cada empleado solo accede a lo que necesita, hay menos personas con acceso a información sensible y disminuye la posibilidad de que alguien del propio equipo la filtre o la use mal.

### 3. ¿Por qué el DBA no debería decidir por sí solo la finalidad del tratamiento de los datos?

Porque el trabajo del DBA es técnico: mantener el sistema funcionando y seguro. Decidir para qué se usan los datos le corresponde al negocio, a privacidad y al área jurídica, que conocen los contratos y las leyes aplicables.

### 4. ¿Por qué los desarrolladores no deberían recibir automáticamente copias completas de bases de datos productivas?

Porque los entornos de desarrollo suelen tener menos seguridad que producción. Entregarles copias reales deja la información de miles de clientes en laptops o servidores de prueba que pueden perderse o ser atacados con más facilidad.

### 5. ¿Por qué una copia utilizada para desarrollo también puede representar un riesgo de privacidad?

Porque, aunque esté en un servidor interno, sigue conteniendo datos personales reales. Si ese entorno se filtra, la empresa tiene la misma responsabilidad legal y operativa que si se hubiera vulnerado producción.

### 6. ¿Por qué la retención debe formar parte del ciclo de vida de los datos?

Porque los datos no deben permanecer para siempre en el sistema. Con una etapa de retención, la información pasa de estar activa a archivarse o borrarse de forma definitiva, lo que reduce costos de almacenamiento y riesgos legales.

### 7. ¿Qué relación existe entre privacidad por diseño y diseño de bases de datos?

La privacidad debe influir desde que se crean las tablas, las relaciones y los esquemas. Esto significa separar los campos sensibles, definir permisos por columna o por vista, y agregar desde el inicio campos que controlen fechas de caducidad o el estado del consentimiento.

### 8. ¿Qué controles técnicos implementarías para reducir el riesgo de exposición de datos personales?

- Enmascarar los datos en pantalla para los roles de soporte.
- Crear vistas anonimizadas para reportes y analítica.
- Cifrar en reposo las columnas sensibles.
- Usar datos sintéticos (ficticios) en las pruebas de desarrollo.
- Activar bitácoras de auditoría que no se puedan alterar.

### 9. ¿Qué información debería conocer un DBA para responder técnicamente a una solicitud ARCO?

Debe saber en qué tablas, vistas, réplicas y respaldos aparece el identificador o los datos de la persona, qué llaves foráneas y dependencias tiene asociadas, y qué procedimiento aplicar (borrado directo o anonimización) sin dañar la base de datos.

### 10. ¿Qué responsabilidades deberían corresponder al DBA, al responsable de privacidad, al área jurídica y al propietario de los datos?

- **DBA:** configurar la seguridad, las vistas y los respaldos, y ejecutar los scripts de depuración.
- **Responsable de Privacidad:** supervisar el cumplimiento normativo, atender las solicitudes ARCO y mantener actualizados los avisos de privacidad.
- **Área Jurídica:** definir el marco legal de retención y respaldar a la empresa ante auditorías o litigios.
- **Propietario de los datos (Negocio):** justificar por qué se necesita cada dato y autorizar qué roles pueden consultarlo.
