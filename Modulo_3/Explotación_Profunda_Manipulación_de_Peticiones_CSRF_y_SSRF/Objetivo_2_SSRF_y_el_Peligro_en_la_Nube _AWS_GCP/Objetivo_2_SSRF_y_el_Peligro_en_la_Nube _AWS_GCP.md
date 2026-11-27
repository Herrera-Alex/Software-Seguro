Si un atacante explota una vulnerabilidad **SSRF** en una aplicación alojada en AWS y fuerza al servidor a consultar la dirección IP 169.254.169.254, logra acceder al Servicio de Metadatos de Instancia de EC2 (IMDS - Instance Metadata Service), desde donde puede extraer credenciales temporales de IAM (claves de acceso y tokens de sesión) para tomar el control de otros servicios en la nube de la empresa.



**¿Qué información altamente sensible extrae el atacante?**

Al navegar por las rutas del servicio de metadatos (principalmente bajo http://169.254.169), el atacante busca los siguientes datos críticos:

* **Credenciales temporales de IAM (IAM Role Credentials) — El objetivo principal:** 

&#x09;Si la instancia EC2 tiene asignado un Rol de IAM (algo muy común para que 	la aplicación pueda leer archivos en S3, escribir en bases de datos 	DynamoDB, etc.), el atacante consulta la ruta: http://169.254.169<nombre-	del-rol> 

&#x09;**El servidor devuelve un objeto JSON con tres datos críticos:** 

&#x09;**.**AccessKeyId (ID de clave de acceso)

&#x09;.SecretAccessKey (Clave secreta)

&#x09;.Token (Token de sesión temporal)

&#x09;**Impacto:** Con estos tres valores, el atacante configura la herramienta aws-	cli en su propia computadora y suplanta la identidad del servidor, pudiendo 	descargar bases de datos, leer buckets privados de S3 o escalar privilegios 	dentro de la cuenta de AWS.

* **Datos de usuario y scripts de arranque (User Data):**

&#x09;Consultando http://169.254.169, el atacante puede obtener los scripts de 	inicialización que se ejecutaron al crear el servidor. A menudo, los 	desarrolladores dejan allí contraseñas en texto plano, cadenas de conexión 	a bases de datos, llaves privadas SSH o tokens de API.

* **Información de red e infraestructura interna:**

&#x09;A través de rutas como /meta-data/network/ o /meta-data/identity-	credentials/, obtiene IPs privadas de la VPC, grupos de seguridad 	(Security Groups), ID de la cuenta de AWS y certificados internos, 	facilitando el movimiento lateral hacia otros servidores internos.



