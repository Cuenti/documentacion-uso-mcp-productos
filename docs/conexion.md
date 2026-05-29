# Conexión y Autenticación

## Transporte

El MCP usa transporte `streamable_http`.

Si usas una librería MCP, normalmente la librería manejará:

- `initialize`
- `notifications/initialized`
- `mcp-session-id`
- `tools/list`
- `tools/call`

Si usas `curl`, Postman o integración propia, debes implementar el flujo MCP manualmente.

## Headers requeridos

Todas las requests deben incluir:

```http
Authorization: Bearer <api_token>
X-Auth-Token-Empresa: <company_id>
X-Branch-Id: <branch_id>
```

Header opcional:

```http
X-Employee-Id: <employee_id>
```

Header recomendado:

```http
X-Request-Id: <request_id>
```

## Reglas de validación

- `company_id` en la tool debe coincidir con `X-Auth-Token-Empresa`
- si mandas `branch_id` en la tool, debe coincidir con `X-Branch-Id`
- si omites `branch_id` en la tool, el MCP usa la sucursal autenticada

## Flujo MCP de bajo nivel

### 1. Initialize

`POST /mcp/`

Body:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "initialize",
  "params": {
    "protocolVersion": "2025-11-25",
    "capabilities": {},
    "clientInfo": {
      "name": "mi-cliente",
      "version": "1.0"
    }
  }
}
```

La respuesta puede incluir `mcp-session-id`. Si aparece, reenvíalo en las siguientes requests.

### 2. Initialized notification

`POST /mcp/`

Body:

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/initialized",
  "params": {}
}
```

### 3. Listar tools

`POST /mcp/`

Body:

```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "tools/list",
  "params": {}
}
```

### 4. Llamar una tool

`POST /mcp/`

Body:

```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "method": "tools/call",
  "params": {
    "name": "search_products",
    "arguments": {
      "company_id": "<company_id>",
      "branch_id": "<branch_id>",
      "query": "producto de ejemplo",
      "top_k": 5
    }
  }
}
```
