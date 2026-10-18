# Protección de datos durante la comunicación

1. **¿La conexión actual utiliza TLS?**
   Depende del valor que regrese la columna `ssl` en la consulta. Si es verdadero, la sesión está protegida con TLS; si es falso, la comunicación va en texto plano.

2. **¿Qué versión de TLS se está utilizando?**
   La que aparece en la columna `version` del resultado.

3. **¿Qué algoritmo de cifrado aparece?**
   El que se muestra en la columna `cipher`, que indica el conjunto de algoritmos criptográficos usados en la conexión.

4. **¿Qué diferencia existe entre una conexión protegida con TLS y una sin TLS?**
   Con TLS, la información que viaja por la red va cifrada, así que nadie puede interceptarla ni leerla en el camino. Sin TLS, los datos viajan completamente legibles y cualquiera que espíe la red puede verlos.
