Eliminar únicamente las etiquetas <script> y </script> es una defensa inútil porque los navegadores modernos permiten ejecutar código JavaScript a través de múltiples vectores alternativos del estándar HTML5, como manejadores de eventos (event handlers) y atributos especiales en otras etiquetas, sin necesidad de abrir un bloque <script>.



**1.¿Por qué esta defensa es técnicamente inútil?**

* **Ejecución basada en eventos del DOM:** El estándar HTML permite asociar código JavaScript directamente a eventos de interacción o estado de casi cualquier elemento visual (por ejemplo, cuando una imagen falla al cargar, cuando el usuario pasa el cursor por encima o cuando se enfoca un campo). El motor de renderizado del navegador interpreta y ejecuta el contenido de estos atributos como JavaScript puro.
* **Soporte de pseudo-protocolos (javascript:):** Ciertos atributos diseñados para recibir direcciones URL (como href en enlaces o src en marcos) aceptan el esquema javascript:, lo que instruye al navegador a ejecutar el código que sigue en lugar de navegar a una página externa.
* **Fallas en la lógica de sanitización (listas negras):** Bloquear palabras específicas (blacklisting) siempre deja puertas abiertas. Además de otras etiquetas, muchos filtros simples son sensibles a mayúsculas/minúsculas (<ScRiPt>) o no son recursivos (si el filtro borra <script> una sola vez, una entrada como <scr<script>ipt> se reconstruye como <script> tras pasar por el filtro).



**2.Ejemplos de payloads que evaden el filtro (sin usar <script>)**



* **Payload 1:** Abuso del evento onerror en una etiqueta de imagen (<img>)

&#x09;**<img src="imagen\_inexistente.jpg" onerror="alert('XSS ejecutado')">**

&#x09;**Cómo funciona:** El navegador intenta cargar la imagen desde una ruta falsa 	(src="imagen\_inexistente.jpg"). Al fallar inmediatamente la carga, se 	dispara automáticamente el evento onerror, ejecutando el código 

&#x09;JavaScript sin requerir ninguna interacción de la víctima.



* **Payload 2:** Abuso del evento onload en una etiqueta vectorial (<svg>)

&#x09;**<svg onload="alert(document.cookie)">**

&#x09;**Cómo funciona:** La etiqueta <svg> (Gráficos Vectoriales Escalables) forma 	parte del estándar HTML5 y soporta sus propios eventos de ciclo de vida. 	En cuanto el navegador dibuja el elemento SVG en la página, dispara el 	evento onload y ejecuta el payload de forma silenciosa y automática.





