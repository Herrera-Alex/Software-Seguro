**1.Diferencia principal entre un "mensaje de error genérico" y un "Stack Trace" (traza de la pila):**

mientras que un mensaje de error genérico oculta los detalles técnicos, un Stack Trace expone la estructura interna del código y del servidor.



**2.¿Por qué un Stack Trace facilita la explotación a un atacante?**

Dejar el modo de depuración (debug) activo en producción convierte un simple error en una guía detallada para un atacante (vulnerabilidad conocida en OWASP como Improper Error Handling o Information Exposure):



* **Mapeo de la arquitectura interna:** Revela rutas exactas del sistema operativo (ej. /var/www/app/controllers/AuthController.php), permitiendo saber si el servidor corre sobre Linux o Windows y cómo están organizadas las carpetas.
* **Identificación de tecnologías y versiones:** Muestra qué lenguaje, framework (Laravel, Django, Spring, .NET) y gestor de base de datos se usan, junto con sus versiones exactas. Con esto, el atacante puede buscar vulnerabilidades públicas conocidas (CVE) específicas para esa versión.
* **Exposición de lógica y consultas (SQL):** Si el error ocurre en la base de datos, el Stack Trace suele imprimir la consulta SQL completa que falló. Esto permite al atacante ver nombres de tablas, columnas y confirmar exactamente cómo inyectar código malicioso (SQL Injection).
* **Fuga de credenciales y variables:** En algunos frameworks, la traza de error vuelca el estado de las variables en memoria en el momento del fallo, lo que puede incluir contraseñas, tokens de sesión o claves de API en texto plano.
* **Ahorro de tiempo en reconocimiento:** Elimina la necesidad de que el atacante tenga que adivinar cómo funciona la aplicación mediante prueba y error, acelerando el paso de la fase de reconocimiento a la explotación directa.



