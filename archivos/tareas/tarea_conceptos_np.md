# Conceptos operaciones estadisticas
## 1. Contar elementos (count)
Sirve para contar el numero de veces que aparece un elemento en un conjunto de datos
dada la lista [100,200,100,300,400]
```Python
lista.count(100)
```
Retornaría un 2 ya que es la cantidad de veces que aparece ese elemento en la lista
## 2. Media aritmética (mean)
La media aritmética se calcula sumando todos los valores y después dividiéndolos entre el numero total de elementos.  
Usando Numpy se calcularía de la siguiente manera:
``` Python
promedio = np.mean(lista)
```
## 3. Desviación estándar(std)
La desviación estándar mide la variación de los datos con respecto a la media.  
Tener una std baja significa que los datos tienden a estar cerca de la media, mientras que una std alta representa que los datos están mas dispersos
Usando Numpy se calcularía de la siguiente manera:
``` Python
desviacion_estandar = np.std(lista)
```
## 4. Valor mínimo (min)
Es valor mas bajo dentro de un conjunto de datos.
Usando Numpy se calcularía de la siguiente manera:
``` Python
minimo = np.min(lista)
```
## 5. Valor máximo (max)
Es el valor mas alto dentro de un conjunto de datos.
``` Python
maximo = np.max(lista)
```
## 6. Q1 - Primer cuartil (25%)
El primer cuartil es la 1/4 parte de los datos ordenados y es el valor limite en el cual están por debajo el 25% de los datos.
Usando Numpy se calcularía de la siguiente manera:
``` Python
q1 = np.percentil(lista,25)
```
## 7. Q2 - Segundo cuartil (50%)
El segundo cuartil coincide con la mediana. es el valor que esta justo a la mitad
Usando Numpy se calcularía de la siguiente manera:
``` Python
q2 = np.percentil(lista,50)
mediana = np.mediana(lista)
```
## 8. Q3 - Tercer cuartil (75%)
Muy parecido al primer cuartil pero ahora es 3/4 parte de los datos y el valor por el cual están por debajo el 75% de los datos.
Usando Numpy se calcularía de la siguiente manera:
``` Python
q3 = np.percentil(lista,75)
```
