# Tutorial de SQL
## Que es una base de datos

Una base de datos, database (db), es cualquier colección de información relacionada o de interés. 

## Sistemas de admon de bases de datos

En inglés, **Database Management Systems (DBMS)** es un programa que ayuda al usuario a crear y mantener una base de datos:
+ Facilita la manipulación de grandes cantidades de información.
+ Administra temas de seguridad (Control de acceso).
+ Permite realizar backups.
+ Se puede importar y exportar datos.
+ Interacción con aplicaciones de software.

## C.R.U.D
Siglas para:
+ Create -> Crear.
+ Read -> Leer.
+ Update -> Actualizar.
+ Delete -> Eliminar.

Son las 4 operaciones típicas que se realizan en una base de datos.

## Tipos de bases de datos
### Base de datos relacional (SQL)
Se organizan los datos en una o más tablas:
+ Cada tabla tiene columnas y filas.
+ Una **llave única** identifica a cada fila.
### Base de de datos no relacional (noSQL / not just SQL)
Se organiza los datos de cualquier manera menos de la forma tradicional:
+ Almacenamiento **clave-valor**.
+ Documentos (JSON, XML,...)
+ Grafos.
+ Tablas flexibles.

## Bases de datos relacionales (SQL)
### Sistema o motor de administración de bases de datos **relacionales** (RDBMS)
Ayuda a crear y mantener bases de datos relacionales:
+ MySQL.
+ Oracle.
+ PostreSQL.
+ MariaDB.

Los RDBMS utilizan SQL (lenguaje de consulta estructurado):
+ Lenguaje estandarizado para trabajar con RDBMS.
+ Permite realizar operaciones CRUD, así como otras tareas relacionadas con administración de usuarios, seguridad, backups.
+ Se usa para definir tablas y estructuras.
+ Existen algunas diferencias dependiendo del tipo de RDBMS que se utilice.

## Bases de datos no relacionales (noSQL)
### Sistema o motor de administración de bases de datos **no relacionales** (NRDBMS)

Ayuda a crear y mantener bases de datos NO relacionales:
+ mongoDB.
+ dynamoDB.
+ Apache cassandra.
+ Firebase.

La implementación en este caso es específica:
+ La mayoria de NRDBMS  implementa su propio lenguaje para realizar tareas CRUD y demás.

## Consultas a la base de datos - Database queries

Una consulta (query) es una petición que se le hace al DBMS por información específica. A medida que la estructura de la base de datos se vuelve más compleja, es más complicado obtener información específica.

# Tablas y llaves

Students
| <u>Student_id</u>  | name  | major  |
|---|---|---|
| 1 | Jack | Biology  |
| 2 |  Kate | Sociology  |
| 3 |  Claire | English  |
| 4 |  Jack | Biology  |
| 5 |  Mike | Comp. Sci  |

Columna: Define un atributo: nombre, major.

Fila: Muestra, observación.

**LLave primaria**: En este caso es Student_id, identifica una única vez a cada muestra de la tabla. En el ejemplo, se puede diferenciar a los estudiantes Jack que son biologos gracias a la llave primaria.

La llave primaria puede ser un número, un string o cualquier otra cosa, pero siempre debe ser un identificador único e irrepetible.

+ Surrogate Key: La llave primaria puede no representar un valor de la realidad. Por ejemplo id = 100, 101, 102... 

+ Natural Key: Una llave primaria natural es creada con información real propia de la tabla, por ejemplo una cédula o un código estudiantil.

* Foreign Key: Contiene la información de la llave primaria de una tabla almacenada en otra tabla. A través de estas se establecen relaciones entre tablas.

Una tabla puede tener más de una llave foránea.

Una llave primaria puede estar compuesta por 2 ó más columnas. Esto puede deberse a que las columnas individuales no permiten identificar con valores únicos e irrepetibles cada registro de la tabla.

Una llave primaria puede estar compuesta por 2 ó más llaves foráneas.

