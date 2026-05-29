# Compatibilidad de Vectores

Esta sección es crítica si vas a usar:

- `semantic_search_products`
- `hybrid_search_products`

Si envías vectores generados con otra configuración, el retrieval puede degradarse de forma importante aunque la request sea técnicamente válida.

## Vector denso

La colección actual usa:

- modelo: `openai/text-embedding-3-small`
- dimensión: `1536`
- nombre del vector en Qdrant: `text-dense`

## Regla de compatibilidad del dense vector

Si vas a enviar `dense_vector`:

- debe haber sido generado con `openai/text-embedding-3-small`
- debe tener longitud `1536`

Si usas otro modelo:

- aunque tenga la misma dimensión, no se garantiza compatibilidad semántica con la colección
- los resultados pueden perder relevancia

## Vector sparse

El sparse vector almacenado en Qdrant usa:

- nombre: `text-sparse`

Punto importante:

- Qdrant no está usando aquí un “modelo sparse por defecto”
- el sparse se genera en la plataforma con un encoder interno

## Cómo se genera el sparse

La estrategia actual es:

- normalización de texto
- tokenización por espacios
- conteo de frecuencia por token
- hash `blake2b`
- dimensión de hash `200003`

## Regla de compatibilidad del sparse vector

Si vas a usar `hybrid_search_products`:

- debes reproducir exactamente esa estrategia para `sparse_indices` y `sparse_values`
- no basta con enviar cualquier sparse vector aceptado por Qdrant

## Recomendación práctica

- si solo tienes texto: usa `search_products`
- si solo puedes garantizar el dense correcto: usa `semantic_search_products`
- usa `hybrid_search_products` solo si puedes reproducir exactamente:
  - modelo denso `openai/text-embedding-3-small`
  - dimensión `1536`
  - encoder sparse interno con hash dimension `200003`
