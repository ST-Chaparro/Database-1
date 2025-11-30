# Database-1
Repositorio de laboratorios del curso Base de datos 1

## Documentación 

### Conceptos

* ¿Qué es un indice y para que sirve en base datos?

Un índice en una base de datos es una estructura de datos auxiliar (como el índice de un libro que sirve para ir directamente al contenido de nuestro interes sin necesidad de leer todo el libro) que se usa para mejorar el rendimiento de consulta de una base de datos (SELECT).S

¿Para qué sirve? Permite que el sistema encuentre filas directamente basándose en el valor de una columna (o varias), sin tener que revisar la tabla completa, lo que es esencial para consultas rápidas y uniones (JOIN) eficientes.

Lo que realiza por debajo es que el motor realiza uso de una busqueda binaria, que lo que hace es dividir la lista en dos mitades hasta que encuentre el elemento buscado

* Qué es normalización?

"Es un proceso repetitivo que nos permite aplicar una serie de reglas a nuestras relaciones, con la finalidad de evitar redundancias y garantiar la integridad de los datos"

Entendiendo la palabra clave `repetitivo` esto hace referencia que en en nuestra base de datos debemos aplicar una serie de reglas para ir eliminando redundancias.

* Para que sirve?

- Disminuir o eliminar redundancias.
- Minimizar los problemas de actualización de datos en las relaciones.
- Asegurar la integridad de los datos

### 5 Formas normales (FN)

Existen 5 reglas que podemos aplicar a las relaciones de nuestra base de datos, tres de ella fueron postuladas por Edgar F. Codd, quien fue el creador del modelo relacional.

1. Primera forma normal (1FN)

"Una relación esta en (1FN) si, y solo si, no tiene grupos repetidos."

por lo tanto y según los establecido en el modelo relacional, en una relación se debe cumplir que:

- No debe existir grupos repetitivos.
- No importa el orden.
- Debe de existir una llave primaria.
- Todos los atributos deben de ser atomicos
- No debe de tener tuplas repetidas.

### Comandos

* Realizar un consulta a los datos

`SELECT * FROM databaseName.tableName`

```sql
SELECT * FROM ecommerce.productos;
```

* Rules para los nombres de las tablas.

Usar `snake_case`

* normalize del valor  `DATE` para usar en lab ,  `año-mes-dia`. Por ejemplo, `2025-11-14`

* como renombre el nombre de una columna usando `RENAME`.

```sql
ALTER TABLE Pedidos
RENAME COLUMN update_at TO updated_at;
```
Hay otra forma que es usando `CHANGE` este es más potente ya que este permite redefinir el tipo de dato.

```sql
ALTER TABLE nameTable
CHANGE COLUMN nameOld nameNew Type_Date_New;
```
* Usar `MODIFY`

```sql
ALTER TABLE Medicos
MODIFY COLUMN nombre VARCHAR(10) NOT NULL;
```





* Agregar una columna a la tabla `ADD COLUMM` seguido del nombre y tipo de dato.

```sql
ALTER TABLE Productos
ADD COLUMN nombre VARCHAR(100) NOT NULL AFTER categoriaID;
```

El `AFTER` lo use para agregar la nueva columna despues de `categoriaID` para tener el orden que queria.

* Agregar valores a una columna o modificar un valor existente con `UPDATE`.

```sql
UPDATE Productos -- Tabla 
SET nombre = 'Colchoneta de Yoga Pro' -- valor y campo 
WHERE productoID = 1; -- condición
```


* Usando el operador `and` de `sql`.
El `AND` operador se utiliza para filtrar registros en función de más de una condición

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

* Usando `ASC`

```sql
SELECT nombre, precio_unitario
FROM medicamentos
ORDER BY precio_unitario ASC; -- Ascendente, en squl si no agrega necesariamente  por defecto es ASC. DESC(descendente) 
```





