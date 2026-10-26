# Privacidad desde el diseño

**Escenario:** una nueva aplicación requiere registrar clientes. El desarrollador propone una tabla `clientes` con id, nombre, correo, telefono, rfc, edad, direccion, ciudad, codigo_postal, fecha_nacimiento, ocupacion, salario, estado_civil y más campos, bajo la justificación: "Es mejor guardar todos los datos por si posteriormente necesitamos alguno."

## 1. ¿Qué problemas identificas?

- **Se recolecta más de lo necesario:** campos como salario, estado civil u ocupación no tienen una finalidad clara para registrar a un cliente.
- **Datos duplicados o redundantes:** `edad` y `fecha_nacimiento` guardan casi lo mismo, y la edad se queda desactualizada con el tiempo.
- **Todo en una sola tabla:** cualquier persona con acceso a la tabla puede ver todos los datos, sin separar por función.
- **Mayor impacto ante una fuga:** si la tabla se filtra, se expone información financiera y personal muy delicada, no solo datos de contacto.
- **Sin finalidad ni plazo definidos:** no se sabe para qué se usa cada dato ni cuándo se eliminará.
- **Tipos de dato sin control:** todo es `TEXT`, sin validaciones ni restricciones, lo que facilita errores y datos incorrectos.
- **Falta de protección en el diseño:** no se contempla cifrado, enmascarado ni separación de datos sensibles.
- **El argumento es una suposición:** "por si acaso" no es una necesidad real y no justifica pedirle datos a una persona.

## 2. ¿Qué principio de privacidad se está ignorando?

El principio de **minimización de datos**: solo debe recolectarse lo adecuado, pertinente y necesario para una finalidad específica. También se ignoran la **limitación de la finalidad** (no hay un propósito claro para cada campo) y la **privacidad desde el diseño y por defecto**, que exige pensar en la protección antes de construir el sistema.

## 3. ¿Qué preguntas realizaría antes de aprobar el diseño?

- ¿Para qué se va a usar exactamente cada campo?
- ¿Qué función del servicio dejaría de funcionar si se quita este dato?
- ¿Qué área o rol necesita verlo?
- ¿Se informó al cliente en el aviso de privacidad que se recolectará?
- ¿Hay una obligación legal que lo requiera?
- ¿Se puede lograr lo mismo con un dato menos sensible, un rango o un dato anónimo?
- ¿Por cuánto tiempo se conservará y cómo se eliminará?
- ¿Qué pasaría si este dato se filtrara?

## 4. ¿Qué datos eliminaría?

- **salario:** no es necesario para registrar ni atender a un cliente, y es muy sensible.
- **estado_civil:** no tiene relación con el servicio.
- **ocupacion:** no es necesaria para la operación básica.
- **edad:** es redundante si se guarda la fecha de nacimiento, y se desactualiza; si solo se necesita para saber si es mayor de edad, basta un dato de confirmación.
- **direccion:** se elimina del registro general si el servicio no incluye entregas a domicilio.

## 5. ¿Qué datos requerirían una justificación adicional?

- **rfc:** solo se justifica si el cliente va a pedir factura; podría pedirse hasta ese momento y no desde el registro.
- **fecha_nacimiento:** necesita una razón clara, como validar mayoría de edad o aplicar una promoción por cumpleaños.
- **direccion:** se justifica solo si hay envíos o servicios en domicilio.
- **telefono:** necesario solo si el soporte o el servicio se da por ese medio.
- **codigo_postal y ciudad:** se justifican si se usan para logística o estadísticas de zona.

## 6. ¿Cómo aplicaría privacidad por defecto?

- Pedir en el registro únicamente nombre y correo, que son lo mínimo para dar el servicio.
- Dejar los demás datos como opcionales, y solicitarlos hasta que realmente se necesiten.
- Poner en "no" por defecto cualquier permiso extra, como recibir publicidad o compartir datos con terceros.
- Separar los datos sensibles o de uso ocasional (como RFC o dirección) en otra tabla con acceso más restringido.
- Dar acceso por rol, de modo que cada área vea solo lo que necesita.
- Cifrar los datos sensibles y enmascarar los que se muestren en reportes.
- Definir desde el inicio el plazo de conservación y la forma de eliminar o anonimizar al terminar.
- Revisar periódicamente qué campos se usan y retirar los que no.
