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

<img src="https://github.com/user-attachments/assets/fe97a93b-930a-4955-92a5-e1f71bd3a9ff" alt="imagen" width="400">

### 2.1. _Wrangling_
En este primer paso, se eliminan caracteres del texto que no son relevantes semánticamente, como signos de puntuación y números. En este caso, se ha elegido eliminar comas (**,**), guiones (**-**), puntos (**.**) y números. 

<img src="https://github.com/user-attachments/assets/0620febe-9dcf-411f-8d9c-79d3ff006199" alt="imagen" width="400">
<img src="https://github.com/user-attachments/assets/03fa3941-0813-4fa6-bbbb-6a2c7560486d" alt="imagen" width="400">



### 2.2. Tokenización
La tokenización consiste en la segmentación del texto en _tokens_, que en este caso serán palabras individuales.

<img src="https://github.com/user-attachments/assets/f279ab6b-cb67-453d-965e-347a44c59366" alt="imagen" width="400">

Una vez se ha separado el texto en _tokens_, antes de aplicar la homogenización, se ha aplicado un filtrado en el que todas las letras del texto se convierten a minúsculas y se eliminan todos aquellos caracteres que no se consideran alfanuméricos. 

<img src="https://github.com/user-attachments/assets/bd55c717-13bd-4220-a309-ce125a5ef7fa" alt="imagen" width="400">


### 2.3. Homogenización
Con la homogenización se busca que todas las palabras con significados equivalentes se representen de una única forma de forma que el tamaño del vocabulario se vea reducido. Esto hará que a la hora de representar los _embeddings_, estos tengan dimensiones menores y en consecuencia se mejore el rendimiento del modelo. En clase se han trabajado dos técnicas, que son la lematización y _stemming_. En este caso se ha elegido la lematización por su mayor precisión, ya que las palabras se reducen a su forma base en lugar de a la palabra raíz más básica, como ocurre en _stemming_.

<img src="https://github.com/user-attachments/assets/96a86f48-8dd9-4ad2-9eef-6e49a2eea7dc" alt="imagen" width="400">


### 2.4. Limpieza
Por último, se procede a la eliminación de aquellas palabras que son muy comunes en el lenguaje y que por lo tanto no tienen un contenido semnántico relevante.

<img src="https://github.com/user-attachments/assets/aed6f406-5057-4940-aaa1-002a5692d2fe" alt="imagen" width="400">


## 3. Vectorización
A continuación, se va a realizar la vectorización de la  variable _directions_, con la que se trabajará en el resto del proyecto.

### 3.1. TF-IDF

En este tipo de vectorización, se asignan valores más altos a aquellos términos que son muy frecuentes en una receta en particular y muy poco en otras recetas. De esta forma, se penaliza a las palabras que aparecen en muchas recetas, lo cual ocurre con las palabras básicas.

