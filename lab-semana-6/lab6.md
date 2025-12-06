 # Laboratorio 6

Brayan Stiven Chaparro Cataño

### Actividad  #1


### Introducción

En esta actividad se va realizar la creacion de la base de datos para un banco y despues realizar una serie de consultas, la creación de la base de datos se debe de tener en cuenta los requerimientos del cliente.


1. Creación db `Banco`

```sql
   CREATE DATABASE banco
```

 
2. Creación tabla ``Clientes`
 
```sql

 CREATE TABLE clients (
  client_id INT AUTO_INCREMENT PRIMARY KEY,
  dni VARCHAR(20) UNIQUE, -- Para evitar clientes repetidos
  firstname VARCHAR(100) NOT NULL,
  lastname VARCHAR(100) NOT NULL,
  sex VARCHAR(1), -- F y M
  date_bird DATE NOT NULL,
  country_resindece VARCHAR(50) NOT NULL,
  city_residence VARCHAR(50) NOT NULL,
  phone VARCHAR(20) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL

);

```

3. tabla `cuentas`


```sql

CREATE TABLE accounts (
  num_account VARCHAR(20)  PRIMARY KEY, -- Número de cuenta
  client_id INT NOT NULL,
  balance DECIMAL(15.2),
  opening_date DATE NOT NULL,
  state_account VARCHAR(50) NOT NULL DEFAULT 'Activa', -- 'Activa' o 'Inactiva'
  coin VARCHAR(10) NOT NULL, -- 'Euro'o 'Dolar'
  type_account VARCHAR(20) NOT NULL, -- 'Corriente' o 'Caja de ahorro'
  FOREIGN KEY (client_id) REFERENCES Clients(client_id)

);

```

3. tabla `historial_cuenta`


```sql

CREATE TABLE accounts_history (
  history_id INT AUTO_INCREMENT PRIMARY KEY,
  num_account VARCHAR(20) NOT NULL, -- Numero cuenta
  transaction_date DATETIME NOT NULL,
  amount DECIMAL(15, 2) NOT NULL,
  type_movement VARCHAR(20) NOT NULL, -- 'Deposito' o 'Retiro'
  medium_transfer VARCHAR(20) NOT NULL, -- 'Banco', 'Online', 'Cajero automatico'
  description_movement VARCHAR(200),
  state_operation VARCHAR(10) NOT NULL, -- 'Pendiente', 'Fallida' o 'Exitosa'


  FOREIGN KEY (num_account) REFERENCES accounts(num_account)

);

```

4. tabla `tarjetas`


```sql

CREATE TABLE cards (

  num_card VARCHAR(16) PRIMARY KEY,
  client_id INT NOT NULL, -- Numero cuenta
  code_security VARCHAR(4) NOT NULL,
  expiration_date DATE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  retire_limmit DECIMAL(10,2) NOT NULL,


  FOREIGN KEY (client_id) REFERENCES clients(client_id)

);

```

4. tabla `tarjeta cuentas`

```sql

CREATE TABLE card_account (

  num_card VARCHAR(16) NOT NULL,
  num_account VARCHAR(20) , -- Número de cuenta
  state_link  VARCHAR(10), -- 'activo', 'inactivo'
  PRIMARY KEY (num_card, num_account),

  FOREIGN KEY (num_card) REFERENCES cards(num_card),
  FOREIGN KEY (num_account) REFERENCES accounts(num_account)

);

```
5. tabla `usuario banco digital`

```sql

CREATE TABLE user_bank (

  client_id INT PRIMARY KEY,
  name_user VARCHAR(50) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  state_push BOOLEAN NOT NULL DEFAULT TRUE,

  FOREIGN KEY (client_id) REFERENCES Clients(client_id)

);
```

### Consultas

1. 

```sql

