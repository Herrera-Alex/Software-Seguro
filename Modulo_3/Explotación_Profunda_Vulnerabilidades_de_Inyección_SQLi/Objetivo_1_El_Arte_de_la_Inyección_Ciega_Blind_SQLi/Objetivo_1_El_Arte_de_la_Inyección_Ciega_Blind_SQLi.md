**1.Diferencia técnica: Boolean-Based vs. Time-Based Blind SQLi**

Ambas técnicas pertenecen a la categoría de Inyección SQL a ciegas (Blind SQL Injection), donde la base de datos no devuelve datos ni mensajes de error directamente, por lo que el atacante debe hacer preguntas de tipo "sí o no".



**Boolean-Based Blind (Basada en booleanos):**

* **Mecanismo de inferencia:** Se inyecta una condición lógica (VERDADERO o FALSO).
* **Indicador de éxito:** La aplicación cambia ligeramente su contenido o comportamiento (ej. muestra un artículo si es verdadero, o página en blanco si es falso).
* **Cuándo se usa:** Cuando la página reacciona de forma distinta ante consultas válidas e inválidas, aunque no muestre datos.



**Time-Based Blind (Basada en tiempo):**

* **Mecanismo de inferencia:** Se inyecta una función de pausa (ej. SLEEP(), WAITFOR DELAY).
* **Indicador de éxito:** La aplicación tarda un tiempo específico en responder (ej. 5 segundos) si la condición es verdadera, o responde al instante si es falsa.
* **Cuándo se usa:** Cuando la página siempre muestra exactamente lo mismo (como una pantalla genérica de "Cargando..." o un mensaje estándar).



**2.¿Cómo extrae el atacante el nombre de la base de datos letra por letra?**

Cuando la aplicación solo devuelve una pantalla genérica de "Cargando...", el atacante no puede guiarse por cambios visuales; por lo tanto, utiliza obligatoriamente la técnica Time-Based Blind convirtiendo el tiempo de espera en un código binario (responde rápido = Falso / tarda X segundos = Verdadero).

* **Averiguar la longitud del nombre:** El atacante pregunta cuántos caracteres tiene el nombre de la base de datos enviando consultas condicionales con una pausa.
* **Adivinar carácter por carácter (usando SUBSTRING y valores ASCII):** Una vez que sabe cuántas letras tiene, aísla cada posición una por una y la compara con el abecedario o códigos ASCII.
* **Automatización y reconstrucción:1.** El atacante repite este proceso para la segunda posición, la tercera, y así sucesivamente hasta completar toda la palabra (ej. t-i-e-n-d-a). Debido a la gran cantidad de peticiones necesarias, esto suele automatizarse con scripts o herramientas como sqlmap.

