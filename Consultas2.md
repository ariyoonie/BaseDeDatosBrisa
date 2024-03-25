# Operaciones de Gestión de Datos

En el entorno de MongoDB, se realizan diversas operaciones para la gestión eficiente de datos, incluyendo lectura, escritura, actualización y eliminación.

## Operaciones de Consulta

Para buscar documentos en una colección, existen varias operaciones de consulta:

- `db.collection.find()`: Permite buscar documentos según criterios específicos.
- `db.collection.findOne()`: Recupera un solo documento que cumple con los criterios especificados.
- `db.collection.aggregate()`: Realiza operaciones de agregación en los datos, como agrupamiento, filtrado y transformación.
- `db.collection.distinct()`: Devuelve un conjunto de valores distintos para un campo específico.
- `db.collection.countDocuments()`: Cuenta los documentos que cumplen con los criterios especificados.

## Gestión de Bases de Datos y Colecciones

Las operaciones para gestionar bases de datos y colecciones incluyen:

- `show dbs;`: Muestra todas las bases de datos disponibles.
- `use dbs (Nombre base de datos);`: Selecciona una base de datos específica para su uso.
- `db.createCollection(Nombre de la colección);`: Crea una nueva colección en la base de datos actual.
- `show collections;`: Muestra todas las colecciones existentes en la base de datos actual.
- `db.dropDatabase();`: Elimina la base de datos actual.
- `db.collection.drop();`: Elimina una colección específica.

## Operaciones de Inserción y Actualización

Para insertar y actualizar documentos en una colección, se emplean las siguientes operaciones:

- `db.collection.insertOne({...});`: Inserta un solo documento en la colección.
- `db.collection.insertMany([...]);`: Inserta múltiples documentos en la colección.
- `db.collection.updateOne({...}, {$set: {...}});`: Actualiza un solo documento que cumple con los criterios especificados.
- `db.collection.updateMany({...}, {$inc: {...}});`: Actualiza múltiples documentos incrementando valores.
- `db.collection.replaceOne({...}, {...});`: Reemplaza un solo documento que cumple con los criterios especificados.

## Operaciones de Eliminación

Para eliminar documentos de una colección, se utilizan las siguientes operaciones:

- `db.collection.deleteOne({...});`: Elimina un solo documento que cumple con los criterios especificados.
- `db.collection.deleteMany({...});`: Elimina múltiples documentos que cumplen con los criterios especificados.

## Consultas Avanzadas y Operadores

En MongoDB, se pueden realizar consultas avanzadas y utilizar diversos operadores para filtrar y manipular datos:

- Operadores de comparación: `$eq`, `$ne`, `$gt`, `$gte`, `$lt`, `$lte`.
- Operadores lógicos: `$and`, `$or`, `$not`.
- Operadores de existencia y tipo: `$exists`, `$type`.
- Operadores de expresiones regulares: `$regex`.
- Operadores para arrays: `$in`, `$nin`, `$elemMatch`, `$size`.
- Operadores aritméticos: `$add`, `$subtract`, `$multiply`, `$divide`, `$mod`.

Estos operadores se utilizan dentro de consultas para realizar operaciones matemáticas, de comparación y lógicas en los valores de los campos.