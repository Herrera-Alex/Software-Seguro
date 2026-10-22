# Objetivo 4: Instalación y uso de un proxy

## 1. Introducción

En este laboratorio se analizó el comportamiento de un proxy dentro de una red, con el objetivo de comprender cómo intercepta el tráfico de datos y cómo afecta la comunicación entre el usuario y los servicios web.

Durante la práctica, se evidenció que Burp Suite fue capaz de interceptar las peticiones generadas en el laboratorio, lo que permitió observar el flujo de información antes de que llegara a su destino.

## 2. Observación del laboratorio

El proxy funciona como un intermediario entre el cliente y el servidor de destino. En este caso, la herramienta de análisis interceptó las solicitudes, lo que permitió ver cómo el tráfico era redirigido y revisado antes de continuar su camino.

> Esto confirma que el proxy puede inspeccionar el tráfico en tránsito, especialmente cuando no existe cifrado de extremo a extremo.

## 3. ¿Qué es un proxy?

Un proxy es un servidor intermedio que se sitúa entre el dispositivo del usuario y Internet. Cuando se utiliza un proxy, las peticiones salen primero hacia ese servidor, quien las procesa y luego las envía al destino final.

Esto permite:

- ocultar la dirección IP original del usuario,
- controlar o filtrar tráfico,
- inspeccionar solicitudes y respuestas,
- y aplicar políticas de seguridad o monitoreo.

Sin embargo, el proxy no siempre cifra el tráfico, por lo que los datos pueden quedar visibles para el servidor proxy o para la persona que lo administra.

## 4. Diferencia entre proxy y VPN

| Característica | Proxy | VPN |
|---|---|---|
| Cifrado de datos | No cifra el tráfico por defecto. Los datos pueden viajar en claro. | Cifra todo el tráfico de extremo a extremo. |
| Alcance | Solo afecta a la aplicación o navegador configurado. | Protege todo el tráfico del dispositivo. |
| Seguridad | Baja, ya que el administrador del proxy puede inspeccionar el tráfico. | Alta, ideal para redes Wi‑Fi públicas y conexiones sensibles. |
| Rendimiento | Suele ser más rápido y ligero. | Puede reducir ligeramente la velocidad por el cifrado. |

## 5. Conclusión

Un proxy es útil para analizar, redirigir o supervisar tráfico a nivel de aplicación, pero no proporciona protección completa del contenido. En cambio, una VPN ofrece un cifrado más robusto y protege el tráfico del sistema completo.

## 6. Resumen final

- El proxy actúa como intermediario en la comunicación.
- Burp Suite puede interceptar tráfico para revisarlo.
- Un proxy no es equivalente a una VPN.
- La VPN ofrece mayor seguridad por cifrado, mientras que el proxy se centra más en la inspección o control del tráfico.

## 7. Conclusión final

Este laboratorio permitió comprender cómo un proxy puede interceptar y observar el tráfico de red, además de resaltar la diferencia entre un proxy y una VPN. La principal diferencia es que la VPN protege todo el tráfico mediante cifrado, mientras que el proxy simplemente actúa como punto intermedio y puede revisar la información que pasa por él.