# Script de limpieza en Power Query

```powerquery
let
    Origen = Table.FromRows(...),

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
