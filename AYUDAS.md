# MySQL
Campusland MySQL
---
# Empezando aplicacion
 create database CamiloNuevo; -- esto es para crear una nueva tabla de base de datos
show databases; -- esto es para ver los r3egistros de la base de datos y saber cual se va a utilizar
use CamiloNuevo; -- Esto es para saber que base de datos se usara
 -- esto es para crear las condiciones de la tabla, el int despues del id espara que sea entero el id, el tipo varchar es para que sea texto solamente y los numeros es para la cantidad maxima de caracteres
create table animales(
id int,
tipo varchar(255),
estado varchar(255),
primary key (id)
);
-- INSERT INTO animales(tipo,estado)Values('chanchito','feliz');
ALTER TABLE animales MODIFY COLUMN id int auto_increment;
SHOW CREATE TABLE animales; 
CREATE TABLE `animales` (
  `id` int NOT NULL AUTO_INCREMENT,
  `tipo` varchar(255) DEFAULT NULL,
  `estado` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
);
INSERT INTO animales(tipo,estado)Values('chanchito','feliz'); -- esto es para agregarle los valores, se usa de esta manera
INSERT INTO animales(tipo,estado)Values('camilo','triste');
INSERT INTO animales(tipo,estado)Values('casa','triste');


SELECT * from animales; -- esto es para ver la tabla 
SELECT * from animales WHERE id = 1;  -- Esto selecciona solo por el id numero 1; 
SELECT * from animales WHERE estado = 'feliz' AND id = 2 AND tipo = 'cata';
-- esto lo que hac e es actualizar el estado del id numero 2;
UPDATE animales SET estado = 'Ultrafeliz' WHERE id = 2; -- esto actualiza con el set le agrega un nuevo valor al estado
DELETE FROM animales WHERE estado = 'feliz';-- ¡¡no se puede por que tiene que ser con un ID!!!
DELETE FROM animales WHERE id = 1 -- ESTE SI ES VALIDO
---
# OTRO CON LAS FUNCIONES PARA BUSQUEDA
CREATE TABLE user(
id int not null auto_increment,
name varchar(50) not null,
edad int not null, 
email varchar(100) not null,
primary key (id)
);
INSERT INTO user (name,edad,email) values('Camilo',22,'camiloht@gmail.com');
INSERT INTO user (name,edad,email) values('Catalina',21,'riverocatalina@gmail.com');
INSERT INTO user (name,edad,email) values('Andres',23,'andres@gmail.com');
INSERT INTO user (name,edad,email) values('Rubiela',47,'rubiela@gmail.com');

SELECT * from user;
SELECT * from user limit 1; -- esto lo que hace es que solo limita la busqueda al primero usuario
SELECT * from user where edad >= 22; -- busca la edad mayor a 22
SELECT * FROM user where edad > 20 AND email = 'camiloht@gmail.com' ;
SELECT * FROM user where edad > 20 or email = 'riverocatalina@gmail.com';
select * from user where edad != 22; -- diferente a la edad de 22 años
select * from user where edad between 30 and 50; -- que la edad entre 30 y 50 esten los pone en la tabla
select * from user where email like '%a@gmail%'; -- esto lo que hace es poder buscar si existe eso entre el email,pero tiene que llevar los dos pocentajes
select * from user where email like '%gmail'; -- esto sera null por que ningun email termina en gmail
select * from user order by edad asc; -- orden ascendente de la edad
select * from user order by edad desc; -- orden  descendente de la edad
select max(edad) as mayor from user;
select id,name,email from user; -- muestra lo que tu quieras que muestre en la tabla seguido de la coma 
select id, name as nombre from user;-- ponerle un alias a la colomna name por nombre







-----------------------------

use world;

select * from country;
select * from city;

select * from countrylanguage;

-- mostrar el pais con mayor poblacion

select Name,Population from country
order by Population desc
limit 1; 

select city from Population
order by Population < 10000000;