# SQL 

Las implementaciones SQL varia según el RDBMS que se utilice, pero los conceptos se mantienen.

En realidad es un lenguaje híbrido. Se compone de 4 lenguajes:
1. Data Query Language (DQL):
    + Se usa para consultar información en la db.
    + Obtener info que ya está almacenada.
2. Data Definition Language (DDL):
    + Definir esquemas para la base de datos.
3. Data Control Language (DCL):
    + Usada para controlar el  acceso a la base de datos.
    + Administración de permisos y usuarios.
4. Data Manipulation Language (DML):
    + Usado para insertar, actualizar y borrar datos en la db.

## Query

Instrucciones dadas al RDBSM para obtener información de interés. Tener en cuenta que en una base de datos puede haber mucha información, en algunos casos oculta en esquemas complejos, donde el objetivo es obtener los datos correctos.

# MySQL
Crear una nueva base de datos, en MySQL command line:
```SQL
create database <database_name>;
```
## Tipos de datos:
Existen los siguientes tipos de datos, en general, disponibles en SQL:
+ **INT**: Números enteros
+ **DECIMAL (M,N)**
    + M: Cantidad TOTAL de dígitos.
    + N: Cantidad de dígitos después de la coma.
+ **VARCHAR(x)**: Cadena de texto de tamaño x.
+ **BLOB**: Binary large object. Sirve para almacenar datos grandes.
+ **DATE**: Formato 'YYYY-MM-DD'.
+ **TIMESTAMP**: Formato 'YYYY-MM-DD HH:MM:SS' Utilizada para registrar algún evento de interés.

## Crear una tabla
```sql
CREATE TABLE <table_name> (
    <column_name> INT PRIMARY KEY,
    <column_name>  VARCHAR(20),
    <column_name>  VARCHAR(20)
);
```
Produce lo mismo qué:
```sql
CREATE TABLE student (
    student_id INT,
    name VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY(student_id)
);
```
Para ver información básica de la tabla creada:
```sql
DESCRIBE <table_name>;
```
Para borrar una tabla:
```sql
DROP TABLE <table_name>;
```

Modificar una tabla ya creada, agregando una nueva columna:
```sql
ALTER TABLE student ADD gpa DECIMAL(3, 2);
```
Modificar una tabla ya creada, eliminando una columna:
```sql
ALTER TABLE <table_name> DROP <column_name>;
```

## Insertar datos
Se ingresan por fila, respetando el orden las columnas:
```sql
INSERT INTO student VALUES(1, 'Jack', 'Biology');
```
Leer toda la info de una tabla:
```sql
SELECT *  FROM student;
```
Insertar info para columnas específicas:
```sql
INSERT INTO student (student_id, name) VALUES(3, 'Claire');
```

### Constraints - Limitaciones
Otra forma de crear una tabla limitando valores por columna:
```sql
CREATE TABLE student (
    student_id INT,
    name VARCHAR(20) NOT NULL --No admite valores nulos,
    major VARCHAR(20) UNIQUE -- No admite valores repetidos,
    PRIMARY KEY (student_id)
);
```
En particular, una llave primario **NO** admite valores nulos ni duplicados.

Se puede especificar un valor por defecto en caso de que no se tenga el dato:
```sql
CREATE TABLE student (
    student_id INT,
    name VARCHAR(20),
    major VARCHAR(20) DEFAULT 'undecided', --Valor por defecto
    PRIMARY KEY (student_id)
);
```
La llave primaria puede incrementarse de manera automática:
```sql
CREATE TABLE student(
    student_id INT AUTO_INCREMENT,
    name VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY(student_id)
);
```

## Actualizar y borrar

Actualizando el valor de una columna:
```sql
UPDATE student 
SET major = 'Bio' --Nuevo valor
WHERE major = 'Biology';--Condición
```
Existen los siguientes operadores de comparación:
```sql
= --igual que
<> -- Diferente que
> -- Mayor que
< -- Menor que
>= --Mayor o igual que
<= -- Menor o igual que 
```