La representación TF-IDF se generó a partir del texto preprocesado (directions y description) de cada receta. Se utilizó la clase TfidfVectorizer de sklearn, configurada con los siguientes parámetros:
- min_df=`: Se descartan términos que aparecen en menos de 5 documentos.
- max_df=0.8: Se eliminan términos que aparecen en más del 80% de los documentos.

De esta forma, se obteniene una matriz que tiene la siguiente forma:

<img src="https://github.com/user-attachments/assets/ae6c3924-0b98-4938-831a-19711aa8547d" alt="imagen" width="300">

Se puede observar que las dimesiones de la matriz son 20130x3924, correpondientes a las 20130 recetas y las 3924 palabras únicas que forman el vocabulario de las recetas. En la parte izquierda se muestran las "coordenadas" de cada palabra y a la derecha el peso TF-IDF asociado a esa palabra.


### 3.1. Word2Vec

Se han realizado distintos análisis a partir de los embeddings extraídos con Word2Vec. En primer lugar, se ha realizado una reducción de la dimensionalidad de los datos.
Un tamaño de embedding de 100 es razonable y suficiente para el número de recetas que tenemos (20,130) debido a que con 20,130 recetas, un embedding de tamaño 100 representa 2013000 parámetros (si consideramos un modelo simple con una capa de entrada que procesa estos embeddings). Esto es manejable para entrenar modelos estándar como Random Forest o k-NN sin riesgo de sobreajuste. Además un embedding más grande de 300 o 768 como Bert podría ser innecesario y añadir ruido en lugar de mejorar la capacidad de generalización.

<img src="https://github.com/user-attachments/assets/032a09d2-4327-4a58-8aeb-6f060b816f89" alt="imagen" width="700">
<img src="https://github.com/user-attachments/assets/91fc2147-0450-4db8-8491-88c3c0067eba" alt="imagen" width="700">

Podemos observar que los términos que son similares en contexto entre sí presentan una distancia espacial entre ellos menor. EXTENDER UN POCO.

Por otro lado y siguiendo con la característica observada anteriormente, buscamos palabras que sean similares a un término específico. Por ejemplo, para el término _bake_ obtenemos lo siguiente:

<img src="https://github.com/user-attachments/assets/4e4e0ae5-826d-4734-8b0a-e693755d931b" alt="imagen" width="200">

Por último, se ha calculado la similitud coseno entre recetas a partir de los _embeddings_ extraídos. Esto se ha realizado para las 10 primeras recetas, comparándolas de 2 en 2 (la primera con la segunda, la tercera con la cuarta...):

<img src="https://github.com/user-attachments/assets/80080646-f6d1-4e31-8026-d1aa9a36f9ca" alt="imagen" width="800">
<img src="https://github.com/user-attachments/assets/44627365-4ea8-46f4-9184-be13ca234709" alt="imagen" width="800">

<img src="" alt="imagen" width="400">


### 3.1. Embeddings contextuales: BERT
Por último, se han vectorizado las características correpondientes a la variable _directions_ a través del modelo basado en transformers BERT.

## 4. Entrenamiento y evaluación
### 4.1. Redes neuronales con PyTorch

### 4.1. Técnicas de regresión de la librería Scikit-learn

En este punto del proyecto, nos enfocamos en el entrenamiento y evaluación de modelos de regresión utilizando las representaciones vectoriales previamente comentadas. Los modelos seleccionados para esta tarea son Random Forest y k-Nearest Neighbors (kNN), los cuales serán evaluados sobre tres tipos de representaciones vectoriales de los documentos: TF-IDF, Word2Vec y BERT.

Estos modelos de regresión, Random Forest y kNN, se entrenarán con las tres representaciones mencionadas para evaluar su rendimiento en la predicción de las valoraciones de recetas. A través de esta experimentación, buscaremos identificar qué tipo de representación vectorial y qué modelo ofrecen un mejor rendimiento en esta tarea de regresión.
#### 4.1.1 TF-IDF
##### 4.1.1.1 Random Forest

En un primer intento de aplicar el regresor random Forest en el notebook "RandomForest-TF-IDF_1.ipynb"con 50 árboles de decisión; para preparar los datos de entrenamiento y test se decide rellenar los datos faltantes del rating con la media, que es una técnica habitual. Se selecciona un subconjunto más pequeño de las muestras de entrenamiento. 1000 recetas se utilizan para entrenar el modelo, lo que es útil cuando se quiere acelerar el proceso de entrenamiento ya que los recursos computacionales son limitados.

La matriz TF-IDF es costosa computacionalmente para un regresor como Random FOrest por lo que se decide reducir dimensionalidad para entrenar el modelo. Se utiliza el método SelectKbest con f_regression que selecciona las mejores características del conjunto de datos basado en un test estadístico que mide la relación entre las características y el target (rating). Se ha establecido que el número de componentes a conservar es 500. Este número fue elegido principalmente por razones de eficiencia computacional. Reducir la dimensionalidad ayuda a que el modelo cargue más rápido y se entrene de manera más eficiente. Además al usar todas las características se observa una ligera empeora del MSE por lo que se puede asegurar que hay muchas componentes ruidosas.

Para justificar este primer analisis se utilizan componentes escogidas aleatoriamente y a través del método SelectKbest obteniendose los siguientes resultados:

Los resultados evidencian que SelectKBest mejora el desempeño del modelo, al elegir características que tienen una mayor correlación con la variable objetivo, en comparación con la selección aleatoria de características. Esto refuerza la idea de que, en problemas supervisados (predicción del rating de recetas), es más efectivo utilizar técnicas de selección de características que consideren la relación con el target, como SelectKBest, en lugar de una selección aleatoria que no aprovecha esa información.

<img src="https://github.com/user-attachments/assets/5010445f-9505-4778-900e-195b15938865" alt="imagen" width="400">

Este análisis permite argumentar que la reducción de dimensionalidad supervisada (como SelectKBest) proporciona mejores resultados que una reducción aleatoria de características. Con el uso de validación cruzada, se ha obtenido una evaluación más precisa del rendimiento del modelo, con un MSE de 1.4202, que es ligeramente mejor que los resultados iniciales obtenidos con SelectKBest sin validación cruzada. Esto valida la robustez de tu modelo y asegura que la selección de características es adecuada para predecir el rating de las recetas.

El modelo ha identificado ciertas palabras clave que impactan las calificaciones de las recetas, pero es importante reconocer que el modelo no entiende el significado semántico de las palabras, sino que simplemente las evalúa por su capacidad para predecir la variable objetivo (rating). Además, al ser un modelo no lineal como Random Forest, las características con mayor importancia no siempre corresponden a las palabras que intuitivamente pensaríamos que deberían tener más peso en el contexto de una receta.

<img src="https://github.com/user-attachments/assets/cd20ad70-1bc2-4eda-bea6-1099e468e983" alt="imagen" width="600">

Se realiza también un análisis de los valores predichos vs reales, donde las predicciones si fueran perfectas se colocarían sobre la línea roja. Los malos resultados se asocian a los ratings se distribuyeb de manera no uniforme como observaremos más abajo, hay muchas recetas que poseen un rating de 3.5 y 4.5 y por ello el modelo encuentra las mayores dificultades para predecir ratings extremos (0 o 5):

<img src="https://github.com/user-attachments/assets/754d0419-d1f0-4785-88f1-fd81d612c40f" alt="imagen" width="600">
 
Este análisis se confirma si se observa como se distribuyen las predicciones vs los valores reales:

<img src="https://github.com/user-attachments/assets/b6e2adbb-a0ca-44c0-8672-87e365930b91" alt="imagen" width="600">

Para mejorar el rendimiento del modelo RandomForestRegressor, hemos implementado una búsqueda exhaustiva de hiperparámetros utilizando GridSearchCV. Este proceso permite probar diferentes combinaciones de parámetros y seleccionar los que mejor optimicen la puntuación de validación cruzada (medida de rendimiento general del modelo). La búsqueda de hiperparámetros se realizó utilizando un conjunto de entrenamiento reducido (1000 recetas).

 Se probaron 50, 100 y 150 árboles de decisión, se probaron distintas profundidades de 10, 20, 30 y none. También se probó el número mínimo de muestras requerido para dividir un nodo. Se probaron 2, 5 y 10 muestras. Tras ejecutar GridSearchCV con una validación cruzada de 3 pliegues (cv=3), los mejores parámetros encontrados fueron los siguientes:

 <img src="https://github.com/user-attachments/assets/bc61e60b-03cd-43ca-8d59-ae4aa22bf8ed" lt="imagen" width="400">

La mejor puntuación de validación cruzada obtenida fue 0.0822, lo que indica que el modelo optimizado tiene un rendimiento moderado en términos de la varianza explicada durante la validación cruzada. Aunque este valor no es alto, refleja un modelo que generaliza razonablemente bien.

Se realiza un análisis para ver como varían el MSE y el R² para diferentes valores del hiperparámetro de número de árboles de decisión y del número de datos de entrenamiento. En términos generales, se esperaría que el MSE disminuya a medida que aumente el tamaño del conjunto de entrenamiento, ya que el modelo tiene más datos para aprender. Asimismo, el R² debería aumentar, ya que el modelo mejora su capacidad para explicar la variabilidad de los datos a medida que se entrena con más ejemplos.

Se observa como a partir de 5000 recetas el modelo podría volverse más sensible a los datos de entrenamiento, capturando detalles no representativos o ruido. Esto puede hacer que el modelo generalice peor en el conjunto de prueba y, como resultado, el MSE empeore a medida que aumenta el tamaño del conjunto de entrenamiento.

Aunque n_estimators=150 podría ofrecer más árboles, esto no necesariamente mejora el rendimiento del modelo. Si el modelo ya ha alcanzado un rendimiento óptimo con un número menor de árboles, aumentar n_estimators más allá de ese punto puede llevar a un sobrecosto computacional sin mejorar la predicción. El aumento en R² podría indicar que el modelo es capaz de explicar más de la variabilidad de los datos en general

![image](https://github.com/user-attachments/assets/874701e6-7aed-4546-8a24-7163be73bc5a)

En conclusión, este comportamiento de empeoramiento del MSE podría indicar que el modelo está empezando a sobreajustarse al conjunto de entrenamiento a medida que aumentas el tamaño de los datos.
##### 4.1.1.2 kNN


#### 4.1.2 Word2vec

#### 4.1.3 Word2vec
## 5. Comparación de lo obtenido con el _fine-tuning_ de un modelo preentrenado con _Hugging Face_





