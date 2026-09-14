# Tarea consultas SQL

## Creación de la tabla e inserción de valores
``` SQL
CREATE TABLE peliculas_andres(
	pelicula_id INT AUTO_INCREMENT PRIMARY KEY,
	titulo VARCHAR(255) NOT NULL,
	director VARCHAR(255) NOT NULL,
	genero VARCHAR(255) NOT NULL,
	ano_estreno INT NOT NULL,
	duracion_minutos INT NOT NULL,
	clasificacion DECIMAL(3,1) NOT NULL,
	disponibilidad BOOLEAN NOT NULL
);

INSERT INTO peliculas_andres (titulo, director, genero, ano_estreno, duracion_minutos, clasificacion, disponibilidad) VALUES
	('Inception', 'Christopher Nolan', 'Ciencia Ficción', 2010, 148, 8.8, TRUE),
	('The Dark Knight', 'Christopher Nolan', 'Acción', 2008, 152, 9.0, TRUE),
	('Pulp Fiction', 'Quentin Tarantino', 'Crimen', 1994, 154, 8.9, FALSE),
	('Interstellar', 'Christopher Nolan', 'Ciencia Ficción', 2014, 169, 8.7, TRUE),
	('Parasite', 'Bong Joon-ho', 'Drama', 2019, 132, 8.5, TRUE),
	('El Viaje de Chihiro', 'Hayao Miyazaki', 'Animación', 2001, 125, 8.6, FALSE),
	('Matrix', 'Lana y Lilly Wachowski', 'Ciencia Ficción', 1999, 136, 8.7, TRUE),
	('Gladiador', 'Ridley Scott', 'Acción', 2000, 155, 8.5, TRUE),
	('Whiplash', 'Damien Chazelle', 'Drama', 2014, 106, 8.5, TRUE),
	('El Señor de los Anillos: La Comunidad del Anillo', 'Peter Jackson', 'Fantasía', 2001, 178, 8.8, FALSE);
```
## 1. Mostrar Todas las películas
``` SQL
SELECT * FROM peliculas_andres
```
## 2.Mostrar solamente el título, género y año de estreno.
``` SQL
SELECT titulo,genero,ano_estreno FROM peliculas_andres;
```
## 3.Mostrar las películas disponibles.
``` SQL
SELECT * FROM peliculas_andres WHERE disponibilidad=TRUE;
```
## 4.Buscar las películas de un género específico.
``` SQL
SELECT * FROM peliculas_andres WHERE genero = "Drama";
```
## 5.Mostrar las películas estrenadas después del año 2015.
``` SQL
SELECT * FROM peliculas_andres WHERE ano_estreno>2015;
```
## 6.Mostrar las películas con calificación mayor a 8.
``` SQL
SELECT * FROM peliculas_andres WHERE clasificacion > 8;
```
## 7.Ordenar las películas de la más reciente a la más antigua.
``` SQL
SELECT * FROM peliculas_andres ORDER BY ano_estreno DESC;
```
## 8.Mostrar la película con mayor calificación.
``` SQL
SELECT titulo, clasificacion FROM peliculas_andres ORDER BY clasificacion DESC LIMIT 1;
```
## 9.Calcular la duración promedio de las películas.
``` SQL
SELECT AVG(duracion_minutos) AS "Duración_promedio" FROM peliculas_andres;
```
## 10.Contar cuántas películas existen por género.
``` SQL
SELECT genero, COUNT(genero) as "Total" FROM peliculas_andres GROUP  BY genero;
```
## 11.Buscar películas cuyo título contenga una palabra utilizando LIKE.
``` SQL
SELECT * FROM peliculas_andres WHERE titulo LIKE "%El %";
```
## 12.Cambiar una película de disponible a no disponible utilizando UPDATE.
``` SQL
UPDATE peliculas_andres
	SET disponibilidad = FALSE
	WHERE pelicula_id=1;
```