Se puede incluir varias condiciones:
```sql
UPDATE student 
SET major = 'Biochemistry'
WHERE major = 'Bio' OR
      major = 'Chemistry';
```
Sin la sentencia WHERE, todos los registros se ven afectados:
```SQL
UPDATE student
SET major = 'undecided';
```

Borrando un registro de la tabla:
```sql
DELETE FROM student
WHERE student_id = 5;
--Si no se coloca WHERE, se borran todos los registros
```

## Consultas básicas

Leer una columna específica:
```sql
SELECT name
FROM student;
--
SELECT name, major
FROM student;
--
SELECT student.name, student.major
FROM student
ORDER BY name; --Orden ascendente
--
SELECT student.name, student.major
FROM student
ORDER BY student_id DESC; --Orden descendente
--
SELECT * 
FROM student
ORDER BY major, student_id; 
-- Ordenando primero por major, si hay  2 major iguales
-- ordena por student_id

---------------------------------------------------------------
SELECT * 
FROM student
ORDER BY major DESC, student_id DESC; -- Ambos ordenes en orden descendente


SELECT name, major
FROM student
WHERE major = 'Chemistry' OR major <> 'Biology'
ORDER BY student_id
LIMIT 2;

SELECT *
FROM student
WHERE name IN ('Claire', 'Jack'); --Valores dentro de una lista
```

# Ejemplo - Company Database

En primer lugar se crean las tablas, únicamente definiendo las llaves primarias de cada una:
```sql
CREATE TABLE employee(
    emp_id INT PRIMARY KEY, 
    first_name VARCHAR(40),
    last_name VARCHAR(40),
    birth_day DATE,
    sex VARCHAR(1),
    salary INT,
    super_id INT, 
    branch_id INT 
);

CREATE TABLE branch(
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(40),
    mgr_id INT,
    mgr_start_date DATE,
    FOREIGN KEY(mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);

-- Definiendo clave foránea en una tabla ya creada:
ALTER TABLE employee
ADD FOREIGN KEY(branch_id)
REFERENCES branch(branch_id)
ON DELETE SET NULL;

ALTER TABLE employee
ADD FOREIGN KEY(super_id)
REFERENCES employee(emp_id)
ON DELETE SET NULL;

CREATE TABLE client(
    client_id INT PRIMARY KEY,
    client_name VARCHAR(40),
    branch_id INT,
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id)
    ON DELETE SET NULL
);

CREATE TABLE works_with(
    emp_id INT,
    client_id INT,
    total_sales INT,
    PRIMARY KEY(emp_id, client_id), --LLAVE COMPUESTA
    FOREIGN KEY(emp_id) REFERENCES employee(emp_id) ON DELETE CASCADE,
    FOREIGN KEY(client_id) REFERENCES  client(client_id) ON DELETE CASCADE
);

CREATE TABLE branch_supplier(
    branch_id INT,
    supplier_name VARCHAR(40),
    supply_type VARCHAR(40),
    PRIMARY KEY(branch_id, supplier_name),
    FOREIGN KEY(branch_id) REFERENCES branch(branch_id) ON DELETE CASCADE
);

--AGREGANDO REGISTROS

INSERT INTO employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);


INSERT INTO branch VALUES(1,'Corporate', 100, '2006-02-09');

UPDATE employee
SET branch_id = 1
WHERE emp_id = 100;

INSERT INTO employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);

-- Scranton
INSERT INTO employee VALUES(102, 'Michael', 'Scott', '1964-03-15', 'M', 75000, 100, NULL);

INSERT INTO branch VALUES(2, 'Scranton', 102, '1992-04-06');

UPDATE employee
SET branch_id = 2
WHERE emp_id = 102;

INSERT INTO employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);
INSERT INTO employee VALUES(104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, 2);
INSERT INTO employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);

-- Stamford
INSERT INTO employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL);

INSERT INTO branch VALUES(3, 'Stamford', 106, '1998-02-13');

UPDATE employee
SET branch_id = 3
WHERE emp_id = 106;

INSERT INTO employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);
INSERT INTO employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);


-- BRANCH SUPPLIER
INSERT INTO branch_supplier VALUES(2, 'Hammer Mill', 'Paper');
INSERT INTO branch_supplier VALUES(2, 'Uni-ball', 'Writing Utensils');
INSERT INTO branch_supplier VALUES(3, 'Patriot Paper', 'Paper');
INSERT INTO branch_supplier VALUES(2, 'J.T. Forms & Labels', 'Custom Forms');
INSERT INTO branch_supplier VALUES(3, 'Uni-ball', 'Writing Utensils');
INSERT INTO branch_supplier VALUES(3, 'Hammer Mill', 'Paper');
INSERT INTO branch_supplier VALUES(3, 'Stamford Lables', 'Custom Forms');


-- CLIENT
INSERT INTO client VALUES(400, 'Dunmore Highschool', 2);
INSERT INTO client VALUES(401, 'Lackawana Country', 2);
INSERT INTO client VALUES(402, 'FedEx', 3);
INSERT INTO client VALUES(403, 'John Daly Law, LLC', 3);
INSERT INTO client VALUES(404, 'Scranton Whitepages', 2);
INSERT INTO client VALUES(405, 'Times Newspaper', 3);
INSERT INTO client VALUES(406, 'FedEx', 2);

-- WORKS_WITH
INSERT INTO works_with VALUES(105, 400, 55000);
INSERT INTO works_with VALUES(102, 401, 267000);
INSERT INTO works_with VALUES(108, 402, 22500);
INSERT INTO works_with VALUES(107, 403, 5000);
INSERT INTO works_with VALUES(108, 403, 12000);
INSERT INTO works_with VALUES(105, 404, 33000);
INSERT INTO works_with VALUES(107, 405, 26000);
INSERT INTO works_with VALUES(102, 406, 15000);
INSERT INTO works_with VALUES(105, 406, 130000);
```

