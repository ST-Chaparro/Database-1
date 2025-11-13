# Laboratorio 3

Brayan Stiven Chaparro Cataño

### Actividad  #1


### Introducción

Se va a realizar uso de comando DDL para la creación de la base de datos basandonos en el diagrama ER.
Tambien usamos DML para insertar registros a la tabla y hacer uso de los comandos DQL.


### comandos DDL

1. Creación de base de datos.

```sql
CREATE DATABASE ecommerce;
```

2. Creación de tabla `Categorias`.

```sql
CREATE TABLE Categorias(
    categoriaID INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    descripcion VARCHAR(200) 
);
```

3. Creación de tabla `Productos`.

```sql
CREATE TABLE Productos(
    productoID INT AUTO_INCREMENT PRIMARY KEY,
    categoriaID INT NOT NULL,
    cantidad_stock INT,
    descripcion VARCHAR(500), 
    garantia DATE,
    precio DECIMAL(20,2),
    

    FOREIGN KEY (categoriaID) references Categorias(categoriaID)
);
```

4. Creación de tabla `Clientes`.

```sql
CREATE TABLE Clientes(
    clienteID INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    fecha_nacimiento DATE 
);
```

5. Creación de tabla `Calificaciones`.

```sql
CREATE TABLE Calificaciones(
    calificacionID INT AUTO_INCREMENT PRIMARY KEY,
    valoracion INT NOT NULL,
    comentario VARCHAR(300),
    fecha DATE, 
    productoID INT NOT NULL,
    clienteID INT NOT NULL,
    

    FOREIGN KEY (productoID) references Productos(productoID),
    FOREIGN KEY (clienteID) references Clientes(clienteID)
);
```

6. Creación de tabla `Pedidos`.

```sql
CREATE TABLE Pedidos(
    pedidoID INT AUTO_INCREMENT PRIMARY KEY,
    fecha DATE,
    estado VARCHAR(20),
    total decimal(20, 2) NOT NULL,
    descripcion VARCHAR(100)
    created_at DATE,
    update_at DATE,
    clienteID INT NOT NULL,
    
    
    FOREIGN KEY (clienteID) references Clientes(clienteID)
);
```

7. Creación de tabla `ProductosPedidos`.

```sql
CREATE TABLE ProductosPedidos(
    producto_pedidoID INT AUTO_INCREMENT PRIMARY KEY,
   
    productoID INT NOT NULL,
    pedidoID INT NOT NULL,
    
    FOREIGN KEY (productoID) references Productos(productoID),
    FOREIGN KEY (pedidoID) references Pedidos(pedidoID)
);
```

8. Creación de tabla `Envios`.

```sql
CREATE TABLE Envios(
    envioID INT AUTO_INCREMENT PRIMARY KEY,
    direccion VARCHAR(100) NOT NULL,
    transportista VARCHAR(100),
    numero_seguimiento VARCHAR(20) NOT NULL UNIQUE,
    fecha_entrega_estimada DATE,
    estado_envio VARCHAR(20) DEFAULT 'En proceso', 

    pedidoID INT NOT NULL,
    

    FOREIGN KEY (pedidoID) references Pedidos(pedidoID),

);
```

9. Creación de tabla `telefonos_clientes`.

```sql
CREATE TABLE telefonos_clientes(
    telefonoID INT AUTO_INCREMENT PRIMARY KEY,
    clienteID INT NOT NULL,
    telefono VARCHAR(20) NOT NULL,
    
    FOREIGN KEY (clienteID) references Clientes(clienteID)
);
```


10. Creación de tabla `email_clientes`.

```sql
CREATE TABLE email_clientes(
    emailID INT AUTO_INCREMENT PRIMARY KEY,
    clienteID INT NOT NULL,
    email VARCHAR(100) NOT NULL,
    
    FOREIGN KEY (clienteID) references Clientes(clienteID)
);
```

11. Creación de tabla `direcciones_clientes`.

```sql
CREATE TABLE direcciones_clientes(
    direccionID INT AUTO_INCREMENT PRIMARY KEY,
    clienteID INT NOT NULL,
    direccion VARCHAR(220) NOT NULL,
    
    FOREIGN KEY (clienteID) references Clientes(clienteID)
);
```
