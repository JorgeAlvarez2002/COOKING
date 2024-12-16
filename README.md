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


### 3.1. Embeddings contextuales: BERT
En este proyecto, se utiliza BERT (Bidirectional Encoder Representations from Transformers) para generar embeddings contextuales de texto a partir del campo directions de nuestras recetas. La idea principal es capturar el contexto semántico de las palabras en cada receta, proporcionando una representación rica y contextualizada para usarse como entrada en modelos de aprendizaje automático para predecir el rating.

Se utilizó el modelo preentrenado bert-base-uncased, que ha sido entrenado con un corpus de 2.500 millones de palabras provenientes de Wikipedia y Google Books. Este modelo genera embeddings con un tamaño fijo de 768 dimensiones para cada entrada, lo que corresponde al tamaño del último estado oculto del token [CLS]. Este token es especialmente relevante porque captura la información semántica de toda la secuencia.

Dado que el procesamiento con BERT es computacionalmente intensivo y nuestro dataset contiene 20,130 recetas, se decidió reducir el tamaño del dataset a 10,000 muestras seleccionadas aleatoriamente. Esto permitió trabajar con un volumen de datos manejable dentro de las restricciones de memoria y tiempo.

Para cada texto, se aplicó una tokenización con un límite máximo de 512 tokens, ya que esta es la longitud máxima permitida por el modelo BERT. Si una receta supera este límite, el texto se trunca para ajustarse. Este recorte es razonable porque las instrucciones de las recetas suelen ser más cortas que este límite.

Para verificar la calidad y las propiedades de los embeddings generados por BERT, graficamos la distribución de valores para un token específico. Esto nos permite observar cómo se estructuran los valores en el espacio latente de 768 dimensiones.

<img width="305" alt="image" src="https://github.com/user-attachments/assets/0cc92551-1ea5-4884-a0de-d29ab97a2a0b" />

## 4. Entrenamiento y evaluación
A continuación se van a entrenar y evaluar modelos de regresión utilizando distintas estrategias de aprendizaje automático.

Para la comparación de las distintas técnicas y configuraciones implementadas, se va a calcular el MSE y el R^2. Por un lado, el MSE (_Mean Squared Error_) representa la magnitud promedio de los errores al cuadrado, siendo los errores en este caso las diferencias entre los valores reales y las predicciones del modelo. Por otro lado, el R^2 es el coeficiente de determinación, y mide qué proporción de la variación total es explicada por el modelo.

### 4.1. Redes neuronales con PyTorch
En este apartado se van a entrenar y evaluar distintas configuraciones de red reuronal, en las que variarán distintos hiperparámetros como el número de épocas, la tamaño de batch y la tasa de aprendizaje. También se mostrará el efecto en los resultados de aumentar el número de capas de la red.
Se han realizado las siguientes comparaciones:

- "Caso peor": se configura un número de épocas bajo (_epochs = 5_), un tamaño de batch grande (_batch_size = 128_) y una tasa de aprendizaje elevada (_lr = 0.1_).
- "Aumentamos el nº de épocas": se configura un mayor número de épocas (_epochs = 20_) y el tamaño de batch y la tasa de aprendizaje se dejan como en el "caso peor".
- "Disminuimos el tamaño de batch": se configura un menor tamaño de batch (_batch_size = 32_) y el número de épocas y la tasa de aprendizaje se dejan como en el "caso peor".
- "Disminuimos la tasa de apredizaje": se configura una menor tasa de aprendizaje (_lr = 0.001_) y el número de épocas y el tamaño de batch se dejan como en el "caso peor".
- "Caso mejor": se configura un número de épocas alto (_epochs = 20_), un tamaño de batch pequeño (_batch_size = 32_) y una tasa de aprendizaje pequeña (_lr = 0.1_).

Por otro lado, se ha aumentado en 2 el número de capas a partir de las configuraciones de "caso peor" y "caso mejor".

Por último, probamos a aumentar el número de épocas a 100 y 200 a partir de la configuración "caso mejor", con el objetivo de comparar si esto mejora los resultados obtenidos a cambio de un mayor coste computacional.

