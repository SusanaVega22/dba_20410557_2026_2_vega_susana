# Linea base de seguridad - PostgreSQL 16

Propuesta de baseline (Actividad 19). El servidor revisado en el laboratorio es PostgreSQL 15.19; los controles aplican igual a la 16.

## Red
- Interfaces autorizadas: solo la interfaz privada del servidor, no `*`.
- Puerto: 5432 documentado (o uno distinto justificado).
- Firewall: permitir 5432 solo desde las redes autorizadas; denegar el resto.
- Redes permitidas: rangos concretos (por ejemplo la red del laboratorio o de DBA), nunca `0.0.0.0/0` ni `::/0`.

## Autenticacion
- Metodo: `scram-sha-256` (evitar `md5` y `trust`).
- Politica de credenciales: contrasenas largas y unicas, rotacion periodica, sin contrasenas compartidas.
- Cuentas administrativas: pocas, nominales, uso restringido y auditado.

## Autorizacion
- Roles: separar DBA, APP y CONSULTA.
- Privilegios: minimos necesarios; sin `SUPERUSER`, `CREATEROLE` ni `CREATEDB` en cuentas de aplicacion o de alumno.
- Cuentas de aplicacion: una por aplicacion, solo con los permisos que usa.

## Configuracion
- `log_connections` y `log_disconnections` en `on`.
- `statement_timeout` e `idle_in_transaction_session_timeout` con valores definidos.
- `max_connections` acorde a la carga y `superuser_reserved_connections` mayor que 0.
- Extensiones: solo las necesarias (`pgcrypto` solo si algo la usa).

## Sistema operativo
- Archivos de configuracion y directorio de datos con propietario `postgres`.
- Directorio de datos con modo `700`; `postgresql.conf` y `pg_hba.conf` sin lectura para otros.
- Acceso al servidor por SSH restringido.

## Cifrado
- TLS habilitado (`ssl = on`), version minima TLS 1.2, reglas `hostssl`.
- Clientes con `sslmode=verify-full`.
- Credenciales no guardadas en texto plano; datos sensibles cifrados o protegidos.

## Mantenimiento
- Aplicar actualizaciones menores de PostgreSQL y del sistema.
- Revision periodica de roles, `pg_hba.conf` y logs.
- Documentar cada cambio en `cambios.md`.
