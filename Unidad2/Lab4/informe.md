# Informe — LAB-04 Hardening y configuración segura de PostgreSQL

Alumna: Susana Valentina Vega García · Grupo 4-4 · Facultad de Informática Culiacán, UAS

**1. ¿Cuál era la principal superficie de ataque?**
El servicio PostgreSQL expuesto en el puerto 5432, escuchando en todas las interfaces (`listen_addresses = *`), alcanzable de forma remota y sin TLS. Es el punto por el que llegan las conexiones y, por lo tanto, los intentos de acceso.

**2. ¿Qué configuración representaba el mayor riesgo?**
`listen_addresses = *` combinado con `ssl = off`: el servidor acepta conexiones por cualquier interfaz y el tráfico viaja sin cifrar. Como riesgo de privilegios, destaca que 82 roles tienen `CREATEROLE`.

**3. ¿Qué cambio produjo la mayor reducción de exposición?**
En este laboratorio no se aplicó ningún cambio (la cuenta de alumno es de solo revisión). El cambio propuesto con mayor efecto es restringir el origen del acceso: `listen_addresses` a la interfaz privada y una regla específica en `pg_hba.conf` (base + usuario + red + `scram-sha-256`), apoyada por el firewall.

**4. ¿Qué diferencia existe entre firewall y `pg_hba.conf`?**
El firewall filtra por IP y puerto antes de que el tráfico llegue a PostgreSQL. `pg_hba.conf` actúa dentro del servicio y decide por base de datos, usuario, origen y método de autenticación. Son capas distintas y complementarias: si una falla, la otra sigue limitando.

**5. ¿Qué diferencia existe entre autenticación y autorización?**
La autenticación verifica quién eres (usuario y contraseña). La autorización define qué puedes hacer una vez dentro (permisos sobre bases, tablas y operaciones).

**6. ¿Por qué una cuenta de aplicación no debe ser `SUPERUSER`?**
Porque un superusuario se salta todos los permisos. Si la aplicación tiene una vulnerabilidad (por ejemplo, inyección SQL) o se roban sus credenciales, el atacante controla todo el servidor: lee y borra cualquier base, crea roles y puede afectar al sistema operativo.

**7. ¿Por qué cambiar el puerto de PostgreSQL no constituye hardening suficiente?**
Porque es seguridad por oscuridad: un escaneo de puertos encuentra el servicio en cualquier puerto. No resuelve la autenticación, los privilegios excesivos, la falta de TLS ni las reglas de acceso amplias. Solo dificulta ligeramente el descubrimiento.

**8. ¿Por qué `listen_addresses = '*'` puede ser innecesario?**
Porque hace que el servidor acepte conexiones por todas sus interfaces, aunque normalmente solo se necesita una (la de la red privada o la de la aplicación). Cada interfaz extra aumenta la superficie de ataque sin aportar nada.

**9. ¿Qué papel tiene el sistema operativo en la seguridad de PostgreSQL?**
Protege lo que PostgreSQL no controla: los archivos de configuración, el directorio de datos, los logs y los usuarios del sistema. Si cualquiera puede leer esos archivos, se salta la autenticación y los permisos de la base. También incluyen actualizaciones, firewall y control de acceso al servidor (por ejemplo, SSH).

**10. ¿Qué controles deberían revisarse periódicamente?**
Interfaces de escucha y puerto; reglas de `pg_hba.conf`; roles, privilegios y cuentas sin uso; superusuarios; extensiones instaladas; configuración de TLS y vigencia de certificados; parámetros de conexión y timeouts; permisos de archivos y directorio de datos; reglas de firewall; logs de conexiones; y que PostgreSQL y el sistema operativo estén actualizados.
