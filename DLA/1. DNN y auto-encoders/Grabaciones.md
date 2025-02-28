Los 10 hitos de la IA, la moraleja: de un 30% a un 60% de los 10 hitos de la inteligencia artificial son sobre redes neuronales

# Taxonomía de las redes neuronales

- **Capas**: Densas, recurrentes, convolucionales, atención, etc..
- **Arquitecturas**: Supervisadas, auto-encoders, encoder-decoder, GAN, etc...
- **Funciones de pérdida**: Error cuadrático medio, error Ridge, cross-entropy, quantile loss, etc...
- **Funciones de activación**: RELU, Softmax, Tangente hiperbólica, etc...
# Capas densas

- Combinaciones lineales
- Numerosas combinaciones lineales

Una capa densa es una combinación lineal, numerosas combinaciones simultaneas, variables latentes. 

![[Captura de pantalla 2025-02-24 a la(s) 6.53.01 p.m..png]]

La neurona *i*esima de la capa oculta.

Nuevamente utilizaremos el playground [[Grabaciones Encajes#Playground de TensorFlow|Playground]] 

## Cómo son las bases de datos en el deep learning

![[Captura de pantalla 2025-02-24 a la(s) 7.07.10 p.m..png]]

¿Por qué no hacer una red neuronal para cada variable objetivo en vez de calcular todas las variables objetivo al mismo tiempo? 

![[Captura de pantalla 2025-02-25 a la(s) 7.53.31 p.m..png]]

¿Qué problemas podemos encontrarnos con esta definición del error?

Aquí hay una respuesta de reddit 

Training a single model on three target variables is equivalent to training three separate models that have shared parameters except for the final layer (assuming a mean squared error loss in both cases), so training a single model effectively regularizes the three models. Whether or not this is a good thing will depend on the dataset, but in the limit of infinite data, three separate models will give you better overall performance than a single model since they won't be regularized.

Aquí hay un artículo que discute [Multiple Output Machine Learning Model - Python,](https://stackoverflow.com/questions/58702812/multiple-output-machine-learning-model-python) aquí otro de [Multioutput Regression in Machine Learning](https://www.geeksforgeeks.org/multioutput-regression-in-machine-learning/) 
# Cómo se entrenan las neuronas

![[Captura de pantalla 2025-02-24 a la(s) 7.15.49 p.m..png]]

Función de activación: Es una función no lineal,  ![[Captura de pantalla 2025-02-24 a la(s) 7.18.48 p.m..png]]

La segunda parte de esta clase la continuaré en este [colab](https://colab.research.google.com/github/OliverRiemann/DeepLearning_Bourbaki/blob/main/Semana%201/Introducci%C3%B3n_redes_neuronales.ipynb#scrollTo=UUl3Pdn8wUoV) 

¿Qué es un tensor? 
In [mathematics](https://en.wikipedia.org/wiki/Mathematics "Mathematics"), a **tensor** is an [algebraic object](https://en.wikipedia.org/wiki/Mathematical_object "Mathematical object") that describes a [multilinear](https://en.wikipedia.org/wiki/Multilinear_map "Multilinear map") relationship between sets of algebraic objects related to a [vector space](https://en.wikipedia.org/wiki/Vector_space "Vector space"). Tensors may map between different objects such as [vectors](https://en.wikipedia.org/wiki/Vector_\(mathematics_and_physics\) "Vector (mathematics and physics)"), [scalars](https://en.wikipedia.org/wiki/Scalar_\(mathematics\) "Scalar (mathematics)"), and even other tensors.

Train, test, evaluation (o validation)

La diferencia entre dataframe y matrices. (en python)

Mientras más épocas más robusto el *entrenamiento*, no el modelo sino el entrenamiento.

Qué es el validation_split

Qué me indica el *loss* 

Cómo interpretar nuestro loss y nuestro mae

Cómo escalar las variables de las demás variables

Funciones lineales vs funciones afines
# Notas del colab

Nótese que modifiqué un poco la definición del modelo simple con el fin de adherirme a las convenciones más actuales. 

- Si la red neuronal solamente usa capas densas, es una red neuronal densa
- Las capas densas, son aquellas que se conectan con todas las neuronas próximas.
- Las capas de mechanism, solamente se conecta con ciertas neuronas.
- La capa de dropout nos deja desactivar algunas neuronas.

# Preguntas del colab de redes neuronales densas

Cuál es la diferencia entre los *pesos* en una regresión logística y redes neuronales

# Auto-encoders

Un auto-encoder es un modelo que fue entrenado de manera supervisada del cuál no teníamos una etiqueta. 

![[Captura de pantalla 2025-02-25 a la(s) 8.02.15 p.m..png]]

Nosotros utilizaremos los auto-encoder densos. 

En este caso de uso cada una de las personas usa una tarjeta de crédito. Supongamos que tenemos $d$ características. Construyamos un autoencoder con la siguiente arquitectura: 

![[Captura de pantalla 2025-02-25 a la(s) 8.05.58 p.m..png]]

Imaginemos a esta capa de neuronas $Z$ como un embudo. 

Este es el dibujo de un problema de compresión. 

¿Qué significa estas $Z$? Es un buen resumen de la base de datos original.

![[Captura de pantalla 2025-02-25 a la(s) 8.17.11 p.m..png]]

El objetivo de este caso de uso es demostrar 

![[Captura de pantalla 2025-02-25 a la(s) 8.18.56 p.m..png]]

Sin funciones no lineales, ¿Cómo es diferente esto de un PCA? La noción de varianza, el error de reconstrucción 

¿Cuál es el problema más dificil de deep learning?