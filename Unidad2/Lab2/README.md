# Laboratorio de seguridad en bases de datos

## 1. Introducción

En este laboratorio se trabajaron los problemas de seguridad que aparecen cuando los datos sensibles quedan expuestos sin autorización, cuando las contraseñas se guardan en texto plano, cuando el tráfico de la red puede ser interceptado y cuando no hay reglas para administrar las llaves criptográficas en un sistema gestor de bases de datos.

## 2. Protección de credenciales

- **Texto claro:** Los datos se guardan sin ninguna protección, así que cualquiera con permiso de lectura puede ver las contraseñas directamente.
- **Hash:** Es un proceso de un solo sentido, que no se puede revertir. Convierte una entrada en una cadena de longitud fija y sirve para validar contraseñas sin guardarlas tal cual.
- **Cifrado:** Es un proceso de dos sentidos. Transforma los datos para que solo se puedan leer con una llave específica, la cual también sirve para descifrarlos después.

## 3. Protección de datos sensibles

El RFC se protegió con cifrado simétrico usando la extensión `pgcrypto`. Este tipo de dato personal debe mantenerse protegido mientras está guardado, para cumplir con las normas de privacidad, y a la vez las aplicaciones autorizadas pueden recuperar el valor original con la llave correspondiente.

## 4. TLS

TLS evita que los datos sean espiados o interceptados mientras viajan entre el cliente y el servidor. En PostgreSQL se revisó la sesión actual consultando las vistas del sistema, donde se comprobó el valor de `ssl`, la versión del protocolo en uso y el algoritmo de cifrado de la conexión.

## 5. Gestión de claves

Las llaves nunca deben guardarse dentro de los scripts de la base de datos ni en el código fuente. Si se hace, quedan al alcance de cualquier usuario o proceso que pueda ver el historial de consultas, los archivos de registro o los repositorios, y el cifrado deja de servir.

## 6. Resultados

- Se configuró el hash de contraseñas con sal usando `crypt` y `gen_salt`.
- Se cifraron y descifraron columnas específicas con `pgp_sym_encrypt` y `pgp_sym_decrypt`.
- Se comprobó que el servidor usa conexiones cifradas con TLS.
- Se definieron lineamientos para administrar los secretos de forma segura.

## 7. Problemas encontrados

Al probar las funciones criptográficas aparecieron errores de sintaxis porque el módulo `pgcrypto` no estaba habilitado en la base de datos de trabajo. Se solucionó ejecutando la sentencia `CREATE EXTENSION`.

## 8. Conclusiones

La seguridad en bases de datos necesita varias capas que se complementan: cifrado, control de acceso y conexiones seguras. En un entorno de producción usaría un gestor de secretos independiente, exigiría conexiones cifradas con TLS y aplicaría hashes robustos para autenticar a los usuarios.

---

## Preguntas de reflexión

**1. ¿Por qué una contraseña no debe almacenarse como texto claro?**
Porque si la base de datos o sus respaldos se filtran, las contraseñas quedan a la vista y los atacantes pueden usarlas directamente.

**2. ¿Por qué un hash no es equivalente a un cifrado?**
Porque el hash va en un solo sentido y no se puede revertir; sirve para validar datos. El cifrado va en dos sentidos y permite recuperar el texto original con la llave correcta.

**3. ¿Por qué el cifrado de una columna no sustituye al control de acceso?**
Porque el cifrado protege los datos si alguien extrae el almacenamiento, pero no decide qué usuarios dentro de la base de datos pueden consultar información o ejecutar acciones. Eso lo hace el control de acceso.

**4. ¿Por qué TLS no sustituye a los mecanismos de autorización de PostgreSQL?**
Porque TLS solo evita que los datos se lean o se modifiquen en la red. No maneja los permisos ni la identidad de los usuarios dentro del motor de la base de datos.

**5. ¿Qué ocurriría si una organización pierde una clave utilizada para cifrar información?**
Los datos cifrados con esa llave no se podrían recuperar nunca, y la información se perdería de forma definitiva.

**6. ¿Qué ocurriría si una clave criptográfica se publica accidentalmente en GitLab?**
Hay que considerarla comprometida de inmediato, porque cualquiera con acceso al repositorio podría usarla para descifrar la información que protege.

**7. ¿Por qué un repositorio privado no debe considerarse un almacén de secretos?**
Porque guarda todo el historial de cambios, se clona en muchos dispositivos y comparte permisos de lectura entre varias personas, lo que aumenta el riesgo de filtración.

**8. ¿Qué diferencia existe entre proteger información almacenada y proteger información durante su transmisión?**
Proteger la información almacenada evita que se lea en el disco o en la base de datos si hay una copia física o una filtración. Proteger la transmisión evita que alguien la intercepte o la lea mientras viaja por la red.

**9. ¿Por qué la gestión de claves es tan importante como el algoritmo criptográfico?**
Porque aunque el algoritmo sea muy fuerte, si la llave se expone, se roba o se guarda mal, la protección se rompe de inmediato.

**10. ¿Qué mecanismo adicional implementarías en una organización para proteger los respaldos de las bases de datos?**
Cifraría automáticamente los archivos de respaldo antes de enviarlos a otras ubicaciones y los guardaría en servidores aislados con control de acceso estricto.
