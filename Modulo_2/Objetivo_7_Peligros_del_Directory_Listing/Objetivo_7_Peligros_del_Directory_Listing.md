**Objetivo 3: Peligros del "Directory Listing"**





**1.¿Qué ocurre técnicamente cuando está activo?**

Cuando un usuario o atacante realiza una petición HTTP (generalmente GET) a la URL de un directorio específico en un servidor web (por ejemplo, https://ejemplo.com), el servidor busca primero un archivo de índice predeterminado (como index.html, index.php o default.aspx).



**Comportamiento seguro (Deshabilitado):** Si el archivo de índice no existe y el listado de directorios está desactivado, el servidor responde con un código de estado HTTP 403 Forbidden (Prohibido), denegando el acceso al contenido de la carpeta.



**Comportamiento vulnerable (Habilitado):** Si no encuentra el archivo de índice y la directiva está activa (ej. Options +Indexes en Apache o autoindex on; en Nginx), el módulo correspondiente del servidor genera dinámicamente una página HTML que muestra un índice navegable con todos los archivos y subcarpetas alojados en esa ruta, junto con metadatos como su tamaño y fecha de última modificación.



**2.Tipos de archivos sensibles que pueden quedar expuestos:**

Al permitir que cualquier persona navegue por la estructura interna de carpetas, un atacante puede descubrir y descargar información crítica que no estaba destinada al público:



**Archivos de configuración y credenciales:** Archivos como .env, config.php, wp-config.php.bak o web.config, que suelen contener contraseñas de bases de datos, claves de API (API Keys) y tokens secretos.



**Copias de seguridad (Backups) y volcados de datos:** Archivos comprimidos (.zip, .tar.gz, .rar) o volcados de bases de datos (.sql, .bak) guardados temporalmente en directorios públicos.



**Código fuente sin procesar:** Archivos de código o repositorios completos (como la carpeta oculta .git/), permitiendo al atacante analizar la lógica interna de la aplicación en busca de otras vulnerabilidades.



**Archivos de registro (Logs):** Archivos .log que pueden revelar rutas internas del servidor, versiones de software, direcciones IP o información de sesiones de usuarios.



**Documentos privados o internos:** Facturas, reportes, datos personales de clientes (PII) o documentos subidos por otros usuarios en carpetas tipo /uploads/ o /temp/.





**3.¿Cómo se mitiga esta vulnerabilidad?**

La solución principal consiste en deshabilitar explícitamente el listado de directorios en la configuración del servidor web para que devuelva un error 403 Forbidden cuando falte el archivo índice:



**Archivos índice vacíos:** Colocar un archivo index.html en blanco dentro de los directorios públicos (como /images o /uploads) como capa extra de defensa.



**Principio de menor privilegio:** No almacenar copias de seguridad, código fuente o archivos .env dentro de la raíz pública del servidor web (/var/www/html).

