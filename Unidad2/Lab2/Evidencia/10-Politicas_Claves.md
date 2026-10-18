# Política para la gestión de claves criptográficas

1. **Generación:** Las llaves se deben crear con métodos criptográficos sólidos y herramientas confiables que garanticen que sean realmente aleatorias.
2. **Almacenamiento:** Las llaves y credenciales se guardan en lugares protegidos, separados del código fuente y de los archivos de la base de datos.
3. **Acceso:** Solo puede consultarlas y usarlas el personal que tenga autorización.
4. **Rotación:** Hay que cambiar las llaves cada cierto tiempo, y de inmediato si hay sospecha de que fueron vulneradas.
5. **Respaldo:** Se deben guardar copias de seguridad protegidas para no perder de forma definitiva las llaves importantes.
6. **Revocación:** Toda llave que ya no esté vigente o que represente un riesgo se debe desactivar para que no se siga usando.
7. **Exposición accidental:** Si una llave se filtra, se considera comprometida por completo y se debe reemplazar de inmediato.
8. **Eliminación:** Cuando una llave termina su ciclo de vida, se borra de forma definitiva con métodos seguros que impidan recuperarla.
