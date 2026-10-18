# Resumen de mecanismos de seguridad

| Situación | Mecanismo apropiado | ¿Qué protege? |
|---|---|---|
| Contraseña de usuario | Hash (`crypt()`) | Evita guardar las contraseñas en un formato que se pueda leer |
| RFC almacenado en una tabla | Cifrado simétrico | Protege el dato fiscal y permite descifrarlo después cuando se necesite |
| Consulta enviada desde un cliente al servidor | TLS | Protege la información mientras viaja por la red |
| Respaldo de una base de datos | Cifrado de respaldos | Impide que alguien sin autorización pueda ver el contenido de las copias |
| Clave criptográfica | Gestor de secretos | Evita que las llaves se filtren o se usen de forma indebida |