#### 4.1.1 TF-IDF
Como se puede observar, los resultados mejoran con respecto al "caso peor" al aumentar el número de épocas y también al disminuir el tamaño de batch. También mejoran, aunque no de forma tan pronunciada, al establecer una tasa de aprendizaje menor. Si se mejoran los tres hiperparámetros a la vez ("caso mejor"), los resultados mejoran considerablemente respecto al resto de casos. 

<img src="https://github.com/user-attachments/assets/b38bd058-88eb-4519-8a90-78c91f1ca27f" alt="imagen" width="400">

Al aumentar el número de capas de la red neuronal, se observa una mejora al partir de la configuración correspondiente al "caso peor". Sin embargo, esto no es así si se parte de la configuración correspondiente al "caso mejor", pues, aunque ligeramente, los valores de MSE y R^2 empeoran, lo cual puede deberse a un sobreajuste de los datos.

<img src="https://github.com/user-attachments/assets/b13d507b-e676-4e62-a44f-71e48d5b01be" alt="imagen" width="400">

Por último, se observa que el aumento del número de épocas con las que se entrena la red es muy relevante. Tanto es así, que incluso se mejoran los resultados obtenidos en "caso mejor" al hacer uso de 200 capas. Con esto se llega a la conclusión de que, para este problema en particular, un gran número de iteraciones en el entrenamiento de la red es un aspecto muy importante para obtener unos resultados óptimos.

<img src="https://github.com/user-attachments/assets/252af8e8-c081-464a-a369-4dc943b2f7a4" alt="imagen" width="400">



#### 4.1.2 Word2vec
A continuación se repite el análisis anterior, esta vez para los embeddings extraídos con el algoritmo Word2Vec. En esta primera comparación se observa que la mejora que se produce en los resultados al aumentar el número de épocas y disminuir la tasa de aprendizaje es bastante mayor que en el caso anterior. En consecuencia, también mejoran los resultados para el "caso mejor", que esta vez son ligeramente peores que los obtenidos al reducir la tasa de aprendizaje. Esto puede deberse a la naturaleza de los embeddings, pues el ajuste que permite una tasa de aprendizaje baja puede ser beneficiosa por aprovechar mejor las relaciones semánticas que representan. Sin embargo, esto puede provocar que al aumentar el número de épocas se produzca un cierto sobreajuste, empeorando las tasas de error.

<img src="https://github.com/user-attachments/assets/a0d95d94-607a-4ad0-a0fc-376a480cfa5c" alt="imagen" width="400">

En cuanto al aumento del número de capas, como ya se venía adelantando, los valores de MSE y R^2 son mejores de forma global. Esto puede explicarse de nuevo con el formato de los embeddings extraídos con Word2Vec, los cuales permiten un apredizaje más profundo, beneficiándose por tanto de redes con un mayor número de capas. Aún así, siguen teniendo el mismo comportamiento que en el caso TF-IDF: aumentar dos capas el número de capas de la red supone una mejora considerable para el "caso peor", sin embargo, con respecto al "caso mejor" se mantiene constante la tasa de error.

<img src="https://github.com/user-attachments/assets/351e3d66-7a8e-4a97-bddc-02f0a3ab4e1f" alt="imagen" width="400">

Aunque lo esperado sería que los resultados mejoraran respecto al caso TF-IDF igual que ocurría en las dos comparaciones anteriores, en este caso resulta perjudicial el aumentar tanto el número de épocas en el entrenamiento de la red. A diferencia de TF-IDF, los embeddings Word2Vec contienen relaciones semánticas previamente aprendidas, por lo que entrenar el modelo durante demasiadas épocas provoca un sobreajuste que lleva a su vez a una disminución de la calidad de las predicciones.

<img src="https://github.com/user-attachments/assets/d4ae3373-5adc-4108-b525-375f291328b9" alt="imagen" width="400">


