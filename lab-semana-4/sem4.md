# Laboratorio 3

Brayan Stiven Chaparro Cataño

### Actividad  #1


### Introducción

En esta actividad se va aplicar la reglas de formalización a una base de datos que contiene demasiadas redundancias, y tambien una vez finalizado crear la db corresponidente y sus tablas y generar el Diagrama ER.

### comandos DDL

1. Creación de base de datos.

```sql
CREATE DATABASE store;
```

2. Creación de tabla `Productos`.

```sql
CREATE TABLE Products(
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name_product VARCHAR(100) NOT NULL,
    unit_price Decimal(20,2)
);
```

3. Creación de tabla `Banco`.

```sql
CREATE TABLE Banks(
    bank_id INT AUTO_INCREMENT PRIMARY KEY,
    name_bank VARCHAR(100)
    
);
```

4. Creación de tabla `Clientes`.

```sql
CREATE TABLE Clients(
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    name_client VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL
);
```

5. Creación de tabla `Tarjeta`.

```sql
CREATE TABLE Cards(
    number_card VARCHAR(16) PRIMARY KEY,
    bank_id INT NOT NULL,
    client_id INT NOT NULL,
    

    FOREIGN KEY (bank_id) references Banks(bank_id),
    FOREIGN KEY (client_id) references Clients(client_id)
);
```

6. Creación de tabla `Ordenes`.

```sql
CREATE TABLE Orders (

    order_number INT PRIMARY KEY, 
    client_id INT NOT NULL,
    number_card VARCHAR(16) NOT NULL,
    date_order DATE NOT NULL,
    total_price DECIMAL(10, 2) NOT NULL,
  
    FOREIGN KEY (client_id) REFERENCES Clients(client_id),
    FOREIGN KEY (number_card) REFERENCES Cards(number_card)
);
```

7. Creación de tabla `Detalle orden`.

```sql
CREATE TABLE detail_order (
    
    order_number INT NOT NULL, 
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    
    PRIMARY KEY (order_number, product_id), -- Uso de clave compuesta
    
   
    FOREIGN KEY (order_number) REFERENCES Orders(order_number),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
```

Como resultado de la normalización y una ves llegado a la FN3.

![alt tablas ya creadas](img/ER-store.png)


### Conclusión actividad 1

El identificar cada uno de los pasos que se lleva en una base de datos que al inicio contiene muchos elementos que son redundante y como aplicanco las reglas de normalizacion podemos eliminar esta redundancia o minimizar. 

