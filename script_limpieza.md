# Script de limpieza en Power Query

```powerquery
let
    Origen = Table.FromRows(Json.Document(Binary.Decompress(Binary.FromText("XZBBasMwEEWvMmgdF0m2WndpJ4GWNhAaly5MFoqihcCWjGxBr5Mz9Ai+WEcqhaq7mQeP/2f6njCyIfAqp8VNcPQOmAAkWzdOYZHKrF8WV8YpvaMUJ055VVBWUEHOm55wRAcXZg3PVg7rbbx4oxxCqZSenTdujlL9T66TXMboTqtBXh0ctFpvFuUYf3x737cNDo8iNxlPZpVirVmch+olGiovXImsLy9omUQRI5uAJcMgvZ6h7ZA04Wrcz5m5xWiy7hGdTjvYfy7aW/xR12YtWZl55e93HhB96IuSIzztYs7fp9Qid+Jp528=", BinaryEncoding.Base64), Compression.Deflate)), let _t = ((type nullable text) meta [Serialized.Text = true]) in type table [id_venta = _t, nombre_producto = _t, categoria = _t, precio = _t, fecha_venta = _t]),
  // Paso 2: eliminar espacios al inicio y al final de nombre_producto
    LimpiarEspacios = Table.TransformColumns(
        Origen,
        {{"nombre_producto", Text.Trim, type text}}
    ),

    // Paso 3: unificar la categoría y dejarla con formato de título
    EstandarizarCategoria = Table.TransformColumns(
        LimpiarEspacios,
        {{"categoria", each Text.Proper(Text.Trim(_)), type text}}
    ),

    // Paso 4: eliminar los registros utilizados como prueba
    EliminarPruebas = Table.SelectRows(
        EstandarizarCategoria,
        each [categoria] <> "Prueba"
    ),

    // Paso 5: asignar el tipo de dato correcto a cada columna
    TiparColumnas = Table.TransformColumnTypes(
        EliminarPruebas,
        {
            {"id_venta", Int64.Type},
            {"nombre_producto", type text},
            {"categoria", type text},
            {"precio", type number},
            {"fecha_venta", type date}
        },
        "en-US"
    )
in
    TiparColumnas
    )
in
    TiparColumnas
