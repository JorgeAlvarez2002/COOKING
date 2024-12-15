# Proyecto final

## 1. Análisis de las variables de entrada
En primer lugar, se ha visualizado el formato de los datos proporcionados. Tal y como se indica en el guión del proyecto, se trata de un fichero JSON que consta de 20130 recetas. Para cada receta se proporcionan una serie de datos, tal y como se puede observar a continuación:

<img src="https://github.com/user-attachments/assets/1b676459-8c64-48e4-b131-1eb032c5afed" alt="imagen" width="1000">


Para el análisis de las variables de entrada, se ha realizado una representación numérica de las categorías. Para ello, se ha asignado una etiqueta numérica a cada categoría y posteriormente se ha creado un diccionario en el que se relacionan ambos parámetros. A continuación se muestra parte de este diccionario:

<img src="https://github.com/user-attachments/assets/d9faf02e-f366-4d69-9b08-9541b38a5507" alt="imagen" width="600">

Como primer análisis de los datos, se propone la visualización de las 10 categorías con mayor _rating_.

<img src="https://github.com/user-attachments/assets/6f7c0d12-a968-4085-9af7-563ac21a7b02" alt="imagen" width="400">

Como se puede observar, son 9 las categorías con el valor de _rating_ máximo (_rating_=5).

Con el objetivo de entontrar la relación entre las categorías de las distintas recetas y sus correpondientes _ratings_, se calcula la correlación de cada categoría, obteniendo valores ínfimos. Esto nos indica la débil relación entre ambas variables, por lo que se busca otro análisis distinto.

<img src="https://github.com/user-attachments/assets/b074c1e1-f46b-4100-8369-d598b579bb46" alt="imagen" width="200">

A continuación, se ha analizado la frecuencia de aparición de las categorías a lo largo de las distintas recetas. En este caso, se han representado dos histogramas en los cuales se muestra la frecuencia de aparición de las 15 categorías con los _ratings_ más altos y más bajos, respectivamente.

<img src="https://github.com/user-attachments/assets/c6e14627-d90f-40cd-bb21-868187bf4c03" alt="imagen" width="400">

<img src="https://github.com/user-attachments/assets/8066f13a-c486-4098-9d5b-0c69efe18de0" alt="imagen" width="400">

De esta forma, se observa que, de forma general, las categorías que mayor _rating_ presentan son aquellas que aparecen con menos frecuencia. Esto podría indicar que las recetas más raras son las mejores puntuadas por los usuarios, mientras que las más comunes reciben peores valoraciones.

Para terminar, se ha representado la variabilidad del _rating_ para una misma categoría. Esto se ha realizado en primer lugar para las 10 categorías más frecuentes así como para las 10 categorías menos frecuentes. La representación utilizada ha sido el diagrama de caja y bigotes:

<img src="https://github.com/user-attachments/assets/1bc6c553-c4a1-453d-8dbb-f646e7d70dee" alt="imagen" width="400">

<img src="https://github.com/user-attachments/assets/88d30f85-e16b-44c6-a430-789867fd2f38" alt="imagen" width="400">

Se representan también los diagramas para 10 categorías que tienen ratings entre 1 y 2 y otras 10 categorías cuyos ratings están entre 4 y 5. De estos diagramas se llega a la conclusión de que las categorías que presentan valores más altos de _rating_ presentan una menor variabilidad que aquellas que tienen valores de _rating_ más bajos. 

<img src="https://github.com/user-attachments/assets/c28114a1-e655-4e7c-8ea1-749256c75289" alt="imagen" width="400">

<img src="https://github.com/user-attachments/assets/5bef85cf-d4d1-4c89-8593-62ff1434feca" alt="imagen" width="400">


## 2. Preprocesado
A continuación, se aplica un preprocesado a los datos de entrada (variables _directions_ y _descriptions_) con el objetivo de optimizar los resultados obtenidos en el cálculo de los embeddings y el entrenamiento y la evaluación posterior. A través de este preprocesado, se eliminará información que no es relevante de forma que únicamente se tenga contenido semántico importante. Para ello se seguirán 4 pasos diferenciados: *wrangling*, tokenización, homogenización y limpieza.

Los textos originales son los siguientes:

<img src="https://github.com/user-attachments/assets/a3e05c58-bfb0-49b5-8a30-4ddd6128575b" alt="imagen" width="400">

### 2.1. _Wrangling_
En este primer paso, se eliminan caracteres del texto que no son relevantes semánticamente, como signos de puntuación y números. En este caso, se ha elegido eliminar comas (**,**), guiones (**-**), puntos (**.**) y números. 

<img src="https://github.com/user-attachments/assets/0620febe-9dcf-411f-8d9c-79d3ff006199" alt="imagen" width="400">
<img src="https://github.com/user-attachments/assets/03fa3941-0813-4fa6-bbbb-6a2c7560486d" alt="imagen" width="400">

<img src="" alt="imagen" width="400">
### 2.2. Tokenización
### 2.3. Homogenización
### 2.4. Limpieza
