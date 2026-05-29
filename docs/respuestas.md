# Contratos de Respuesta

## `get_collection_status`

Respuesta:

```json
{
  "collection_name": "<collection_name>",
  "exists": true
}
```

## Respuesta de las búsquedas

Todas las tools de búsqueda devuelven este contrato general:

```json
{
  "collection_name": "<collection_name>",
  "match_type": "exact",
  "matched_field": "sku",
  "results": [
    {
      "company_id": "<company_id>",
      "id_producto": "<id_producto>",
      "id_sucursal": "<branch_id>",
      "id_producto_sucursal": "<id_producto_sucursal>",
      "nombre": "PRODUCTO DE EJEMPLO",
      "sku": "<sku>",
      "id_marca": "<id_marca>",
      "nombre_marca": "MARCA DE EJEMPLO",
      "id_categoria": "<id_categoria>",
      "nombre_categoria": "CATEGORIA DE EJEMPLO",
      "semantic_text": "Producto: PRODUCTO DE EJEMPLO. Categoría: CATEGORIA DE EJEMPLO. Marca: MARCA DE EJEMPLO. SKU: <sku>.",
      "normalized_text": "producto: producto de ejemplo. categoria: categoria de ejemplo. marca: marca de ejemplo. sku: <sku>.",
      "precio_venta": "<precio_venta>",
      "precio_compra": "<precio_compra>",
      "costo": "<costo>",
      "existencias": "<existencias>",
      "score": "<score>"
    }
  ]
}
```

## Significado de los campos

- `collection_name`: nombre de la colección consultada
- `match_type`: `exact`, `semantic` o `hybrid`
- `matched_field`: campo que produjo el exact match. Puede ser `null`
- `results`: lista de productos encontrados

Cada item de `results` puede incluir:

- `company_id`
- `id_producto`
- `id_sucursal`
- `id_producto_sucursal`
- `nombre`
- `sku`
- `id_marca`
- `nombre_marca`
- `id_categoria`
- `nombre_categoria`
- `semantic_text`
- `normalized_text`
- `precio_venta`
- `precio_compra`
- `costo`
- `existencias`
- `score`

## Notas

- `score` es relativo al modo de búsqueda
- `matched_field` suele venir en búsquedas exactas
- `semantic_text` y `normalized_text` son útiles para depuración

## Respuesta vacía

Si no hay coincidencias:

```json
{
  "collection_name": "<collection_name>",
  "match_type": "hybrid",
  "matched_field": null,
  "results": []
}
```
