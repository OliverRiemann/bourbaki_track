## ¿Qué es Machine Learning?

Machine learning es un conjunto de técnicas que nos permiten hacer pre-
dicciones utilizando información del pasado. En este curso hablaremos con detalle del perceptrón que es un primer ejemplo de un algoritmo que produ-
ce una red neuronal para hacer predicciones. El perceptrón es un algoritmoque corresponde a la fase de entrenamiento de una red neuronal de una capa,
fue ideado por F. Rosenblatt.

Criterio para la mayor parte de modelos de machine learning, l

## Modelo Vs Algoritmo

En la jerga de la ciencia de datos modelo y algoritmo son palabras que pueden
confundirse sin mayor incoveniente. Sin embargo, a lo largo de este curso y
por cuestiones diácticas, distinguiremos dos etapas al abordar un problema.

La primera será el algoritmo, que corresponde al entrenamiento o aprendizaje; y una segunda etapa a la que denominaremos modelo que ya dispone del entrenamiento para realizar predicciones.

## Perceptrón

A lo largo del curso supondremos que un problema clásico de aprendizaje
supervisado tipo clasificación binaria en $R_d$, donde buscamos entrenar a nuestro modelo con un conjunto de ejemplos

$$S = \{(x_1,y_1), \dots, (x_N, y_N)\}$$

Donde $x_i \in R^d$ son las variables explicativas y $y_i \in \{-1, +1\}$ es la supervisión (Utilizamos los valores 1 y −1 para clasificar nuestros registros, pero podría ser cualquier clasificación binaria) 
## Dos etapas

### Aprendizaje

Astucia matemática que le permite a la computadora aprender patrones de la base de datos.
### Modelo

Función que el algoritmo aprendió con la cual puedo hacer inferencias

### Vectorizar

La imagen la podemos definir como
$x = (x_1, x_2,... x_d)$ donde d es el número de características donde $x_i$ es un elemento del 0 al 252.

En estas secciones nos vamos a centrar en el modelo. 

El modelo lo vamos a llamar beta. En este caso vamos a usar una suma ponderada

![[Captura de pantalla 2024-11-06 a la(s) 7.44.26 p.m..png]]

nótese que beta también es 
 $$\beta = (\beta_1, \beta_2,... \beta_d)$$
el modelo es esta función 

![[Captura de pantalla 2024-11-06 a la(s) 8.14.25 p.m..png]]

## Perceptrón

La actualización se hace paso a paso con cada $x_i$, cómo se mitiga que actualize su posición sin dejar de separar correctamente los x anteriores, se repite el proceso reordenando la base de datos. Es decir las épocas. Esto es porque el orden de los registros no importan. El último registro que ve el algoritmo es la mas importante porque es la que se quedó el modelo.

## Los árboles de decisión

Subajuste: Cuando el error en el conjunto de entrenamiento es muy grande. 

Sobreajuste: Cuando el error en el conjunto de test es muy grande. 

## Churn rate e interpretabilidad

Preferimos un modelo que no sea muy bueno. Preferimos un modelo que sea interpretable. 

Los modelos están en un espectro donde de un lado está en la precisión y en el otro lado es la entrerpretabilidad.

Hay un tradeoff entre estas dos características.

### Qué es el churn rate

- Tasa de abandono
- retención de clientes
- estrategias de marketing
- diseño del producto

Lo que intentamos predecir con el modelo es quiénes de los clientes nos va a abandonar. Este es un modelo de clasificación.

 #### Tres técnicas para el chrun rate
 
 - Clasificación binaria
 - Multi-clase
 - Análisis de supervivencia
Los problemas es categórica o no categórica 

El problema del churn rate se puede afrontar a través de un análisis de supervivencia. 

## Performance vs. interpretabilidad

Desempeño contra interpretabilidad, cada vez más es más frecuente que las decisiones que tomemos dependen de algoritmos entrenados por machine learning. 

La ley rider, 

Necesitamos un filtro de seguridad. 

Necesito volver a ver la parte de definición de arboles de decisión, mas o menos es a la hora después de empezar la clase.

Definición: Un árbol con profundidad r <= d  es una familia ordenada de pregunta x_j = 0 o x_j = 2 donde el último nodo es x_jr

Un arbol es un feature selection. Un conjunto de 

Decisión: Una decisión se toma en base de un arbol. Para decidir

Las propiedades no pueden ser de tipo factor sin orden. i.e. Algún estado, algún código postal, un número de telefono.

Las variables no pueden contener valores nulos.

Tenemos una base de datos compuesta exclusivamente con datos binarios. Las variables numéricas las transformadas de la siguiente forma: Buscamos un umbral tal que si el valor numérico cae en cierto nivel del umbral le asignamos un valor binario. Esto lo hace scikit.learn de manera interna al entrenar al modelo. 

Entropía: Es una función que cuantifica la incertidumbre. Con dominio del 0 al 1 y un rango de 0 a 1, ![[Captura de pantalla 2024-11-14 a la(s) 7.53.39 p.m..png]]
Esta función mide el desbalance. 

La entropía de un espacio de probabilidad es la suma de las entropías. 

Para decidir cual es el orden de las features, el algoritmo primero mide la entropía de todas las variables y se queda con la que menos entropía. Así continúa para los siguientes variables. 

# 18/11/2024

22min: Introducción al tema de la semana. Regresión logística. En este 

31min: Sesgo. Clasificaba como falso correctamente por las razones equivocadas.

40min: Vectorización del texto

41min: 

45min: Interesante reflexión

52man: Errores graves

53: 

59: Bag of words

60: La combinatoria de palabras

7:46: bolsa de palabras ejemplo

7:46: Vocabulario, el conjunto de palabras que se usan en el "corpus".

