Objetivo 10: Análisis de Automatización y Fuerza Bruta:
Su principales diferencias son:



**Fuerza Bruta Tradicional:** Prueba combinaciones de forma matemática y secuencial (ej. a, b, c... aa, ab, ac). Intenta adivinar la clave probando todos los caracteres posibles hasta acertar. Es altamente ineficiente pero infalible si se cuenta con tiempo ilimitado.



**Ataque de Diccionario:** Utiliza un archivo de texto precargado con palabras reales, contraseñas comunes (ej. 123456, password) o datos filtrados. No pierde tiempo con combinaciones caóticas; va directo a lo que los humanos suelen elegir. Es mucho más rápido pero depende totalmente de la calidad de la lista.



**Mecanismo de defensa:**

Para mitigar estas automatizaciones en un formulario de login, un desarrollador puede implementar:



**Bloqueo de cuentas (Account Lockout):** Deshabilitar temporalmente el inicio de sesión tras un número específico de intentos fallidos (ej. 3 o 5 intentos).



**Limitación de tasa (Rate Limiting):** Restringir la cantidad de solicitudes HTTP permitidas desde una misma dirección IP en un periodo de tiempo.



**CAPTCHA:** Introducir desafíos visuales o de comportamiento que solo un humano pueda resolver, deteniendo los scripts automatizados.



**Autenticación de Múltiples Factores (MFA):** Añadir un segundo paso (como un código por SMS o app), haciendo que adivinar la contraseña no sea suficiente para entrar.

