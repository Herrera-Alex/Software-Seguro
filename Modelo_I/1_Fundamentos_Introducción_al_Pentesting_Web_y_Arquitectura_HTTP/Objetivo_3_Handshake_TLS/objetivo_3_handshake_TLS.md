# El Handshake TLS

Más conocido como **apretón de manos**, el handshake TLS es una forma de cifrado segura para la comunicación entre ordenadores.

## ¿Cómo funciona el handshake?

Se puede explicar en cuatro pasos:

### 1. El "Hola" del cliente

El cliente inicia el handshake de TLS enviando información de configuración al servidor. Esto incluye datos como la versión de TLS compatible con el cliente, los conjuntos de cifrado que puede utilizar y algunos datos aleatorios denominados `client random`.

### 2. El "Hola" del servidor

El servidor responde escogiendo la versión de TLS y el algoritmo de cifrado que ambos tienen en común. En este mismo paso, el servidor le envía su certificado digital al navegador.

### 3. Verificación e intercambio de claves

El navegador analiza el certificado. Si es válido, utiliza cifrado asimétrico para acordar o enviarle al servidor una combinación matemática de la cual ambos generarán una clave maestra secreta.

### 4. Finalización

Ambos se envían un mensaje cifrado confirmando que todo está listo. A partir de este momento, se cierra el apretón de manos y el navegador envía su primera petición HTTP de forma segura.

## ¿Qué son el cifrado simétrico y asimétrico?

### Cifrado asimétrico

Usa una llave pública, que todos pueden ver, para cifrar y una llave privada, que permanece secreta en el servidor, para descifrar.

### Cifrado simétrico

Utiliza la misma clave secreta tanto para cifrar como para descifrar los datos que viajan de ida y vuelta.

## ¿Qué son los certificados digitales?

El certificado digital actúa como el documento nacional de identidad (DNI) o pasaporte del sitio web. No sirve para ocultar los datos, sino para evitar la suplantación de identidad, es decir, impedir que un atacante se haga pasar por el sitio legítimo.