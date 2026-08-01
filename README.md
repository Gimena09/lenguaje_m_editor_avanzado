# lenguaje_m_editor_avanzado
# Lenguaje M en el Editor Avanzado

## Descripción

Este proyecto muestra una limpieza de datos realizada directamente con lenguaje M en el Editor Avanzado de Power Query.

La tabla original contenía espacios en blanco en los nombres de productos, categorías escritas con distintos formatos, registros de prueba y tipos de datos que debían corregirse.

## Transformaciones realizadas

- Eliminación de espacios al inicio y al final en nombre_producto.
- Estandarización de categoria con formato de título.
- Eliminación de los registros con categoría PRUEBA.
- Asignación correcta de tipos de datos.
- Uso de comentarios descriptivos dentro del código M.

## Preguntas teóricas

### 1. ¿Qué hace exactamente el bloque let ... in en lenguaje M? ¿Por qué cada paso puede referenciar al anterior?

El bloque let ... in organiza una consulta en una secuencia de pasos. Dentro de let se definen las transformaciones y cada paso puede usar el resultado del anterior como entrada. La sección in indica cuál de esos pasos será devuelto como resultado final de la consulta.

### 2. ¿Por qué M es Case Sensitive y qué consecuencia práctica tiene?

M distingue entre mayúsculas y minúsculas. Por eso, Table.SelectRows y table.selectrows no son lo mismo. Si una función se escribe con una combinación incorrecta de mayúsculas y minúsculas, Power Query genera un error porque no reconoce el nombre.

### 3. ¿Cuál es la diferencia entre Text.Trim y Text.Clean en M?

Text.Trim elimina espacios al inicio y al final de un texto. En cambio, Text.Clean elimina caracteres no imprimibles, como saltos de línea ocultos o caracteres de control. Ambas funciones limpian texto, pero resuelven problemas diferentes.

### 4. ¿Por qué se filtraron los registros PRUEBA después de estandarizar la categoría y no antes?

Se estandarizó primero la categoría para unificar valores como prueba, PRUEBA y Prueba. Después de convertirlos al mismo formato, el filtro pudo eliminar todos los registros de prueba de manera consistente. Si se filtraba antes, algunos registros podían quedar sin eliminar por diferencias entre mayúsculas y minúsculas.
