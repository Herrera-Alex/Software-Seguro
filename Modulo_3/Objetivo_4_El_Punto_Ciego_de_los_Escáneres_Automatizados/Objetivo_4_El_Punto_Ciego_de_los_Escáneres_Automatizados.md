La lógica de negocio es el mayor **punto ciego** de los escáneres automatizados porque estas herramientas detectan patrones técnicos y errores de sintaxis, pero carecen de contexto humano y comprensión funcional sobre cómo debería operar legítimamente cada aplicación.



**1.¿Por qué fallan los escáneres automatizados?**

* **Ausencia de contexto y propósito:** Un escáner no sabe qué es un "carrito de compras", qué significa un "cupón de un solo uso" ni por qué una cantidad no puede ser -5. Para la herramienta, enviar un -5 y recibir un código HTTP 200 OK sin errores de servidor parece una operación normal y válida.
* **Flujos de múltiples pasos:** Muchos procesos de negocio requieren seguir una secuencia específica (registrar usuario -> aplicar descuento -> confirmar pago). Los escáneres no pueden razonar qué pasa si un atacante se salta el paso intermedio para llegar directo a la confirmación sin pagar.



**2.¿Por qué la auditoría manual es indispensable?**

* **Comprensión del negocio y pensamiento crítico:** Un auditor humano entiende el valor real de los activos y las reglas del negocio (por ejemplo, que nadie debería ganar dinero comprando un producto o canjear dos veces el mismo beneficio)**.**
* **Creatividad y abuso de flujos:** El pentester puede ponerse en el lugar del atacante para formular hipótesis ("¿qué pasa si cambio este estado?", "¿qué ocurre si envío peticiones simultáneas?"), diseñando pruebas a medida que ninguna regla genérica de un escáner podría anticipar.

