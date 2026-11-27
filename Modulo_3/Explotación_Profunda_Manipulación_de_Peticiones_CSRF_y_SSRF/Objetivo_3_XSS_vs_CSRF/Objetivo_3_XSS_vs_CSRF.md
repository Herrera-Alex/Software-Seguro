La diferencia fundamental entre ambos ataques radica en la dirección de la confianza vulnerada: el **XSS (Cross-Site Scripting)** explota la confianza que el usuario tiene en un sitio web legítimo (ejecutando código malicioso dentro del origen confiable), mientras que el **CSRF (Cross-Site Request Forgery)** explota la confianza que un sitio web legítimo tiene en el navegador del usuario (forzando peticiones no autorizadas desde un origen externo).



**Comparación Técnica: XSS vs. CSRF**

**Cross-Site Scripting (XSS):**

* **Dirección de la confianza:**Usuario → Sitio Web: La víctima confía en que el contenido servido por la aplicación legítima es seguro.
* **Origen de ejecución:**Same-Origin (Mismo origen): El código JavaScript del atacante se ejecuta dentro del contexto y dominio de la aplicación vulnerable.
* **Inyección de código:**Sí requiere inyectar código (JavaScript/HTML) en la aplicación vulnerable.
* **Capacidad de lectura:**Bidireccional (Lectura y Escritura): Puede leer respuestas del servidor, extraer datos del DOM, robar tokens/cookies y realizar acciones.
* **Alcance del impacto:**Total: Puede leer información confidencial, suplantar la sesión completa, alterar la interfaz y evadir cualquier defensa anti-CSRF.
* **Mitigación principal:**Context-Aware Output Encoding (codificación de salida) + Content Security Policy (CSP).



**Cross-Site Request Forgery (CSRF):**

* **Dirección de la confianza:**Sitio Web → Navegador: La aplicación confía ciegamente en cualquier petición que incluya las cookies de sesión del usuario.
* **Origen de ejecución:**Cross-Origin (Origen cruzado): La petición se dispara desde un sitio web externo controlado por el atacante hacia la aplicación legítima.
* **Inyección de código:**No requiere inyectar código en la aplicación objetivo; solo envía peticiones HTTP válidas.
* **Capacidad de lectura:**Unidireccional (Solo Escritura / Acción): El atacante envía la orden ("a ciegas"), pero la Same-Origin Policy (SOP) le impide leer la respuesta del servidor.
* **Alcance del impacto:**Limitado a acciones: Solo puede ejecutar funciones específicas que cambian de estado (ej. transferir dinero, cambiar contraseña o correo).
* **Mitigación principal:**Tokens Anti-CSRF impredecibles + atributo de cookie SameSite=Strict / Lax.



