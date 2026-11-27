**sqlmap** falla principalmente cuando la aplicación requiere flujos de negocio complejos, cifrado personalizado o evasión de defensas dinámicas que una herramienta automatizada no puede interpretar por sí sola.



**Escenarios donde puede fallar:**

**1.Inyecciones de Segundo Orden (Second-Order SQL Injection):**

* **El escenario:** El usuario introduce el payload malicioso en un formulario (por ejemplo, al registrarse o actualizar su perfil: admin' OR 1=1--). La aplicación guarda ese texto de forma segura en la base de datos usando consultas parametrizadas (por lo que en ese momento no ocurre nada). Sin embargo, más tarde, otra función del sistema (como un panel de administrador o un generador de reportes) lee ese dato almacenado y lo concatena sin sanitizar en una nueva consulta SQL.
* **¿Por qué falla sqlmap?:** sqlmap espera una reacción inmediata en la respuesta HTTP de la misma petición donde envió el payload. Al no ver cambios ni retrasos en el registro, asume que el parámetro no es vulnerable y descarta el ataque.
* **¿Cómo lo logra el pentester manual?:** Usando el Repeater de Burp Suite, el atacante envía el payload en la petición A (registro) y luego envía manualmente la petición B (ver perfil/reporte) para observar el resultado o el error generado, confirmando y explotando la vulnerabilidad en dos pasos.



**2.Parámetros cifrados, firmados o con tokens anti-CSRF dinámicos:**

* **El escenario:** Muchas aplicaciones modernas (especialmente bancarias o APIs móviles) protegen sus peticiones enviando los parámetros dentro de un objeto JSON cifrado con AES en el lado del cliente (JavaScript), o incluyen un hash de integridad (HMAC) y un token anti-CSRF de un solo uso que cambia en cada petición.
* **¿Por qué falla sqlmap?:** Si sqlmap intenta inyectar comillas o comandos SQL directamente sobre el texto cifrado, destruye el formato y el servidor rechaza la petición con un error de descifrado o de firma inválida antes siquiera de llegar a la base de datos.
* **¿Cómo lo logra el pentester manual?:** El analista hace ingeniería inversa al código JavaScript del navegador para descubrir la clave o el algoritmo de cifrado. Luego, en Burp Suite, toma el payload SQL, lo cifra manualmente (o mediante una extensión personalizada) y recalcula la firma antes de enviarlo al servidor.

