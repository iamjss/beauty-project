# B34uty is in the Eye of a Computer?
Este proyecto tiene como objetivo el identificar el nivel de atractivo facial de una persona, en base a un dataset con ratings ya incorporadas.
El dataset elegido ha sido: [**The Chicago Face Database, Version 2.0.3 de Julio 2016**](https://chicagofaces.org/default/), que provee fotografías en HR de tanto hombres como mujeres de diferentes razas. A su vez, el dataset incluye atritutos físicos como votaciones de características subjetivas, como es el atractivo.

## Procedimiento
El procedimiento es tratar las imágenes para que el programa pueda aprender de ellas mediante un modelo de Machine Learning de redes neuronales. Con este modelo se entreta a nuestra máquina para que sea capaz de analizar y dar un rating a una fotografía.

### 1er Paso
Importamos las librerías necesarias para el tratamiento de datos.
En este caso, nuestro dataset contiene información que no necesitamos por lo que nos quedamos únicamente con el identificador de cada usuario y su valoración estética. Dado que los rasgos faciales no parecen muy fiables, también los eliminamos y obtenemos los puntos faciales manualmente.

### Obtención de datos de las imágenes
Al ser tan grandes las imágenes, las añadimos a una variable convirtiéndolas a escala de grises (puesto que una imagen a color es de 4 dimensiones y así reducimos su dimensionalidad a 3) y reduciendo su tamaño de manera proporcional a 140x200.
De igual modo, extraemos los puntos faciales o *landmarks* de cada imagen y los asignamos a otra variable.
![Imágenes resizeadas y con landmarks](https://github.com/iamjss/beauty-project/blob/master/images/example_landmarks.png?raw=true)

### Trabajo con los datos
Creamos un CSV con los datos obtenidos por los landmarks y por otro lado, en un DataFrame nos quedamos con las imágenes en formato píxel y su rating correspondiente, al cual le aplicamos unos BINS para transformarla de una variable continua a una discreta y también lo guardamos en un CSV. 
Ambos se pueden encontrar en la carpeta */output*.

### Algoritmo de Machine Learning
Vamos a trabajar con una red convolucional, pero para ello primero dividimos los datos en un 80%-20% para entrenamiento y testeo, correspondientemente.
El modelaje se realiza con unos batches o bloques de 20 y 10 vueltas o epochs completas a los datos.
![alt text](http://i67.tinypic.com/2pz9po0.png)
De ahí obtenemos un accuracy de un 0.40 para un test loss de 1.50. Sin duda este modelo es mejorable con la inserción de más capas, y luchando contra el overfitting ya que hubo en algún caso en el que contaba con un accuracy en el rango del 90% pero cuanto más incrementaba, mayor pérdida había de datos ya que menos generalista era.

## Comprobación del modelo
Probamos con una imagen del test para ver qué nota nos asigna y como podemos comprobar:
![Imagen de test y nota](https://github.com/iamjss/beauty-project/blob/master/images/model_test.png?raw=true)
La sitúa entre el 3 y el 4, que es efectivamente la nota que tiene, por lo que podemos comprobar que con un acierto de un 40% asigna mediamente bien que está entre esas notas.

## Pasos para el futuro
Sin duda hay que mejorar el modelo y profundizar en él para que tenga un mayor acierto.
A largo plazo sería interesante que se le aplicase un sistema de recomendación de diferentes cirugías faciales para poder mejorar esa nota en función de los datos que tenemos.