select * from country order by Population desc limit 3 ;

select name,LifeExpectancy from(
select name,Lifeexpectancy
from country
where continent = "europe" and Lifeexpectancy <> ""
order by Lifeexpectancy asc limit 5
) as Alcontrario order by lifeexpectancy desc limit 5;
 
 select name,Lifeexpectancy
from country
where continent = "europe" and Lifeexpectancy <> "nan"
order by Lifeexpectancy asc limit 5;

-- session 3 gestion de datos SQP

-- crear tablas temporales
-- para el ejemplo 5 de europa y lifeexpectancy

create table Exp_Vida as
select name,Lifeexpectancy
from country as C
where continent = "europe" and Lifeexpectancy is not null
order by Lifeexpectancy limit 5;

select * from Exp_Vida;

select * from Exp_Vida order by Lifeexpectancy desc, name;

/* crear una tabla temporal llamada empleados_departamentos_x la
 cual tendra la informacion de los empleado(nombre y salario) de la 
 tabla empleados
 -estos empleados trabajan en el departamento x y ganan mas de 1'200.000
 */
 
 
use mundo;
 
 
select * from temp_pais;

create temporary table empleados_dep(
nombre varchar(50) not null,
salario int not null check(salario > 1200000));

drop table empleados_dep;
DESC table empleados_dep;

use world;
create temporary table temp_pais as 
select c.name as nombre,c.population as poblacion
from world.country as c
where c.population <= 1000000;

drop table temp_pais;

-- relaciones entre tablas

-- uno a muchos

create database biblioteca2;

use biblioteca2;

create table libro(
ID INT PRIMARY KEY,
TITULO VARCHAR(100),
AUTOR VARCHAR(100)
);

CREATE TABLE Prestamos(
ID INT PRIMARY KEY,
ID_LIBRO INT,
FECHAPRESTAMO DATE,
FECHADEVOLICION DATE,
foreign key (id_libro) references libro (id)
);

-- relacion de muchos a muchos

-- ESTUDIANTE E INSCRIPCION A CURSOS(N:N)

CREATE TABLE estudiante(
ID INT PRIMARY KEY,
NOMBRE VARCHAR(100)
);

CREATE TABLE curso(
id int primary key,
nombre varchar(100),
descripcion text
);

create table inscripcion(
idestudiante int,
idcurso int,
fechacinscripcion date,
primary key(idestudiante,idcurso),
foreign key(idestudiante) references estudiante(ID),
foreign key(idcurso) references curso(id)
);

create database IDIOMAS;
USE IDIOMAS;

create table idioma(
id int primary key,
idioma varchar(100)
);

create table pais(
idpais int primary key,
nombre varchar(20),
continente varchar(50),
poblacion int
);

create table idioma_pais(
id_idioma int,
id_pais int,
es_oficial tinyint(1),
primary key(id_idioma,id_pais),
foreign key (id_idioma)references idioma(id),
foreign key (id_pais) references pais(idpais)
);
drop table idioma_pais;
select * from idioma_pais;

create table ciudad(
id_ciudad int primary key,
nombre varchar(20),
id_pais int,
foreign key(id_pais) references pais(idpais)
)
;
-- RESVISION DE ESTRUCTURAS DE UNA TABLA

-- COMANDO DESCRIBE O DESC

-- COMANDO SHOW COLUMNS FROM
-- muestra como se hizo la table el CODIGO;
use mundo;

show columns from temp;

use biblioteca2;

show create table inscripcion;

-- COMANDO: SHOW TABLE STATUS -> INFORMACION GENERAL DE LA TABLA

show table status like "inscripcion";


-- comando_ information_schema.tables y information_schema.columns

select * from information_schema.columns
where table_name = "inscripcion";

select * from information_schema.tables
where table_schema = "biblioteca";

-- funciones y comandos en campos en mysql
-- 1. CONCAT : concatena dos o mas cadenas de texto

use world;

