**1. ¿Qué protege exactamente la bandera HttpOnly?**

La bandera HttpOnly protege el contenido de la cookie contra el acceso mediante scripts del lado del cliente, como JavaScript (por ejemplo, a través de document.cookie).

* **Objetivo principal:** Mitigar el impacto de los ataques Cross-Site Scripting (XSS). Si un atacante logra inyectar código JavaScript malicioso en un sitio web, no podrá leer ni robar la cookie de sesión para suplantar la identidad del usuario.



**2. ¿Qué riesgo corre el usuario si no tiene la bandera Secure activada?**

Si una cookie de sesión carece de la bandera Secure, el navegador permite que sea enviada a través de conexiones sin cifrar (HTTP).

* **Riesgo principal:** El usuario queda expuesto a ataques de tipo Man-in-the-Middle (MitM) o intercepción de tráfico (sniffing) en redes inseguras (como un Wi-Fi público). Un atacante en la misma red puede capturar la cookie en texto plano y realizar un secuestro de sesión (Session Hijacking) para acceder a la cuenta de la víctima sin necesidad de su contraseña.



A continuación tenemos 3 sitios web que analize y puse aprueba sus banderas como el HttpOnly no las tienen habilitadas por el cual pude ver mis cookies y la de Secure si están bien:

Foto 1

Foto 2

Foto 3 

&#x20;

