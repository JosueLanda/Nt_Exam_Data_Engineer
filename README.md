# Prueba técnica : Data Engineer

### Paso 1.- Levantamiento de Docker
Entrar a la carpeta Docker_Mysql_Postgres y construir el docker (Docker_Mysql_Postgres/docker-compose.yml) con el siguiente comando :
```sh
 docker-compose up -d
```
### Paso 2.- Creación del venv
Correr en terminal los siguientes comandos para la creación del ambiente para poder ejecutar el archivo .ipynb (Data Pipeline)
Nota.- Se tiene que buscar la ruta en donde esta el .ipnb 
```sh
 python3 -m venv examen_data
 cd bin
 source activate
 pip install -r requirements.txt
 jupyter notebook
```

### Paso 3.- Creación de Tablas 
Para que el flujo de datos sea correcto , se necesitan crear las siguientes tablas , la primera en MySQL y la segunda en PostgreSQL

MySQL
```sql
CREATE DATABASE DATABASE_EXAMEN;

USE DATABASE_EXAMEN;

CREATE TABLE FINAL_TABLE (
id varchar(255) NOT NULL,
company_name varchar(130) NULL,
company_id varchar(255) NULL,
amount double NULL,
status varchar(30) NULL,
created_at timestamp NOT NULL,
updated_at timestamp NULL
);
```
PostgreSQL
```sql
CREATE DATABASE DATABASE_EXAMEN;
```
Nota.- Se puede usar el Database Manager de preferencia para correr las consultas o desde línea de comandos
### Paso 4.- Correr el notebook
Se necesita correo el Data Pipeline para tener los resultados en las bases de datos.
### Paso 5.- Creación de vista
Se necesita crear la vista con la siguiente consulta
```sql
CREATE VIEW vista_final AS SELECT A.company_name,SUM(A.amount) FROM 
  (SELECT * FROM charges
  INNER JOIN companies
  ON charges.company_id = companies.company_id
  ) AS A
GROUP BY A.company_name;
```
### Acerca de Notebook_Data_Pipeline/Data Pipeline.ipynb
Contiene todo el desarrollo del Data_Pipeline 

