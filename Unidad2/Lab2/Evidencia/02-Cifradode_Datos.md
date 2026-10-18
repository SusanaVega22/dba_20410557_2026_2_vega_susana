# Cifrado de información sensible

1. **¿Qué diferencia existe entre `crypt()` y `pgp_sym_encrypt()`?**
   `crypt()` genera un hash de un solo sentido y se usa para guardar contraseñas, porque ese dato no se necesita recuperar. En cambio, `pgp_sym_encrypt()` hace un cifrado simétrico que va en dos sentidos: protege el dato y después se puede descifrar cuando se necesite.

2. **¿Cuál de los dos mecanismos permite recuperar el dato original?**
   `pgp_sym_encrypt()`, porque con la llave secreta correcta se puede deshacer el cifrado y obtener el dato original.

3. **¿Qué ocurre si se utiliza una clave incorrecta?**
   Marca un error al intentar descifrar, ya que la clave no es la misma que se usó para cifrar el contenido.

4. **¿Qué problema de seguridad representa colocar la clave directamente en una consulta?**
   La clave queda a la vista de cualquiera que pueda revisar el historial de la base de datos, las auditorías o los logs de transacciones. Con eso, la protección del dato cifrado deja de servir.