Se guarda de forma rectangular, donde cada columna indica el número de veces que aparece en un dado texto

7:48: Pesado boleano, donde la columna indica la presencia de la palabra en un texto dado

7:49: Otra métrica de definir el vocabulario

7:50 características de bolsa de palabras, o vocabulario

7:59: stopwords

7:59: conteo de palabras

8:00: otras características de preprocesamiento

8:03: Matriz dispersa: Tiene muy pocos elementos distintos a cero

8:05: Randomtree 

8:07: Las bibliotecas que se usan

8:15: Exploración de los datos. Una función interesante describe.

8:17: Preprocesamiento

8:20: Regular expression

8:22: Otra función de transformación de texto

8:24: Normalización

8:26: Stimming en el colab

8:28: Otra librería de lenguaje natural

8:32: Definición de la bolsa de palabras particular.

# 20/11/24

23min: Bolsa de palabras

26min: Reducir dimensionalidad

27min: Palabras o tokens

30min: Lematizer

32min: TF-IDF

33min: nuestra x

36min: Pregunta, respuesta mía, porque no nos da mucha información, 

38min: Comentario importante, cómo elegir la escala

41min: Cómo elegir una escala

42min: Cómo elegir una nueva escala

44min: Ejercicio moral, reescalar el perceptrón

44min: Por que la frecuencia es mejor que el binario

46min: Aquellos 

47min: Las mayúsculas

document frequency, cuántas veces aparece la palabra i en la base completa

N es el tamaño del dataset, es la cardinalidad del conjunto de los datos

Un dataset que 

52min: Leyes de potencias, la ley de ZIP

Muy poca cantidad de información

53min: definición de dfi

63min: TF-IDF

69min:

1hr 15min: por que utilizamos el logaritmo.

8:06: Función sigmoide, donde casi siempre es casi 0 o casi siempre es casi 1 Sigmoide

# 21/11/24

10min: bigramas

18: Vectorización mediante BOW

22: Parametro de ridge en LogisticRegression

30: Maryúsculas para matrices y minúsculas para vectores

30: Definición de función evaluación

35: Los coeficientes beta

35: La pregunta de los $$lambda$$
36: Documentación logística

39: Proposición de lambdas

7:16: cross validation

7:22 más del crossvalidation

7:38: Grid search results

7:39: Descripcion de la tabla

7:42: Mejor parametro

Cómo parametrizamos la función

Como predice con probabilidad
Tarea moral: Jugar con la definición de deceptive

8:01:  Histograma de probabilidad es deceptive

8:07: Curva rock

8:12 Clasificador rl para probar otra curva 

8:20: Pasarlo por la función exponencial

# 22/11/24

5:12min: Combinar los entrenamientos y prueba.

"Cuando hacemos cross validation es una versión radical en la separación entre entrenamiento y prueba, es una versión que intenta ser más robusta que solo tomar un conjunto de entrenamiento y un solo conjunto de prueba. Estamos siendo más rigurosos a la hora de elegir nuestros hiperparámetros."

La promesa de _machine learning_: Mientras más datos tengas, mejor se van a entrenar los modelos. 

Paráfrasis: El cross validation nos ayuda a encontrar los mejores _parámetros_, para construir el modelo, usamos estos parámetros, el CV no construye el modelo.

19:25min: Optimizadores

Tendremos una sesión el martes a las 7pm.

El examen consistirá de dos partes, un exámen práctico y un exámen teórico. Las indicaciones para estos se encuentran en el curso ML for the working analist en la pestaña "Exámen Módulo I"

El exámen práctico: Es construir un modelo para detectar cuando una compra en internet es fraudulenta o no fraudulenta. 

Ahí está el dataset, es una base de datos supervisada, los datos ya están en parte preprocesados (no hay que trabajar en la base de datos original, hay que trabajar sobre la base FraudeCanastas.csv). La gran mayoría de características son columnas de productos que pueden haber en estas canastas, las unidades o el peso son las unidades que se compraron por el costo unitario del producto.  Al final de la lista de columnas hay campos que de alguna manera resumen la información de la compra (Costo promedio, costo máximo costo mínimo, etc.) 

El objetivo es que utilicemos las técnicas que se han enseñado en ese curso. En el notebook no solamente hay que solamente desarrollar el código, también hay que justificar y comentar nuestro proceso. En este exámen no se va a premiar que se usen algoritmos sofisticados. Lo que va a contar es que lo que aprendimos en esta semana sea usado con el propósito con el que nos enseñaron. 

El exámen conceptual: Es un exámen oral en parejas que van a hacer (lo más probable) el jueves y viernes  que dura 20 min. Es una reunión por cada pareja, nos hará preguntas conceptuales sobre lo que hemos aprendido en este curso. Se espera que estudiemos. El consejo es que estudiemos todo, que nos "hagamos buenísimos en todo lo que hicimos". 

La información sobre las parejas y el horario que tomaremos el exámen nos llegará el Lunes a través de un correo. Hay un día máximo para confirmar el exámen, es importante confirmarlo. 

Información extra I: Las sesiones de la siguiente semana no son para aprender un nuevo algoritmo. La primera sesión para dudas generales que podamos tener sobre el examen. El miércoles es probable que no haya sesión. 

Información extra II: En la sesión de dudas del martes se hablará de optimizadores que es un tema mucho más técnico.



¿Tengo que estudiar cuál es el beneficio de ridge sobre la regresión logística usual?

También hay un grupo de whatsapp.

La curva rock que definimos es la siguiente: 

La curva rock vive en un plano cartesiano, particularmente en el cuadrante dentro de 

Donde un eje es los falsos negativos, otro es los verdaderos positivos.

**CURVA ROCK**: 1:55:00


Métricas de cross validation. No estamos cambiando nuestra función de error. 

