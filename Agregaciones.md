# Agregaciones en MongoDB

En MongoDB, las agregaciones son operaciones que permiten procesar datos de manera flexible y realizar análisis avanzados en colecciones. A continuación, se detallan algunas de las operaciones más comunes utilizadas en las agregaciones:

## Operaciones de Agregación

1. `$match`: Filtra documentos de entrada y pasa solo los documentos que coinciden con las condiciones especificadas.
2. `$group`: Agrupa documentos por un campo específico y permite realizar cálculos de agregación en los grupos resultantes.
3. `$project`: Permite especificar los campos que deseas incluir en la salida y excluir los que no necesitas.
4. `$limit`: Limita el número de documentos que se pasan a la etapa siguiente en la tubería de agregación.
5. `$skip`: Omite un número especificado de documentos y pasa el resto a la siguiente etapa de la agregación.
6. `$sort`: Ordena los documentos de entrada según un criterio especificado y pasa los documentos ordenados a la siguiente etapa de la agregación.
7. `$unwind`: Descompone un campo de matriz en documentos individuales, creando un documento para cada elemento de la matriz.
8. `$lookup`: Realiza una "unión" entre dos colecciones, recuperando documentos de una colección secundaria y agregándolos a los documentos de la colección principal.
9. `$group` con operadores de acumulación: Permite realizar operaciones de agregación como sumas, promedios, mínimos, máximos, etc., en los valores de los campos agrupados.

## Ejemplos de Agregaciones

### Agregación Match y Project

Este conjunto de comandos realiza una agregación en la colección, primero filtrando los documentos con la editorial "Biblio" y luego proyectando solo los campos específicos.

```mongodb
[
  {
    $match: {
      editorial: "Biblio"
    }
  },
  {
    $project: {
      id: 0,
      titulo: 1,
      precio: 1,
      NombreEditorial: "$editorial"
    }
  }
]
```

### Agregación Group Sort

Este conjunto de comandos realiza una agregación en la colección, agrupando por editorial y contando el número de documentos, luego ordenando por el número de documentos de manera ascendente.

```mongodb
[
  {
    $group: {
      _id: "$editorial",
      "Número Documentos": {
        $count: {}
      }
    }
  },
  {
    $sort: {
      "Número Documentos": 1
    }
  }
]
```

### Agregación Match, Project y Sort

Este conjunto de comandos realiza una agregación en la colección, primero filtrando los documentos con la editorial "Biblio", luego proyectando campos específicos y calculando la ganancia total por documento, y finalmente ordenando por el precio de manera ascendente.

```mongodb
[
  {
    $match: {
      editorial: "Biblio"
    }
  },
  {
    $project: {
      _id: 0,
      titulo: 1,
      precio: 1,
      cantidad: 1,
      "Nombre Editorial": "$editorial",
      "Total Ganancia": {
        $multiply: ["$precio", "$cantidad"]
      }
    }
  },
  {
    $sort: {
      precio: 1
    }
  }
]
```

### Máximo de Grupo

Este conjunto de comandos realiza una agregación en la colección, agrupando por editorial y calculando el número de documentos, el precio promedio y el precio máximo, luego ordena por el precio máximo de manera ascendente.

```mongodb
[
  {
    $group: {
      _id: "$editorial",
      "Número de Documentos": {
        $count: {}
      },
      media: {
        $avg: "$precio"
      },
      "Precio Máximo": {
        $max: "$precio"
      }
    }
  },
  {
    $sort: {
      "Precio Máximo": 1
    }
  }
]
```

### Set Out

Este conjunto de comandos realiza una agregación en la colección, agrupando por editorial y calculando el número de documentos y el precio promedio, luego redondea la media y guarda los resultados en una nueva colección llamada "Media_Editoriales".

```mongodb
[
  {
    $group: {
      _id: "$editorial",
      Numero: {
        $count: {}
      },
      media: {
        $avg: "$precio"
      }
    }
  },
  {
    $set: {
      "Media Total": {
        $trunc: ["$media", 2]
      }
    }
  },
  {
    $out: "Media_Editoriales"
  }
]
```

### Set Unset

Este conjunto de comandos realiza una agregación en la colección, agrupando por editorial y calculando el número de documentos y el precio promedio, luego elimina el campo "media" del resultado final.

```mongodb
[
  {
    $group: {
      _id: "$editorial",
      Numero: {
        $count: {}
      },
      media: {
        $avg: "$precio"
      }
    }
  },
  {
    $set: {
      "Media Total": {
        $trunc: ["$media", 2]
      }
    }
  },
  {
    $unset: "media"
  }
]
```