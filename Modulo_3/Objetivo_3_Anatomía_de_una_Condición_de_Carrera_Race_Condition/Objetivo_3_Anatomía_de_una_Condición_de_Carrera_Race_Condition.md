Una **Condición de Carrera (Race Condition)** de tipo **TOCTOU (Time-of-Check to Time-of-Use)** ocurre cuando existe una pequeña ventana de tiempo (milisegundos) entre el momento en que el servidor verifica si una condición es válida y el momento en que actualiza el estado en la base de datos.



**¿Cómo un atacante lo explota con Turbo Intruder (Burp Suite)?**

Si un atacante envía peticiones normales una tras otra, la latencia de red hace que lleguen en fila y el servidor alcance a marcar el cupón como usado tras la primera. Para vencer esa latencia, se utilizan técnicas de sincronización extrema:

* **Captura de la petición:** El atacante intercepta la petición HTTP legítima de canje (por ejemplo, POST /api/cupones/canjear) y la envía a Turbo Intruder (o al Repeater con envío en grupo).
* **Preparación en cola (Pre-rendering / Last-Byte Sync):** Turbo Intruder abre múltiples conexiones paralelas contra el servidor y envía casi toda la petición HTTP en cada una, reteniendo únicamente el último byte de cada paquete. De este modo, elimina la diferencia de tiempos de viaje por internet.
* **Disparo simultáneo (Gate):** Una vez que las 50 peticiones están esperando en la puerta del servidor listas para completarse, Turbo Intruder libera ese último byte en todas las conexiones al mismo microsegundo.
* **Explotación de la ventana:** El servidor web recibe las 50 peticiones en el mismo instante y las asigna a 50 hilos paralelos. Varios de esos hilos consultan la base de datos al mismo tiempo, ven que el cupón aún figura como disponible (usado = false) y aplican el descuento repetidas veces antes de que el primer hilo ejecute el UPDATE.