select concat(name, "",region) as ubicacion
from country
limit 5;

-- 2. UPPER convierte una cadena a mayuscula

select upper(concat(name,"",region)) as ubicacion
from country
limit 5;

-- 3. LOWER convierte una cadena a mayuscula

select LOWER(concat(name,"",region)) as ubicacion
from country
limit 5;

-- 4. LENGTH: DEVUELVE LA LONGITUD DE UNA CADENA
select (concat(name,"",region)) as ubicacion,
 length(concat(name,"",region)) as largo
from country
limit 5;

-- muestre un listado con los tres nombre mas largos, ordenados del mayor al menor

select name ,length(name) as nombre_largo
from country order by nombre_largo desc
limit 5;

-- comando: SUBSTRING() ESTRAE UNA PARTE DE UNA CADENA

select substring(concat(name,"",region),1,3) as "Sigla de la ubicacion"
from country
limit 5;

-- comando locate; encuentra la pocision de una subcadena

select name from country
where locate("g")
limit 5;

-- ------

select substring(name,1,locate(" ", name)) as "compuestos"
from country
where locate(" ",name) <> 0;
-- comando trim: quita los espacios al principio y al final
-- EL RTRIM QUITA LOS ESPACION A LA DERECHA
-- LTRIM QUITA LOS ESPACIONS A LA IZQUIERDA
select substring(name,1, locate(" ",name)) as ALIAS, name
from country
where locate(" ",name);

select name,replace(name,"Gu","YUL") AS remplazo
from country
where region = "South america";

select name,replace(name,"Gu","YUL") AS remplazo
from country
where remplazo LIKE "%YUL" ;


select name,population, 
if(population > 40000000,"Es mas de 100mil",if(population < 20000000,"Poblado", "Sobrepoblado")) as superPoblado
from country
where region  like "%America";

select name, format(population,0)as Poblacion,
if(population < 20000000,"Despoblado",if(population < 40000000,"Poblado","Sobrepoblado")) as Densidad
from country
where region = "south america";

select * from country;

select name,surfaceArea,Population, (population/surfaceArea) as Division,
if(population/surfaceArea >= 30 ,"sobrePOBLADO",
if(population/surfaceArea >= 20 and population/surfaceArea <= 40,"Poblado",if(population/surfaceArea >= 10 and population/surfaceArea <= 20,"poco poblado",
if(population/surfaceArea < 20,"despoblado","")))) as Estatus
from country
where continent = "south america" or continent = "north america" order by Division desc;

create database Animal;
use Animal;
-- EJERCICIOS
create table cat(
id_gato int primary key,
nombre varchar(50) not null,
raza varchar(150) not null,
color_gato varchar(50),
edad int,
sexo varchar(1),
Juguete_fav varchar(20)
);
drop table cat;

INSERT INTO cat (id_gato,nombre,raza,color_gato,edad,sexo,Juguete_fav) 
values('1',"catico","chandozo","negro",3,"F","peluche"),
('2',"karl","menkium","gris",2,"M","pelota"),
('3',"maarl","persa","blanco",4,"M","");

select * from cat;
-- primero
select sexo,nombre,Juguete_fav
as notieneJuguete
from cat
where sexo = "M" and juguete_fav = "" ;
-- segundo
SELECT id_gato,nombre,raza,color_gato 
from cat
where sexo = "M" AND Juguete_fav = ""
 and raza <> "persa" and raza <> "siamesa";
 
 -- ejercicios world
 
 use world;
 select * from countrylanguage;
 select language,countrycode,
 if(length(language) = 25,"PaisConmasletras","no hay")as longitud
 from countrylanguage
 where length(language) = 25 order by longitud desc
 ;

 -- conexion entre tablas
-- PRODUCTO CRUZ TODOS CON TODOS
select C.CODE, C.NAME, D.ID, D.NAME,D.COUNTRYCODE
from country as C,city as D;

