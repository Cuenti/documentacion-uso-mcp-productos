# Playground con MCP Inspector (Docker)

Esta guía explica cómo probar el MCP de productos usando MCP Inspector ejecutado con Docker Compose.

## Qué necesitas

- Docker y Docker Compose
- credenciales válidas del MCP
  - `Authorization: Bearer <token>`
  - `X-Company-Id: <company_id>`
  - `X-Branch-Id: <branch_id>`

## Archivo Docker Compose

Puedes descargar el archivo de configuración para levantar MCP Inspector:

- [Descargar docker-compose.yml](assets/downloads/mcp-inspector/docker-compose.yml){ download="docker-compose.yml" }

## Levantar MCP Inspector

Desde la raíz donde descargaste el archivo, ejecuta:

```bash
docker compose up -d
```

Para ver logs y obtener el token de sesión:

```bash
docker compose logs -f mcp-inspector
```

## Conectar al MCP de productos

1. Revisa los logs y ubica la línea `MCP Inspector is up and running at:`.
2. Abre en el navegador el enlace exacto que imprime la consola (incluye el token de sesión).
      - ejemplo: `http://0.0.0.0:6274/?MCP_PROXY_AUTH_TOKEN=<TOKEN>`
3. Selecciona transporte `Streamable HTTP`.
4. Usa la URL del MCP:
   - `https://mcp-productos.cuenti.co/mcp/`.
5. Selecciona conexión vía `MCP Inspector Proxy` o simplemente `Via Proxy`
6. No toques nada de `OAuth 2.0 Flow` para esta integración.
7. Agrega headers:
   - `Authorization: Bearer <token>`
   - `X-Company-Id: <company_id>`
   - `X-Branch-Id: <branch_id>`
8. Conecta al servidor MCP.
9.  Revisa las tools disponibles.
10. Ejecuta pruebas con tus credenciales.

## Solución de problemas rápida

- Si ves `invalid origin`, verifica que estés abriendo `http://localhost:6274`.
- Si falla autenticación, revisa token, `company_id` y `branch_id`.
