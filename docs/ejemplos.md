# Ejemplos de Consumo

## Ejemplo desde Python

```python
import asyncio
import json
import warnings

warnings.filterwarnings(
    "ignore",
    message=r"authlib\.jose module is deprecated.*",
    category=Warning,
)

from fastmcp import Client
from fastmcp.client.transports import StreamableHttpTransport


MCP_URL = "https://mcp-productos.cuenti.co/mcp/"
API_TOKEN = "REEMPLAZAR_CON_TOKEN"
COMPANY_ID = "REEMPLAZAR_CON_COMPANY_ID"
BRANCH_ID = "REEMPLAZAR_CON_BRANCH_ID"
EMPLOYEE_ID = "REEMPLAZAR_CON_EMPLOYEE_ID"
REQUEST_ID = "<request_id>"
QUERY = "producto de ejemplo"
TOP_K = 5


async def main() -> None:
    transport = StreamableHttpTransport(
        url=MCP_URL,
        headers={
            "Authorization": f"Bearer {API_TOKEN}",
            "X-Auth-Token-Empresa": COMPANY_ID,
            "X-Branch-Id": BRANCH_ID,
            "X-Employee-Id": EMPLOYEE_ID,
            "X-Request-Id": REQUEST_ID,
        },
    )

    async with Client(transport) as client:
        tools = await client.list_tools()
        print([tool.name for tool in tools])

        result = await client.call_tool(
            "search_products",
            {
                "company_id": COMPANY_ID,
                "branch_id": BRANCH_ID,
                "query": QUERY,
                "top_k": TOP_K,
            },
        )

        payload = result.data or result.structured_content
        if payload is not None:
            print(json.dumps(payload, indent=2, ensure_ascii=False))
        else:
            print(result)


asyncio.run(main())
```

## Verificar health

```bash
curl https://mcp-productos.cuenti.co/health
```

## Recomendaciones de uso

- si solo tienes texto del usuario: usa `search_products`
- si ya tienes el embedding denso compatible: usa `semantic_search_products`
- si ya tienes dense + sparse compatibles: usa `hybrid_search_products`
