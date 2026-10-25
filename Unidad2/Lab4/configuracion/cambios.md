# Cambios

## Cambios aplicados

Ninguno. El laboratorio es de revision y documentacion, y la cuenta de alumno no tiene permisos para modificar la configuracion del servidor.

## Cambios propuestos (no aplicados)

| # | Cambio propuesto | Motivo |
|---|---|---|
| 1 | `listen_addresses` = IP privada del servidor (en lugar de `*`) | Reducir interfaces expuestas |
| 2 | Regla en `pg_hba.conf`: `host db_20410557_susana_vega u_20410557_susana_vega 192.168.200.0/24 scram-sha-256` | Minimo privilegio: base + usuario + origen + metodo |
| 3 | `ssl = on` con certificado, `ssl_min_protocol_version = 'TLSv1.2'` y reglas `hostssl` | Cifrar el trafico |
| 4 | Quitar `CREATEROLE` a las cuentas de alumnos (`ALTER ROLE <rol> NOCREATEROLE;`) | 82 roles lo tienen sin necesitarlo |
| 5 | `statement_timeout` y `idle_in_transaction_session_timeout` con valores razonables | Hoy estan en 0 (sin limite) |
| 6 | Revisar los 43 roles sin login | Posibles cuentas innecesarias |
| 7 | Firewall: permitir 5432 solo desde la red autorizada | Defensa en capas |
