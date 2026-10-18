# Informe del Laboratorio 1

## 19.1 Clasificación

Se deben proteger los datos personales, confidenciales o financieros, por ejemplo: nombre completo, RFC, correo electrónico y datos bancarios. Si se filtran o se usan sin permiso, se afecta la privacidad de las personas, se facilita el robo de identidad y se pueden violar las leyes de protección de datos.

## 19.2 Enmascaramiento

- **Qué se ocultó:** Parte de los datos sensibles o todos ellos, como los números de una tarjeta o pedazos de una contraseña.
- **Para quién:** Para los usuarios o roles que en su trabajo diario no necesitan ver el dato completo.
- **Por qué:** Para que la información crítica no quede a la vista de cualquiera en pantallas o reportes.
- **Qué mecanismo se utilizó:** Cortar el dato o cambiar sus caracteres por símbolos como asteriscos (*).

## 19.3 Seudonimización

- **Cómo se generaron los tokens:** Con funciones hash o con identificadores únicos aleatorios que se ponen en lugar de los datos que identifican a la persona.
- **Dónde se encuentra el mapa de correspondencia:** En una tabla o base de datos aparte, con acceso muy restringido y separada de los datos de operación.
- **Quién debería poder acceder a él:** Solo personal administrativo con privilegios altos y bien justificados.
- **Por qué se separaron los permisos:** Para que quien tenga acceso a los datos seudonimizados no pueda ligarlos fácilmente con la identidad real de las personas.

## 19.4 Anonimización

- **Qué identificadores fueron eliminados:** Nombres, teléfonos, correos y cualquier otro dato de contacto directo.
- **Qué atributos fueron generalizados:** La edad se cambió por rangos y la ubicación por zonas amplias, en vez de usar fechas exactas o lugares precisos.
- **Qué grupos fueron suprimidos:** Los registros con características muy únicas, porque con ellos se podría identificar a una persona en particular.
- **Qué riesgo de reidentificación permanece:** Que alguien cruce los datos con otras fuentes externas o use los cuasi-identificadores que quedaron para deducir quién es la persona.

## 19.5 Retención

- **Qué criterio se utilizó:** Guardar la información solo el tiempo necesario por razones de operación, contratos o leyes.
- **Qué información debería conservarse:** Los registros obligatorios para auditorías, impuestos o transacciones que siguen vigentes.
- **Qué información podría eliminarse:** Datos que ya no sirven, registros temporales y datos de usuarios inactivos cuyo plazo legal ya venció.
- **Qué controles deberían existir antes de eliminarla:** Autorización formal, respaldos seguros y comprobar que ningún proceso activo todavía dependa de esos registros.

## 19.6 Conclusiones

- **¿Qué técnica utilizarías para un área de soporte?**
  Enmascaramiento, porque así pueden reconocer al cliente a simple vista sin ver sus datos completos ni sensibles.
- **¿Qué técnica utilizarías para un área de analítica?**
  Seudonimización, porque permite analizar el comportamiento de los usuarios sin exponer quiénes son en realidad.
- **¿Qué técnica utilizarías para publicar estadísticas?**
  Anonimización completa, para que nadie pueda ser identificado ni rastreado.
- **¿Por qué ninguna de estas técnicas sustituye al control de acceso?**
  Porque solo cambian cómo se ve el dato o qué tanto se puede usar, pero no deciden quién puede entrar al sistema ni validan su identidad.

---

## 20. Preguntas de reflexión

**1. ¿Cuál es la diferencia entre enmascaramiento y seudonimización?**
El enmascaramiento solo esconde una parte del dato al mostrarlo en pantalla. La seudonimización cambia el identificador por un token único, y la relación entre ambos queda guardada en un mapa aparte.

**2. ¿Por qué la seudonimización no significa anonimización?**
Porque con el mapa o llave de correspondencia se puede volver a la identidad real, es decir, el proceso es reversible. En los datos anónimos eso no se puede hacer.

**3. ¿Por qué eliminar nombre y RFC no garantiza que un conjunto de datos sea anónimo?**
Porque los demás datos que quedan (cuasi-identificadores) se pueden combinar con bases públicas y así descubrir quién es la persona.

**4. ¿Qué función tienen los cuasi-identificadores?**
Son datos que solos no identifican a nadie, pero juntos (por ejemplo, edad, colonia y profesión) hacen mucho más fácil reidentificar a una persona.

**5. ¿Por qué es importante separar el mapa de seudonimización?**
Para que, si roban o filtran el almacenamiento principal, no se pueda saber a quién pertenece cada token.

**6. ¿Qué principio de seguridad se aplica al impedir que el analista acceda al mapa?**
El principio de menor privilegio junto con la separación de funciones: cada quien solo accede a lo que necesita para su trabajo.

**7. ¿Por qué una vista puede ser preferible a entregar acceso directo a la tabla?**
Porque la vista puede ocultar columnas sensibles, enmascarar datos al momento de consultarlos y dar acceso controlado sin mostrar toda la estructura de la tabla original.

**8. ¿Qué diferencia existe entre proteger un dato para visualización y protegerlo contra acceso no autorizado?**
Proteger para visualización cambia cómo se ve el dato en pantalla o reportes. Proteger contra acceso no autorizado impide, mediante permisos en la base de datos, que alguien consulte, extraiga o modifique la información.

**9. ¿Por qué la retención forma parte de la protección de datos?**
Porque guardar datos que ya no se necesitan aumenta lo que un atacante puede robar y hace más grave el daño si hay una filtración.

**10. ¿Qué riesgo existe si una organización conserva información indefinidamente?**
Queda expuesta al robo masivo de datos históricos y puede incumplir las leyes de privacidad que limitan cuánto tiempo se puede guardar la información.
