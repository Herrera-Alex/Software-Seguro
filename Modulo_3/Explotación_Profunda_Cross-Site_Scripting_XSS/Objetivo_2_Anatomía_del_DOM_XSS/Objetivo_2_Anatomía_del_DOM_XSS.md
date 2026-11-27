El **DOM-Based XSS** es indetectable para la mayoría de los WAF e IPS porque el payload malicioso nunca se envía al servidor a través de la red; todo el ciclo de ataque (inyección y ejecución) ocurre exclusivamente dentro del navegador de la víctima (client-side).



**1.El rol del identificador de fragmento (#) en la URL**

Por estándar de protocolos web (RFC 3986), todo lo que aparece después del símbolo de numeral (#) en una URL se denomina identificador de fragmento (por ejemplo: https://ejemplo.com<img src=x onerror=alert(1)>).

* **Comportamiento del navegador:** El navegador utiliza este fragmento exclusivamente de manera local (originalmente para desplazarse a una sección específica de la página). Cuando el navegador realiza una petición HTTP/HTTPS al servidor, recorta automáticamente el # y todo su contenido.
* **Ceguera de los WAF e IPS:** Los sistemas perimetrales como WAF (Web Application Firewalls) e IPS (Sistemas de Prevención de Intrusos) analizan el tráfico HTTP que viaja desde el cliente hacia el servidor. Como el payload viaja dentro del fragmento #, nunca llega a cruzar la red ni aparece en las cabeceras, parámetros GET/POST o registros (logs) del servidor. Para el WAF, la petición luce completamente limpia y legítima (GET /perfil HTTP/1.1).



**2.¿Qué sucede cuando JavaScript procesa location.hash de forma insegura?**

Aunque el servidor nunca recibe el código malicioso, el ataque se concreta gracias al propio código JavaScript legítimo que la página descargó previamente:

* **La Fuente (Source):** El código JavaScript del lado del cliente lee datos controlados por el usuario directamente desde la URL usando propiedades del DOM como location.hash (o document.URL, location.href).
* **El Sumidero (Sink):** Si la aplicación toma ese valor leído de location.hash y, sin sanitizarlo ni codificarlo, lo pasa a una función peligrosa que modifica la estructura HTML de la página —como element.innerHTML, document.write() o eval()— se produce la vulnerabilidad.
* **La Ejecución:** El motor del navegador interpreta la cadena inyectada como código HTML/JavaScript activo y modifica el DOM en tiempo real, ejecutando el payload del atacante con los permisos de la sesión de la víctima, sin haber tocado jamás el servidor ni las defensas perimetrales.