# Consultas Básicas
```sql
-- Seleccionar columnas y cambiarles el nombre
SELECT first_name as forename, last_name as surname
FROM employee
-- Seleccionar los DIFERENTES valores de una columna
SELECT DISTINCT sex
from employee;
```

# Funciones

Bloque de código que realiza alguna tarea particular:
```sql
-- Encontrar cantidad de empleados 
SELECT COUNT(emp_id)
FROM employee;

--Encontrar cantidad de empleados con supervisor
SELECT COUNT(super_id)
FROM employee;

--Empleadas (F) que nacieron después de 1970
SELECT COUNT(emp_id) as Resultado
FROM employee
WHERE employee.sex = 'F' AND
employee.birth_day > '1971-01-01';


-- PROMEDIO DE UN SALARIO
SELECT AVG(salary)
FROM employee
WHERE sex = 'M';

-- SUMA DE LOS SALARIOS
SELECT SUM(salary)
FROM  employee;

--  Calcular la cantidad de hombres y mujeres
SELECT COUNT(sex), sex
FROM employee
GROUP BY sex;

--AGREGACIONES

-- Total de ventas($) por cada vendedor
SELECT emp_id, SUM(total_sales)
FROM works_with
GROUP BY emp_id;

-- Total de ventas($) por cliente
SELECT client_id, SUM(total_sales)
FROM works_with
GROUP BY client_id;
```

# Wildcard - comodines

Utilizado para generar comodines en expresiones regulares:
+ %: Cualquier cantidad de caracteres.
+ _: Un caracter
```sql

SELECT *
FROM client
WHERE client_name LIKE '%LLC'; --LLC al final de x caracteres

SELECT *
FROM branch_supplier
WHERE  supplier_name LIKE '% Labels%';


SELECT * 
FROM employee
WHERE birth_day LIKE '____-10%'; --4 caracteres para el año

SELECT *
FROM client 
WHERE client_name LIKE '%school%';
```

