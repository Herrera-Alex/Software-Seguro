# Mapeo lógico

## Diagrama

El flujo principal del sistema representa la comunicación entre el **Cliente** y el **Servidor**:

```mermaid
flowchart LR
    Cliente[Cliente] -->|Petición| Servidor[Servidor]
    Servidor -->|Respuesta| Cliente
```

## Elementos

| Elemento | Responsabilidad |
| --- | --- |
| Cliente | Inicia la comunicación enviando una petición. |
| Servidor | Recibe la petición, la procesa y devuelve una respuesta. |

## Diagrama interactivo

[Abrir el diagrama en diagrams.net](./diagrama.drawio.md.html)