# Ejemplos de Uso (Descargables)

En esta carpeta publicamos ejemplos listos para descargar y ejecutar como clientes del MCP.

## ¿Para qué sirve esta carpeta?

- permite compartir implementaciones de referencia en formato portable (`.zip`)
- facilita onboarding de equipos técnicos que solo necesitan un ejemplo puntual
- mantiene los ejemplos separados de la documentación narrativa para versionarlos por lenguaje

## ¿Por qué está dentro de la documentación?

- centraliza el acceso: quien lee la doc también encuentra el ejemplo ejecutable
- reduce fricción: puedes descargar, abrir y probar en minutos
- prepara el crecimiento del proyecto: aquí iremos agregando ejemplos para más lenguajes

## Archivos disponibles

- [ejemplo-uso-mcp-python.zip](ejemplos-uso/ejemplo-uso-mcp-python.zip)
- [ejemplo-uso-mcp-nodejs.zip](ejemplos-uso/ejemplo-uso-mcp-nodejs.zip)
- [ejemplo-uso-mcp-langchain.zip](ejemplos-uso/ejemplo-uso-mcp-langchain.zip)

Sugerencia:

- si tu caso de uso parte de texto del usuario y no necesitas controlar embeddings manualmente, suele ser mejor empezar por las tools base (por ejemplo `search_products`), ya que el servidor puede aplicar su pipeline completo de normalizacion y retrieval
- las tools con vectores precomputados (`semantic_search_products` / `hybrid_search_products`) son utiles cuando ya cuentas con dense/sparse compatibles y buscas control total del flujo

## Próximamente

En esta misma sección se seguirán agregando paquetes equivalentes para otros stacks (por ejemplo Go y otros lenguajes).
