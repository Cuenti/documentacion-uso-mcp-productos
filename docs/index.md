# MCP de Productos

Documentación oficial del MCP de productos basado en Qdrant.

Este servicio expone herramientas MCP para consultar el catálogo vectorial de productos de una empresa y una sucursal específicas. Está pensado para ser consumido por:

- agentes IA
- chatbots
- asistentes
- ERPs
- CRMs
- integraciones externas

## Qué permite hacer

El MCP permite:

- buscar productos por texto natural
- buscar productos por SKU
- buscar productos por `idProductoSucursal`
- buscar productos usando un vector denso precomputado
- buscar productos usando dense + sparse precomputados
- consultar el estado de la colección

## Reglas funcionales

- todas las búsquedas quedan filtradas por empresa autenticada
- la información de inventario, precios y existencias corresponde solo a la sucursal autenticada o solicitada
- no se mezclan resultados entre empresas
- no se mezclan resultados entre sucursales
- un producto solo aparece si existe en la sucursal filtrada

## Endpoints

- `GET /health`
- `POST /mcp/`

Importante:

- usa siempre `/mcp/` con slash final
- algunos clientes MCP fallan si apuntas a `/mcp` sin slash final y reciben redirección

Ejemplo:

```text
https://mcp-productos.cuenti.co/mcp/
```

## Modos de búsqueda

El MCP soporta tres modos:

1. `exact`
   - por `sku`
   - por `idProductoSucursal`

2. `semantic`
   - dense-only
   - el cliente envía el vector denso precomputado

3. `hybrid`
   - dense + sparse
   - el cliente envía ambos vectores precomputados

Además existe una tool de conveniencia:

- `search_products`
  - detecta exact match si aplica
  - si no, genera internamente dense + sparse y hace búsqueda híbrida

## Navegación recomendada

- Si vas a conectar un cliente nuevo: revisa primero [Conexión y Autenticación](conexion.md)
- Si vas a enviar vectores precomputados: revisa [Compatibilidad de Vectores](vectores.md)
- Si necesitas el detalle de inputs por tool: revisa [Tools Disponibles](tools.md)
- Si necesitas el shape de salida: revisa [Contratos de Respuesta](respuestas.md)
- Si quieres copiar ejemplos listos: revisa [Ejemplos de Consumo](ejemplos.md)
- Si quieres descargar proyectos base listos para ejecutar: revisa [Ejemplos Descargables](ejemplos-uso.md)
