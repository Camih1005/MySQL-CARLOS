# MySQL
Campusland MySQL
---
### Empezando aplicacion
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