#### 4.1.3 Bert
Por último, se obtienen los resultados correspondientes al entrenamiento y evaluación de embeddings extraídos con BERT. 
Como era de esperar, dada la mayor calidad y complejidad de los embeddings, los resultados obtenidos de forma general son mejores que para los dos casos anteriores. En esta primera comparación, se observa que el "caso peor" y el "caso mejor" presentan valores similares, y únicamente un menor tamaño de batch y tasa de apredizaje mejoran los resultados ligeramente. Esto es un indicador de la calidad de los embeddings de BERT, pues como se puede apreciar, el modelo no depende tanto de los hiperparámetros con los que se configure la red.

<img src="https://github.com/user-attachments/assets/09853cc1-12ba-4100-b597-dcc63286f61a" alt="imagen" width="400">

Por otro lado, de igual manera que para el resto de embeddings, el aumento del número de capas solo tiene efecto para el "caso peor", pues en el "caso mejor" ya se está aprovechando la información de los embeddings con la configuración optimizada de la red.

<img src="https://github.com/user-attachments/assets/47e3c1bd-2ac3-4d44-b547-90cb85cdb3a9" alt="imagen" width="400">

Por último, vemos que, aunque en menor medida que en el caso Word2Vec, los resultados empeoran al aumentar el número de épocas que se entrena la red neuronal. Esto ocurre debido al sobreajuste a los datos de entrenamiento provocado por el número elevado de épocas, igual que ocurría en el caso anterior.

<img src="https://github.com/user-attachments/assets/e7dcceb1-f6f4-49d3-9809-325fddfcde79" alt="imagen" width="400">


### 4.2. Técnicas de regresión de la librería Scikit-learn
En este punto del proyecto, nos enfocamos en el entrenamiento y evaluación de modelos de regresión utilizando las representaciones vectoriales previamente comentadas. Los modelos seleccionados para esta tarea son Random Forest y k-Nearest Neighbors (kNN), los cuales serán evaluados sobre tres tipos de representaciones vectoriales de los documentos: TF-IDF, Word2Vec y BERT.

Estos modelos de regresión, Random Forest y kNN, se entrenarán con las tres representaciones mencionadas para evaluar su rendimiento en la predicción de las valoraciones de recetas. A través de esta experimentación, buscaremos identificar qué tipo de representación vectorial y qué modelo ofrecen un mejor rendimiento en esta tarea de regresión.

#### 4.2.1 TF-IDF
##### 4.2.1.1 Random Forest
En un primer intento de aplicar el regresor random Forest en el notebook "RandomForest-TF-IDF_1.ipynb" con 50 árboles de decisión; para preparar los datos de entrenamiento y test se decide rellenar los datos faltantes del rating con la media, que es una técnica habitual. Se selecciona un subconjunto más pequeño de las muestras de entrenamiento. 1000 recetas se utilizan para entrenar el modelo, lo que es útil cuando se quiere acelerar el proceso de entrenamiento ya que los recursos computacionales son limitados.

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

Para mejorar el rendimiento del modelo RandomForestRegressor en "RandomForest-TF-IDF_2.ipynb", se implementa una búsqueda exhaustiva de hiperparámetros utilizando GridSearchCV. Este proceso permite probar diferentes combinaciones de parámetros y seleccionar los que mejor optimicen la puntuación de validación cruzada (medida de rendimiento general del modelo). La búsqueda de hiperparámetros se realizó utilizando un conjunto de entrenamiento reducido (1000 recetas).

 Se probaron 50, 100 y 150 árboles de decisión, se probaron distintas profundidades de 10, 20, 30 y none. También se probó el número mínimo de muestras requerido para dividir un nodo. Se probaron 2, 5 y 10 muestras. Tras ejecutar GridSearchCV con una validación cruzada de 3 pliegues (cv=3), los mejores parámetros encontrados fueron los siguientes:

 <img src="https://github.com/user-attachments/assets/bc61e60b-03cd-43ca-8d59-ae4aa22bf8ed" alt="imagen" width="400">

La mejor puntuación de validación cruzada obtenida fue 0.0822, lo que indica que el modelo optimizado tiene un rendimiento moderado en términos de la varianza explicada durante la validación cruzada. Aunque este valor no es alto, refleja un modelo que generaliza razonablemente bien.

