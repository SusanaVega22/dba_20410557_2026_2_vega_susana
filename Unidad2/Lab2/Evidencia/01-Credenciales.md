# Protección de credenciales

**¿Qué ocurriría si una persona obtiene acceso de lectura a esta tabla?**
Se perdería por completo la seguridad de las cuentas. Como las contraseñas están guardadas en texto claro, el atacante las puede leer directamente, hacerse pasar por los usuarios y robar su información personal.

---

## Generar una representación no reversible

1. **¿Son iguales?**
   No.

2. **Si no son iguales, ¿por qué?**
   Porque cada vez que se ejecuta la instrucción se genera un valor aleatorio distinto (la sal). Por eso el hash cambia aunque la contraseña sea la misma.

3. **¿Qué función cumple `gen_salt()`?**
   Crea una cadena aleatoria que se mezcla con la contraseña antes de procesarla. Así, dos contraseñas iguales no dan el mismo hash, y se evitan los ataques que usan tablas de hashes ya calculados.

4. **¿Qué función cumple `crypt()`?**
   Toma la contraseña en texto plano y la sal, y las procesa con el algoritmo elegido para producir un hash de un solo sentido.

5. **¿Esto es cifrado reversible?**
   No. Es hashing, una función de un solo sentido, y no hay manera de regresar del hash a la contraseña original.

---

## Verificar una contraseña

1. **¿Qué resultado obtuviste con la contraseña correcta?**
   Un resultado positivo (verdadero): al recalcular el hash, coincidió con el guardado.

2. **¿Qué resultado obtuviste con la contraseña incorrecta?**
   Un resultado negativo (falso): el hash calculado no coincidió, así que la contraseña es incorrecta.

3. **¿Por qué no es necesario recuperar la contraseña original?**
   Porque solo se necesita procesar la contraseña que escribe el usuario con la sal guardada en el registro y comparar el resultado con el hash almacenado. Si son iguales, la contraseña es correcta.

4. **¿Por qué un hash no debe confundirse con cifrado?**
   Porque el cifrado va en dos sentidos: con la clave adecuada se puede descifrar y recuperar el texto original. El hash solo va en un sentido y sirve para comprobar que un dato es auténtico o no ha cambiado, sin revelar el dato original.