SELECT
    ah.transaction_date AS Fecha_Operacion,
    ah.amount AS Monto_Movimiento,
    ah.type_movement AS Tipo_Movimiento,
    ah.description_movement AS Descripcion,
    ah.state_operation AS Estado_Operacion,
    a.num_account AS Numero_Cuenta,
    a.coin AS Moneda,
    a.balance AS Balance_Actual_Cuenta -- El balance actual de la cuenta
FROM
    accounts_history ah
JOIN
    accounts a ON ah.num_account = a.num_account
ORDER BY
    ah.transaction_date DESC 
LIMIT 5;

```

2. 

```sql
SELECT
    C.firstname,
    C.lastname,
    CRD.num_card AS Numero_Tarjeta,
    A.num_account AS Numero_Cuenta,
    A.coin AS Moneda_Cuenta
FROM
    cards CRD
JOIN
    clients C ON CRD.client_id = C.client_id  -- Obtiene el nombre del cliente
JOIN
    card_account CA ON CRD.num_card = CA.num_card -- Vincula la tarjeta con la cuenta
JOIN
    accounts A ON CA.num_account = A.num_account -- Obtiene detalles de la cuenta (moneda)
WHERE
    CRD.num_card = '4567890123456781';

```

3. 

```sql
SELECT
    A.num_account AS Numero_Cuenta,
    A.coin AS Moneda,
    A.type_account AS Tipo_Cuenta,
    A.balance AS Balance_Actual,
    ah.amount AS Monto_Operacion,
    ah.state_operation AS Estado_Operacion,
    ah.type_movement AS Tipo_Movimiento,
    ah.transaction_date AS Fecha_Operacion
FROM
    accounts A
JOIN
    accounts_history ah ON A.num_account = ah.num_account
WHERE
    A.num_account = 'ES01' -- el número de cuenta 
ORDER BY
    ah.history_id DESC; 
```
4. 

```sql
SELECT
    type_movement AS Tipo_Movimiento,
    medium_transfer AS Medio_Transferencia,
    description_movement AS Concepto,
    state_operation AS Estado,
    amount AS Monto
FROM
    accounts_history
WHERE
    num_account = 'ES01' 
    AND amount BETWEEN 50.00 AND 500.00 -- rango 
ORDER BY
    transaction_date DESC;

```
5. 

```sql
SELECT
    medium_transfer AS Medio_Transferencia,
    description_movement AS Concepto,
    state_operation AS Estado,
    amount AS Monto
FROM
    accounts_history
WHERE
    num_account = 'ES01'
    AND type_movement = 'Retiro' 
ORDER BY
    transaction_date DESC;

```
6. 

```sql
SELECT
    num_account AS Numero_Cuenta,
    medium_transfer AS Medio_Transferencia,
    description_movement AS Concepto,
    state_operation AS Estado,
    amount AS Monto
FROM
    accounts_history
WHERE
    num_account = 'ES01'  
    AND state_operation = 'Exitosa' 
    AND amount > 100.00 
ORDER BY
    transaction_date DESC;

```
7. 

```sql
SELECT
    UB.name_user AS Nombre_Usuario_Digital,
    UB.state_push AS Estado_Notificaciones_Push,
    C.firstname AS Nombres,
    C.lastname AS Apellidos,
    C.dni AS Numero_Identidad,
    C.phone AS Telefono,
    C.email AS Correo_Electronico
FROM
    user_bank UB
JOIN
    clients C ON UB.client_id = C.client_id
WHERE
    UB.client_id = 1;

```
8. 

```sql
SELECT
    C.num_card AS Numero_Tarjeta,
    C.expiration_date AS Fecha_Vencimiento,
    C.retire_limmit AS Limite_Retiro,
    A.num_account AS Numero_Cuenta_Enlazada,
    A.coin AS Moneda_Cuenta
FROM
    cards C
JOIN
    card_account CA ON C.num_card = CA.num_card -- Conecta la tarjeta con las cuentas enlazadas
JOIN
    accounts A ON CA.num_account = A.num_account -- Obtiene los detalles (número y moneda) de las cuentas
WHERE
    C.num_card = '4567890123456781';

```
