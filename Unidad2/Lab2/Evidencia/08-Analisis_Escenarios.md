# Analizar un escenario de seguridad

1. **¿Cuáles son los principales riesgos?**
   Casi todos los puntos débiles están presentes. La información confidencial queda totalmente expuesta y cualquier atacante o persona sin autorización puede acceder a ella.

2. **¿Qué mecanismo utilizarías para cada elemento?**
   - **Nombre y correo:** Control de acceso por roles, con permisos estrictos.
   - **Contraseña:** Hash seguro con algoritmos robustos como bcrypt o Argon2.
   - **RFC:** Cifrado simétrico a nivel de columna.
   - **Información financiera:** Cifrado de los datos y políticas de acceso estrictas.
   - **Claves criptográficas:** Un gestor de secretos externo.
   - **Conexiones:** TLS, validando por completo el certificado del servidor.
   - **Respaldos:** Cifrar las copias y guardarlas en un lugar con acceso restringido.

3. **¿Cuál de los problemas consideras más crítico y por qué?**
   Guardar las contraseñas en texto claro. Si alguien vulnera el sistema o saca la tabla, obtiene todas las contraseñas de inmediato y puede entrar a las cuentas de los usuarios.

4. **¿Tener correctamente configurados los usuarios y permisos elimina estos riesgos?**
   Solo en parte. Los permisos no resuelven la falta de cifrado en reposo, ni protegen si alguien extrae los datos directamente del almacenamiento, ni si las llaves criptográficas se manejan mal.