Se realiza un análisis para ver como varían el MSE y el R² para diferentes valores del hiperparámetro de número de árboles de decisión y del número de datos de entrenamiento. En términos generales, se esperaría que el MSE disminuya a medida que aumente el tamaño del conjunto de entrenamiento, ya que el modelo tiene más datos para aprender. Asimismo, el R² debería aumentar, ya que el modelo mejora su capacidad para explicar la variabilidad de los datos a medida que se entrena con más ejemplos.

Se observa como a partir de 5000 recetas el modelo podría volverse más sensible a los datos de entrenamiento, capturando detalles no representativos o ruido. Esto puede hacer que el modelo generalice peor en el conjunto de prueba y, como resultado, el MSE empeore a medida que aumenta el tamaño del conjunto de entrenamiento.

Aunque n_estimators=150 podría ofrecer más árboles, esto no necesariamente mejora el rendimiento del modelo. Si el modelo ya ha alcanzado un rendimiento óptimo con un número menor de árboles, aumentar n_estimators más allá de ese punto puede llevar a un sobrecosto computacional sin mejorar la predicción. El aumento en R² podría indicar que el modelo es capaz de explicar más de la variabilidad de los datos en general

![image](https://github.com/user-attachments/assets/874701e6-7aed-4546-8a24-7163be73bc5a)

En conclusión, este comportamiento de empeoramiento del MSE podría indicar que el modelo está empezando a sobreajustarse al conjunto de entrenamiento a medida que aumentas el tamaño de los datos.

Con la gráfica de la curva de aprendizaje que se genera, se observa que el MSE de entrenamiento disminuye conforme aumenta el tamaño del conjunto de entrenamiento. Sin embargo, este no llega a a acercarse a un valor muy bajo lo cual podría indicar que la capacidad del modelo es limitada.

<img src="https://github.com/user-attachments/assets/c6d3e36f-711d-4b43-801e-1be2c48513bd" alt="imagen" width="600">

Este análisis permite ver que aunque aumentes el tamaño del conjunto de entrenamiento, el modelo aún no ha logrado reducir suficientemente el MSE en el conjunto de prueba ni de entrenamiento. Si a continuación se observa el histograma que compara las predicciones vs valores reales para el mejor modelo obtenido tras el estudio previo de hiperparámetros se observa un ligero mejor ajuste de las predicciones:

<img src="https://github.com/user-attachments/assets/d1dfba4f-522e-4abe-8e2a-fddeffc0be66" width="425" alt="image">

##### 4.2.1.2 kNN

Al observar los resultados obtenidos de Random Forest, como el MSE alto tanto en el conjunto de entrenamiento como en el de prueba (en particular, el MSE de prueba no mejora significativamente con el tamaño del conjunto de entrenamiento), es claro que el modelo no está capturando bien las relaciones subyacentes entre las características y la variable objetivo. A pesar de los esfuerzos por optimizar los hiperparámetros (a través de GridSearchCV), el modelo sigue mostrando un rendimiento limitado. Este comportamiento puede indicar que Random Forest no es adecuado para la naturaleza de los datos en cuestión, o que las características seleccionadas no son las más representativas. Se decide probar con el regresor kNN que es un modelo no paramétrico que no hace suposiciones sobre la forma de la relación entre las características y la variable objetivo. A diferencia de Random Forest, que intenta aprender patrones complejos mediante árboles de decisión, kNN utiliza una metodología simple basada en la proximidad de los puntos de datos, lo que puede ser útil cuando los datos tienen una estructura no tan compleja.

Como kNN es menos exigente computacionalmente utilizamos las 1000 características más representativas por cada receta según kBest y se utiliza el total de todas las recetas. El siguiente gráfico muestra el comportamiento del Error Cuadrático Medio (MSE) en función del número de vecinos k en el algoritmo kNN. El MSE disminuye drásticamente cuando el número de vecinos (k) se incrementa desde valores bajos hasta un punto donde se estabiliza, lo que indica que kNN se vuelve más estable a medida que se promedia sobre más vecinos.

<img src="https://github.com/user-attachments/assets/1d4c4b54-b36d-4dcf-8529-781c23ac1082" width="418" alt="image">

Como un k muy alto puede llevar a subajuste (underfitting), ya que el modelo sería demasiado simple y no capturaría las relaciones locales de los datos.Se llega al compromiso de elegir como k óptimo=20, aunque se obtiene un peor resultado de MSE que con random Forest.

<img src="https://github.com/user-attachments/assets/c94aa9dc-95b7-4626-9035-9fc6bb225834" width="185" alt="image">

En la representación de valor real vs predicción se puede llegar a la misma conclusión que con random forest y los valores que mejor se predicen son el rating 3.5 y 4.

<img src="https://github.com/user-attachments/assets/90a1c929-5b30-49e7-b33c-3a325460335c" width="374" alt="image" >

Sobre la curva de aprendizaje se pueden hacer comentarios interesantes:

El puntaje del conjunto de entrenamiento que oscila alrededor de 0.3 indica que el modelo no logra ajustar completamente los datos de entrenamiento. Esto puede sugerir un subajuste (underfitting), donde el modelo no es lo suficientemente complejo para capturar las relaciones entre las características y la variable objetivo.
Que el puntaje de prueba comience en -0.1 es preocupante porque sugiere que el modelo inicial tiene un rendimiento muy bajo, posiblemente peor que un modelo ingenuo.

<img src="https://github.com/user-attachments/assets/ad86458d-3b22-4ec4-8347-edfbeb673ea5" width="385" alt="image" >

<img width="443" alt="image" src="https://github.com/user-attachments/assets/e9452525-21b6-45a0-8a9b-c318ad52cfd2" />

#### 4.2.2 Word2vec

##### 4.2.2.1 Random Forest

Para los análisis se hará uso de un torch size de (20130,100) la dimensionalidad de 100 se justificó previamente pero dimensionalidad 100 permite un equilibrio entre eficiencia y rendimiento, además que para el número de recetas y longitud de las recetas una dimensionalidad de 100 es suficiente, se hará una prueba con 200 más adelante para confirmar esto.

Resultado para 50 árboles de decisión:

<img  src="https://github.com/user-attachments/assets/429f7d5d-d550-42a6-9458-8894a060d8f8" width="230" alt="image">

Con validación cruzada se confirma la consistencia de este resultado, MSE con validación cruzada: 1.4465

<img src="https://github.com/user-attachments/assets/ded1321f-201c-4517-8464-25bbe80c3091" width="400" alt="image" >
<img  src="https://github.com/user-attachments/assets/751c78fd-c00d-4941-a2f3-eac067fb3b63" width="400" alt="image">

Si se usa la representación vectorial con dimensionalidad 200 se obtiene el siguiente MSE:

<img  src="https://github.com/user-attachments/assets/d89b08da-0a6c-47e2-b319-1db36f44ea9d" width="225" alt="image">

Por lo tanto, la mejora es infima y no justifica el hecho de duplicar la dimensionalidad. 

Al igual que antes se realiza un análisis de hiperparametros con GridSearch pero fijando el dataset de entrenamiento a todo el conjunto ya que computacionalmente es viable y se obtienen los siguientes resultados como mejor modelo:

<img  src="https://github.com/user-attachments/assets/3fd32550-6580-47a3-b868-069698dc42c8" width="534" alt="image">

También se observa la mejoría que hay al aumentar el número de árboles de decisión pero la mejora no es sustancial y computacionalmente muy costoso.

![image](https://github.com/user-attachments/assets/1d10508d-c1ee-4928-a0f5-a6f91d910e87)

Por último se observa la Distribución de las predicciones vs. valores reales

<img src="https://github.com/user-attachments/assets/2933fa04-3afd-42e4-a3e7-c7118dce09d4" width="425" alt="image" >

##### 4.2.2.2 Regresor kNN

En cuanto a los resultados para el regresor kNN utilizando como representación vectorial word2vec se observa una mejora en términos de MSE respecto al regresor kNN para la representación vectorial de TF-IDF.

<img  src="https://github.com/user-attachments/assets/5c063163-c38d-499d-b703-f15dbb042f8f" width="427" alt="image">

Por hacer una comparativa con el mismo k que antes se imprimen los resultados para k=20:

<img width="193" alt="image" src="https://github.com/user-attachments/assets/3c789214-b029-46a1-b222-e0d6c82fe026" />

<img width="386" alt="image" src="https://github.com/user-attachments/assets/ccef2c5e-406b-4704-9ac2-6d00e586d5f5" />
<img width="386" alt="image" src="https://github.com/user-attachments/assets/552f5e9a-da64-4954-94e3-8fe9f4d43343" />

Además para el regresor kNN se realiza un estudio de como afecta la reducción de dimensionalidad al MSE. En un primer barrido, se decide ir eliminando la dimensión i-ésima y viendo como afecta su elminación al modelo. Si para la retirada de alguna característica se observara una empeora significativa en terminos de MSE. Indica que ninguna característica individual tiene un gran impacto en el rendimiento del modelo.

<img width="419" alt="image" src="https://github.com/user-attachments/assets/1b8dd871-4cfa-4a4c-b688-4846924fac89" />

En un siguiente análisis se estudia el impacto que tiene en el MSE la reducción de la dimensionalidad, de donde se observa un mínimo local para 20 dimensiones que se asocia a que al reducir las dimensiones, eliminamos ruido y características menos relevantes que podrían dificultar la identificación de patrones en el kNN. Esto permite que kNN funcione de manera más eficiente, ya que la distancia entre puntos es más fácil de calcular y más representativa. Al aumentar el número de dimensiones el MSE empeora inicialmente porque el modelo empieza a incluir características irrelevantes o ruidosas. A partir de 60 dimensiones el MSE vuelve a disminuir porque, al aumentar las dimensiones, el modelo empieza a recuperar características informativas y relevantes. Para 100 dimensiones, se alcanza el óptimo, lo que sugiere que a esta cantidad de características se logra capturar la información más importante de los datos sin saturar el modelo con ruido.

<img width="424" alt="image" src="https://github.com/user-attachments/assets/7cf404a9-3ebb-4d4e-becd-893b23470963" />

#### 4.2.3 Bert

Para Bert como se ha explicado se trabajará con 10000 recetas por un motivo principalmente computacional. El tamaño de la matriz de embeddings crece con el número de ejemplos, lo que impacta directamente en el consumo de memoria RAM y en el tiempo de entrenamiento del modelo. La dimensión de 768 viene de que la salida final de cada texto procesado proviene de la última capa oculta de la red, que tiene un tamaño fijo de 768 dimensiones para cada token en el caso de BERT-base.

##### 4.2.3.1 Random Forest

Al igual que se ha hecho antes se aplica random forest con 50 árboles de decisión para poder hacer un análisis inicial:

<img width="128" alt="image" src="https://github.com/user-attachments/assets/1117bf13-c6aa-4d79-87c3-df812d3f62ea" />

Los peores resultados de Random Forest al aplicar directamente los embeddings de BERT en comparación con TF-IDF y Word2Vec pueden justificarse por varias razones técnicas y características propias de los embeddings de BERT:

**1-** Los embeddings de BERT tienen una dimensión fija alta (768 dimensiones), que es mucho mayor en comparación con las representaciones de TF-IDF o Word2Vec. Esta alta dimensionalidad puede generar ruido y dificultar que Random Forest capture patrones relevantes, ya que este modelo no maneja bien espacios de características muy grandes sin una reducción previa de dimensionalidad.Esta hipotesis se confirma si reducimos a 500 dimensiones con selectKbest donde se observa que el MSE mejora ligeramente:

<img width="125" alt="image" src="https://github.com/user-attachments/assets/bf1a28cf-97be-410c-859b-949a3305fd1f" />

**2-** BERT embeddings capturan información contextual y compleja de las palabras en el texto. Estas representaciones son densas y altamente correlacionadas, lo cual no se adapta bien a los algoritmos de Random Forest.

**3-** BERT embeddings están diseñados para ser entrada de modelos lineales como redes neuronales que pueden manejar la alta dimensionalidad y las relaciones no lineales presentes en los datos.



## 5. Comparación de lo obtenido con el _fine-tuning_ de un modelo preentrenado con _Hugging Face_





