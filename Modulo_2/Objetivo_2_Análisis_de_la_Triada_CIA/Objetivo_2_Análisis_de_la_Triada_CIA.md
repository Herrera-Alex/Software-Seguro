**Objetivo 2: Análisis de la Triada CIA**

**Confidencialidad:**

Garantiza que la información sea accesible únicamente para las personas, sistemas o procesos autorizados, evitando cualquier divulgación no permitida.

**Ejemplo de ataque web:** Inyección SQL (SQLi) orientada a extracción de datos. Un atacante manipula un campo de búsqueda en una tienda en línea para ejecutar comandos no autorizados en la base de datos y descargar la tabla completa de usuarios, exponiendo contraseñas y correos electrónicos privados.



**Integridad:**

Asegura que los datos se mantengan exactos, completos y sin alteraciones indebidas durante su almacenamiento o transmisión, detectando cualquier modificación no autorizada.

**Ejemplo de ataque web:** Cross-Site Request Forgery (CSRF) o manipulación de parámetros en una API (IDOR). Un atacante engaña al navegador de un usuario autenticado en su banco en línea para que envíe una petición oculta que altera el número de cuenta de destino y el monto de una transferencia sin su consentimiento.



**Disponibilidad:**

Garantiza que los sistemas, servicios y datos estén operativos y accesibles en el momento en que los usuarios legítimos los necesiten.

**Ejemplo de ataque web:** Denegación de Servicio Distribuida (DDoS) a nivel de aplicación (Capa 7). Una red de bots envía millones de peticiones HTTP complejas por segundo contra el buscador de un portal gubernamental, saturando la memoria y el CPU del servidor hasta que la página deja de responder para los ciudadanos.



