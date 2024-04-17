## **Actividad de Evaluación: Práctica de Agregaciones**

### **Consultas**

1. **Cuenta los productos de tipo “medio”, usando un método básico**
   ```mongosh
   db.productos.count({ tipo: "medio" })
   ```

2. **Indica con un distinct las empresas (fabricantes) que hay en la colección**
   ```mongosh
   db.productos.distinct("fabricante")
   ```

3. **Usando aggregate, visualiza los productos que tengan más de 80 unidades**
   ```mongosh
   db.productos.aggregate([
       { $match: { unidades: { $gt: 80 } } }
   ])
   ```

4. **Con $project, visualiza solo el nombre, unidades y precio de los productos que tengan menos de 10 unidades**
   ```mongosh
   db.productos.aggregate([
       { $match: { unidades: { $lt: 10 } } },
       { $project: { nombre: 1, unidades: 1, precio: 1, _id: 0 } }
   ])
   ```

5. **Con $project, muestra el fabricante con el nombre “empresa”**
   ```mongosh
   db.productos.aggregate([
       { $match: { unidades: { $lt: 10 } } },
       { $project: { nombre: 1, unidades: 1, precio: 1, empresa: "$fabricante", _id: 0 } }
   ])
   ```

6. **Añade un campo calculado llamado "total" que multiplique precio por unidades**
   ```mongosh
   db.productos.aggregate([
       { $match: { unidades: { $lt: 10 } } },
       { $project: { nombre: 1, unidades: 1, precio: 1, empresa: "$fabricante", total: { $multiply: ["$precio", "$unidades"] }, _id: 0 } }
   ])
   ```

7. **Haz que el nombre salga en mayúsculas con el operador $toUpper**
   ```mongosh
   db.productos.aggregate([
       { $project: { nombre_en_mayusculas: { $toUpper: "$nombre" } } }
   ])
   ```

8. **Añade un campo calculado llamado “completo” que contenga el nombre del producto y el tipo concatenado**
   ```mongosh
   db.productos.aggregate([
       { $project: { completo: { $concat: ["$nombre", " - ", "$tipo"] } } }
   ])
   ```

9. **Ordena el resultado por el campo “total”**
   ```mongosh
   db.productos.aggregate([
       { $sort: { total: 1 } }
   ])
   ```

10. **Consulta el número de productos por tipo de producto**
    ```mongosh
    db.productos.aggregate([
        { $group: { _id: "$tipo", count: { $sum: 1 } } }
    ])
    ```

11. **Añade el valor mayor y el menor**
    ```mongosh
    db.productos.aggregate([
        { $group: { _id: null, max_precio: { $max: "$precio" }, min_precio: { $min: "$precio" } } }
    ])
    ```

12. **Añade el total de unidades por cada tipo**
    ```mongosh
    db.productos.aggregate([
        { $group: { _id: "$tipo", total_unidades: { $sum: "$unidades" } } }
    ])
    ```

13. **Usa el operador $set y el operador “$substr” para visualizar datos del producto "Small Metal Tuna" y los primeros 5 caracteres del nombre**
    ```mongosh
    db.productos.aggregate([
        { $match: { nombre: "Small Metal Tuna" } },
        { $project: { datos_producto: "$$ROOT", primeros_5_caracteres_nombre: { $substr: ["$nombre", 0, 5] } } }
    ])
    ```

14. **Crea una salida con el nombre del artículo y el total (precio por unidades) y guárdalo en una colección denominada productos2**
    ```mongosh
    db.productos.aggregate([
        { $project: { nombre: 1, total: { $multiply: ["$precio", "$unidades"] } } },
        { $out: "productos2" }
    ])
    ```

15. **Comprueba que se ha creado la colección productos2**
    ```mongosh
    db.productos2.find()
    ```

---
