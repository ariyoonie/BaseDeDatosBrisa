# Visualización de Bases de Datos y Selección

Para visualizar todas las bases de datos disponibles y seleccionar una específica para su uso, se ejecutan los siguientes comandos:

```mongodb
* show dbs; 
* use practica1;
```

## Resultado:
![Visualización de Bases de Datos](https://cinecity.space/Imagenes/Cap1.png)

# Creación y Listado de Colecciones

Para crear una nueva colección dentro de la base de datos actual y listar todas las colecciones existentes en ella, se emplean los siguientes comandos:

```mongodb
* db.createCollection("facturas");
* show collections;
```

## Resultado:
![Creación y Listado de Colecciones](https://cinecity.space/Imagenes/Cap2.png)

# Inserción de Documentos en una Colección

Para intentar insertar un documento vacío en la colección "productos", se utiliza el siguiente comando:

```mongodb
* db.productos.insertOne();
```

## Resultado:
![Inserción de Documentos](https://cinecity.space/Imagenes/Cap3.png)

# Eliminación de Documentos en una Colección

Para intentar eliminar un documento de la colección "productos", se emplea el siguiente comando:

```mongodb
* db.productos.deleteOne();
```

## Resultado:
![Eliminación de Documentos](https://cinecity.space/Imagenes/Cap4.png)

# Visualización de Documentos en una Colección

Para visualizar todos los documentos en la colección "facturas", se utiliza el siguiente comando:

```mongodb
* db.facturas.find();
```

## Resultado:
![Visualización de Documentos](https://cinecity.space/Imagenes/Cap5.png)

# Consultas en la Colección de Empleados

Estas consultas específicas se realizan en la colección "empleados".

## Consulta General

Para obtener todos los documentos en la colección "empleados", se ejecuta el siguiente comando:

```mongodb
* db.empleados.find();
```

## Resultado:
![Consulta General](https://cinecity.space/Imagenes/Cap6.png)

## Consulta por Empresa (Google)

Para buscar todos los documentos donde el campo "empresa" sea igual a "Google", se usa:

```mongodb
* db.empleados.find({"empresa":{$eq:"Google"}});
```

## Resultado:
![Consulta por Empresa (Google)](https://cinecity.space/Imagenes/Cap7.png)

## Consulta por País (Perú)

Para buscar todos los documentos donde el campo "pais" sea igual a "Perú", se emplea:

```mongodb
* db.empleados.find({"pais": {$eq: "Peru"}});
```

## Resultado:
![Consulta por País (Perú)](https://cinecity.space/Imagenes/Cap8.png)

## Consulta por Salario (Mayor a 8000)

Para obtener todos los documentos donde el campo "salario" sea mayor que 8000, se usa:

```mongodb
* db.empleados.find({"salario": {$gt:8000}});
```

## Resultado:
![Consulta por Salario (Mayor a 8000)](https://cinecity.space/Imagenes/Cap9.png)

## Consulta por Ventas (Menor a 10000)

Para obtener todos los documentos donde el campo "ventas" sea menor que 10000, se emplea:

```mongodb
* db.empleados.find({"ventas": {$lt:10000}});
```

## Resultado:
![Consulta por Ventas (Menor a 10000)](https://cinecity.space/Imagenes/Cap10.png)

## Primer Documento con Ventas Menores a 10000

Para obtener el primer documento que cumpla la condición de que "ventas" sea menor que 10000, se utiliza:

```mongodb
* db.empleados.findOne({"ventas": {$lt:10000}});
```

## Resultado:
![Primer Documento con Ventas Menores a 10000](https://cinecity.space/Imagenes/Cap11.png)

## Consulta por Empresa (Google o Yahoo)

Para obtener todos los documentos donde el campo "empresa" sea "Google" o "Yahoo", se ejecuta:

```mongodb
* db.empleados.find({$or:[{"empresa": "Google"}, {"empresa": "Yahoo"}]});
```

## Resultado:
![Consulta por Empresa (Google o Yahoo)](https://cinecity.space/Imagenes/Cap12.png)

## Consulta por Empresa (Google o Yahoo) Usando $in

Similar al anterior, busca documentos donde el campo "empresa" esté dentro de una lista que contiene "Google" o "Yahoo":

```mongodb
* db.empleados.find({"empresa": {$in:["Google","Yahoo"]}});
```

## Resultado:
![Consulta por Empresa (Google o Yahoo) con $in](https://cinecity.space/Imagenes/Cap13.png)

## Consulta por Empresa (Amazon) y Salario (Mayor a 9000)

Para buscar documentos donde la "empresa" sea "Amazon" y el "salario" sea mayor que 9000, se usa:

```mongodb
* db.empleados.find({$and:[{"empresa":{$eq:"Amazon"}},{"salario":{$gt:9000}}]});
```

## Resultado:
![Consulta por Empresa (Amazon) y Salario (Mayor a 9000)](https://cinecity.space/Imagenes/Cap14.png)

## Consulta Combinada (Yahoo y Salario Mayor a 6000 o Google y Ventas Menores a 20000)

Para realizar una consulta más compleja, buscando documentos donde la empresa sea "Yahoo" y el salario sea mayor que 6000, o donde la empresa sea "Google" y las ventas sean menores que 20000, se utiliza:

```mongodb
* db.empleados.find({$or: [{$and: [{empresa: "Yahoo"}, {salario: {$gt:6000}}]},{$and:[{empresa: "Google"}, {ventas: {$lt:20000}}]}]});
```

## Resultado:
![Consulta Combinada](https://cinecity.space/Imagenes/Cap15.png)

## Consulta Específica (Campos Específicos)

Para obtener todos los documentos, pero solo incluyendo los campos "nombre", "apellidos" y "pais", excluyendo el campo "_id", se ejecuta:

```mongodb
* db.empleados.find({},{_id:0,nombre:1, apellidos:1,pais:1});
```

## Resultado:
![Consulta Específica](https://cinecity.space/Imagenes/Cap16.png)