# Unión

Combinar resultados de multiples SELECT en un solo resultado.
+ Se debe tener la MISMA cantidad de columnas
+ Deben tener tipos de datos iguales
```sql
SELECT first_name AS Company_names 
FROM employee
UNION -- Union x columna
SELECT branch_name
FROM branch
UNION 
SELECT client_name
FROM client;

SELECT client_name, client.branch_id 
FROM client
UNION 
SELECT supplier_name, branch_supplier.branch_id
FROM branch_supplier;

SELECT salary 
FROM employee
UNION
SELECT total_sales
FROM works_with;
```

# JOINS

Combinar información de múltiples columnas comunes.
Existen varios tipos:
+ JOIN (INNER JOIN).
+ LEFT JOIN.
+ RIGHT JOIN.
+ FULL OUTTER JOIN.
```SQL

SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee -- A 
INNER JOIN branch --  B 
--A intersección B
ON employee.emp_id = branch.mgr_id;--condición


SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee -- Todos sus registros se incluyen
lEFT JOIN branch  --Se agrega info de B en A
ON employee.emp_id = branch.mgr_id;-- Condición


SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee --Se agrega info de A en B
RIGHT JOIN branch -- Todos sus registros se incluyen
ON employee.emp_id = branch.mgr_id;

--Existe el full outter join, incluye todo
```
# Consultas anidadas

```sql
SELECT first_name, last_name
FROM employee
WHERE employee.emp_id IN(
    SELECT emp_id
    FROM Works_with
    WHERE total_sales > 30000);
```
MySQL resuelve una consulta anidada comenzando por la "más profunda" hasta la más general:
```sql
SELECT client.client_name--Se resuelve al final
FROM client
WHERE Client.branch_id = (
    SELECT branch.branch_id --Se resuelve primero
    FROM branch
    WHERE branch.mgr_id = 102
    LIMIT 1); --conviene ponerlo
```
# On delete
Al eliminar un registro que tiene presente una llave foránea, ¿que sucede?.

Hay dos opciones
```SQL
ON DELETE SET NULL --Deja el dato como NULL
ON DELETE CASCADE --Se elimina toda la fila

DELETE FROM employee
WHERE emp_id = 102;
```
SET NULL es útil cuando la información eliminada no es relevante. En caso de que, por ejemplo, una llave foránea sea una de las que compone una llave primaria, si es necesario eliminar todo el registro con CASCADE.

# Triggers

Eventos que ocurren cuando se realiza alguna consulta en la base de datos. En MySQL es necesario cambiar el delimitador para poder definir los triggers de manera correcta:
```sql
DELIMITER $$ --Cambia el delimitador (; por defecto)
CREATE 
TRIGGER my_trigger BEFORE INSERT --Puede ser AFTER
ON employee
FOR EACH ROW BEGIN
INSERT INTO trigger_test VALUES("Added new employee");
END $$
DELIMITER;

DELIMITER $$ --Cambia el delimitador (; por defecto)
CREATE 
TRIGGER my_trigger_1 BEFORE INSERT 
ON employee
FOR EACH ROW BEGIN
INSERT INTO trigger_test VALUES(NEW.first_name);
END $$
DELIMITER; 

DELIMITER $$
CREATE
	TRIGGER my_trigger_2 BEFORE INSERT
	ON employee
	FOR EACH ROW BEGIN
		IF NEW.sex = 'M' THEN
			INSERT INTO trigger_test VALUES('Added male employee');
		ELSEIF NEW.sex = 'F' THEN
			INSERT INTO trigger_test VALUES('Added female employee);
		ELSE
			INSERT INTO trigger_test VALUES('Added other employee');
		END IF;
	END$$
DELIMITER ;

DROP TRIGGER <my_trigger>; --Eliminar trigger  
```