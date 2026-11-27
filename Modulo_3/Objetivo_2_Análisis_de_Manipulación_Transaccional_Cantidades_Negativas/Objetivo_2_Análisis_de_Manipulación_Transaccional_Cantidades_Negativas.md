Esta vulnerabilidad corresponde a una falla de lógica de negocio (Business Logic Flaw) combinada con una validación insuficiente de entradas (CWE-20).



**1. ¿Por qué ocurre técnicamente esta falla?**

* **Ausencia de validación de dominio en el Backend:** El servidor verifica únicamente que el campo cantidad sea un dato numérico válido (por ejemplo, un entero int) para evitar errores de sintaxis, pero omite comprobar si tiene sentido dentro de la regla de negocio.
* **Cálculo aritmético sin control de signo:** El backend ejecuta directamente la operación matemática (subtotal = precio\_unitario \* cantidad). Al multiplicar un precio positivo ($100) por una cantidad negativa (-5), obtiene un subtotal negativo (-$500), el cual al sumarse al balance o proceso de pago invierte el flujo financiero a favor del atacante.
* **Confianza ciega en el cliente (Frontend):** El desarrollador probablemente restringió las cantidades únicamente en la interfaz gráfica (por ejemplo, con <input type="number" min="1"> en HTML o botones +/-), asumiendo que ningún usuario enviaría un número negativo.



**2. ¿Cómo debe validarlo estrictamente el desarrollador en el servidor?**

Para remediarlo, el backend debe aplicar principios de programación defensiva antes de realizar cualquier cálculo:

* **Validación estricta de tipo de dato:** Verificar que el parámetro recibido sea exactamente un número entero (integer), rechazando cadenas de texto, decimales, valores nulos o arreglos.
* **Validación de rango mínimo y máximo (Límites de negocio):**Exigir explícitamente que la cantidad sea estrictamente mayor o igual a uno (cantidad >= 1 o cantidad > 0), devolviendo un error 400 Bad Request ante cualquier valor cero o negativo. Establecer un límite máximo razonable por compra y verificar que no supere el stock disponible en la base de datos (cantidad <= stock\_actual).
* **Verificación de integridad en el total de la transacción:** Como última capa de defensa antes de procesar el pago o actualizar saldos, validar que tanto el subtotal de cada ítem como el monto total de la orden sean estrictamente positivos (total > 0).

