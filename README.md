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

Conjunto de instrucciones dados al RDBSM para obtener información de interés. Tener en cuenta que en una base de datos puede haber mucha información, en algunos casos oculta en esquemas complejos, donde el objetivo es obtener los datos correctos.
