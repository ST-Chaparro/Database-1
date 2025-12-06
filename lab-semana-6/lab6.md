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

 id CREATE TABLE clients (
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

  FOREIGN KEY (client_id) REFERENCES Clients(client_id),

);