Una **Consulta Parametrizada (Prepared Statement)** neutraliza la inyección SQL porque separa estrictamente la estructura del código SQL de los datos proporcionados por el usuario, enviándolos al motor de base de datos en dos fases distintas.



**1.¿Cómo funciona a nivel de arquitectura?**

En una consulta vulnerable tradicional, la aplicación concatena texto (código + entrada del usuario) y envía todo junto al motor de base de datos para que lo interprete. En cambio, un Prepared Statement divide la comunicación entre la aplicación y el gestor de base de datos (DBMS) en dos pasos:



**Fase 1: Preparación y Compilación (El molde):**

* La aplicación envía únicamente la plantilla de la consulta SQL al motor de base de datos, usando marcadores de posición (placeholders como ? o :usuario) en lugar de los valores reales. Ejemplo: SELECT \* FROM usuarios WHERE username = ? AND password = ?
* El motor de base de datos analiza sintácticamente (parsea), compila y optimiza esta estructura, generando un plan de ejecución fijo en memoria. En este punto, la lógica de la consulta ya está cerrada y definida.



**Fase 2: Vinculación de Parámetros y Ejecución (Binding):**

* La aplicación envía los datos introducidos por el usuario por un canal separado para rellenar esos marcadores de posición.
* El motor de base de datos inserta esos valores directamente en el plan de ejecución ya compilado, sin volver a pasar por el analizador sintáctico (parser) de SQL.



**2.¿Por qué neutraliza por completo cualquier intento de inyección?**



* **Tratamiento estricto como dato literal:** Como el plan de ejecución ya fue compilado antes de recibir la entrada del usuario, el motor de base de datos trata cualquier contenido recibido en la Fase 2 exclusivamente como un valor literal (una cadena de texto o un número), nunca como instrucciones ejecutables.
* **Inmunidad ante caracteres especiales:** Si un atacante envía admin' OR '1'='1, la base de datos no interpreta la comilla simple (') como el cierre de una cadena ni el OR como un operador lógico. Simplemente busca en la columna username a un usuario cuyo nombre literal sea exactamente la cadena de texto "admin' OR '1'='1".
* **No depende de filtros o listas negras:** A diferencia de bloquear palabras (SELECT, UNION) o escapar comillas —que siempre pueden evadirse mediante codificaciones, comentarios o funciones alternativas—, la parametrización elimina la raíz del problema: el intérprete SQL jamás llega a leer la entrada del usuario como código.



