# Tools Disponibles

## `get_collection_status`

Consulta si la colección existe para una empresa.

Input:

```json
{
  "company_id": "<company_id>"
}
```

## `lookup_products`

Búsqueda exacta dentro de una empresa y sucursal.

Soporta:

- `sku`
- `sku_candidates`
- `id_producto_sucursal`

### Por SKU

```json
{
  "company_id": "<company_id>",
  "branch_id": "<branch_id>",
  "sku": "<sku>",
  "top_k": 5
}
```

### Por varias variantes de SKU

```json
{
  "company_id": "<company_id>",
  "branch_id": "<branch_id>",
  "sku_candidates": ["<sku>", "<sku_alternativo_1>", "<sku_alternativo_2>"],
  "top_k": 5
}
```

### Por `idProductoSucursal`

```json
{
  "company_id": "<company_id>",
  "branch_id": "<branch_id>",
  "id_producto_sucursal": "<id_producto_sucursal>",
  "top_k": 5
}
```

Uso recomendado:

- ya conoces el identificador exacto
- no quieres semántica ni embeddings

## `search_products`

Tool principal para texto natural.

Input:

```json
{
  "company_id": "<company_id>",
  "branch_id": "<branch_id>",
  "query": "producto de ejemplo y su stock",
  "top_k": 5
}
```

Comportamiento:

- intenta exact match si detecta un identificador
- si no, genera embedding y sparse internamente
- luego ejecuta búsqueda híbrida

Uso recomendado:

- agentes
- asistentes
- integraciones conversacionales
- clientes que solo tienen texto del usuario

## `semantic_search_products`

Búsqueda semántica dense-only.

Input:

```json
{
  "company_id": "<company_id>",
  "branch_id": "<branch_id>",
  "dense_vector": [<float_1>, <float_2>, <float_3>, <float_n>],
  "top_k": 5
}
```

Uso recomendado:

- ya tienes el embedding denso correcto
- no vas a enviar sparse

## `hybrid_search_products`

Búsqueda híbrida usando dense y sparse precomputados.

Input:

```json
{
  "company_id": "<company_id>",
  "branch_id": "<branch_id>",
  "normalized_query": "producto de ejemplo",
  "dense_vector": [<float_1>, <float_2>, <float_3>, <float_n>],
  "sparse_indices": [<index_1>, <index_2>, <index_n>],
  "sparse_values": [<value_1>, <value_2>, <value_n>],
  "top_k": 5
}
```

Uso recomendado:

- ya controlas el dense y el sparse
- quieres control total del retrieval