-- CIUDADES DE COLOMBIA

SELECT P.NAME,C.NAME FROM country AS P
inner join city as C on P.code = C.countrycode
where P.name = "colombia";

-- INTERCESECION LEFTT JOINN

-- Los elementos del conjunto A y  donde no exista relacion con B entonces es null

select L.language,P.name  from countrylanguage as L
left join country as P on L.countrycode = P.code
where L.language = "Spanish";

insert into countrylanguage(countrycode,language,isofficial,percentage) values("zzz","marciano","T",100);


select p.name, c.name
from city as c right join country as p on c.countrycode = p.code
where p.name = "colombia"



-- funciones de campos de mysql
-- OTROS EJERCICIOS GROUP BY

-- EJERCICIO 1
-- 1. Calcula el número total de productos que hay en la tabla productos.
use tienda;
SELECT count(p.nombre)as cantidad from producto as p;

-- 2. Calcula el número total de fabricantes que hay en la tabla fabricante.

select count(*)as cantidad from fabricante as f;

-- 3. Calcula el número de valores distintos de 
-- identificador de fabricante aparecen en la
-- tabla productos.

select distinct count(id_fabricante) from producto;

-- 4. Calcula la media del precio de todos los productos.

select format(avg(precio),3) from producto;

-- 5 Muestra el precio máximo, precio mínimo,
-- precio medio y el número total de productos que
-- tiene el fabricante Crucial.

select max(precio) as MAX,min(precio) as MIN, avg(precio) as medio,
count(p.nombre)as cantProd from producto as p
join fabricante as f on  id_fabricante = f.id
where f.nombre = "crucial";

/* 6 Muestra el número total de productos que tiene cada uno de los fabricantes.
 El listado también debe incluir los fabricantes que no tienen ningún
 producto. El resultado mostrará dos columnas, una con el nombre
 del fabricante y otra con el número de productos que tiene.
Ordene el resultado descendentemente por el número de productos.*/

select f.nombre as fabricante,count(p.nombre)as cant from fabricante as f
left join producto as p on p.id_fabricante = f.id
group by f.nombre
order by cant desc;

/*7. Muestra el precio máximo, precio mínimo y precio medio de los productos
 de cada uno de los fabricantes. El resultado mostrará el nombre 
 del fabricante junto con los datos que se
solicitan.*/

select f.nombre, max(precio)as MAXX,min(precio) 
as MINN,AVG(precio) as medio 
from producto as p
join fabricante as f on p.id_fabricante = f.id
group by f.nombre;


/*8. Muestra el precio máximo, precio mínimo, precio medio y el 
número total de productos de los fabricantes que tienen un precio
 medio superior a 200€. No es necesario mostrar el
nombre del fabricante, con el identificador del fabricante es suficiente.*/

select id_fabricante, max(precio)as MAXX,min(precio) 
as MINN,AVG(precio) as medio,count(p.nombre) as cont from producto as p
join fabricante as f on p.id_fabricante = f.id
group by id_fabricante
having medio >= 200
;

/*9. Muestra el nombre de cada fabricante, junto con el precio máximo,
 precio mínimo, precio medio y el número total de productos
 de los fabricantes que tienen un precio medio superior
a 200€. Es necesario mostrar el nombre del fabricante.*/

select f.nombre, max(precio)as MAXX,min(precio) 
as MINN,AVG(precio) as medio,count(p.nombre) as cont from producto as p
join fabricante as f on p.id_fabricante = f.id
group by f.nombre
having medio >= 200
;

/*10. Calcula el número de productos que tienen un precio mayor o igual a 180€.*/

select count(p.nombre) from producto as p
where p.precio >= 180;

/*11. Calcula el número de productos que tiene cada fabricante con un 
precio mayor o igual a
180€.*/

select f.nombre,count(p.nombre) from producto as p
join fabricante as f on id_fabricante = f.id
where p.precio >= 180
group by f.nombre;

select * from producto;
