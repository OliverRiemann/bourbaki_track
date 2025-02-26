l Definiciones de AI, AI contenida en este módulo. Una parte gigantesca de la inteligencia artificial proviene del machine learning. 

## Encajes y redes recurrentes

- Introducción a encajes semánticos
- Word2vec, GLOVE, etc.
- Redes recurrente y _Seq2seq_
- NER
las redes neuronales recurrentes son el primer modelo que genuinamente trata el orden de las características.

- Embeddings = Encajes

### Encajes semánticos

Word2vec es un modelo de procesamiento de lenguaje natural. 

![[Captura de pantalla 2025-01-14 a la(s) 6.46.50 p.m..png]]

¿Cómo definimos la semántica entre vectores?


## Breve repaso de embeddings en NLP

Un encaje es una función que logra construir un diccionario en un lenguaje (Español, inglés, francés, etc.) que le asigna un vector (en el caso de Word2vec)de dimension 300. $$\omega \to \widehat{\omega} \in \mathbb{R}^{300}$$
Estos encajes tienen las siguientes características: 

- Si $\omega \sim \omega'$  entonces $\cos(\hat{\omega}, \hat{\omega}')\approx 1$  
- Si $(\omega_1, \omega_1') \sim (\omega_2, \omega_2')$ entonces $\cos((\widehat{\omega_1} - \widehat{\omega_2}), (\widehat{\omega_1'}- \widehat{\omega_2'}))\approx 1$ 

En palabras, si dos palabras son similares, entonces la medida del coseno entre sus vectorizaciones es igual a uno y si la relación entre una palabra y otra es similar a la relación entre otro par de palabras, entonces la medida del coseno entre sus diferencias es igual a 1.

Un ejemplo de esto es: 

"El gerundio de hablar es hablando"

Si decimos que "hablar" es $\omega$ y que "hablando" es $\omega´$ 

Este modelo es capaz de entender que hay una relación similar entre esos vectores que los vectores de correr y corriendo. 

Incluso modelos como gpt son capaces de dar una respuesta para palabras que quizá no existen como "silla" (quizá respondería silleando).

Otro ejemplo de las capacidades de chatgpt es la capacidad de "mejorar un texto" por ejemplo un correo volverlo formal. Si en la base de datos existe un ejemplo de textos informales y textos formales, entonces chatgpt puede aprender la relación entre este tipo de textos y replicarlo. 

Esa es la importancia de w2v.

La diferencia entre este modelo y [[Grabaciones TM#Latent Dirichlet Allocation|LDA]] es que en LDA identifica qué textos son similares; sin embargo no hay una relación entre las _palabras_.  

Pero podríamos asignarle una vectorización según LDA, es decir, para cada palabra $\omega$ construimos su vectorización $\widehat{\omega} = (x_1, x_2, \dots, x_k)$ donde $x_i$ es 1 si la palabra $\omega$ está en el tópico $i$ y $0$ si no. Pero esto no funciona.

## Ciencia de Materiales, una aplicación interesante sobre W2V

![[Captura de pantalla 2025-01-25 a la(s) 3.50.45 p.m..png]]

## Playground de TensorFlow

[Una pequeña herramienta](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.68284&showTestData=false&discretize=false&percTrainData=20&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false) 

Si queremos ir de un perceptrón a una red neuronal.

## Redes neuronales densas (Word2vec)

### El perceptrón como red neuronal

Supongamos que tenemos una familia de características $x = (x_1, \dots, x_d)$. Para construir una $\hat{y}$ tomabamos una combinación lineal y considerabamos su signo para hacer nuestra predicción. 

![[Captura de pantalla 2025-01-25 a la(s) 5.17.11 p.m..png]]
Donde cada $\beta_i$ es el peso de la combinación lineal

Agregar capas ocultas significa lo siguiente.


# Cómo se entrena W2V

Supongamos que tenemos una base de datos gigantesca, por ejemplo: Wikipedia. Ordenemoslos de la siguiente manera: 

$\text{Wikipedia} = A_1, A_2, \dots, A_N$  

## Caso de estudio

El código para nuestras redes neuronales recurrentes estará en el siguiente [gist de colab](https://colab.research.google.com/gist/OliverRiemann/8a21f91987073b6a84ca1c3b60b045da/reconocimiento-de-entidades-nombradas-mediante-rnn.ipynb)
## Redes recurrentes

¿Por qué usar Word2vec? 
Pensemos en un modelo de riesgo de crédito. 

En la clase del martes 21 hay un ejemplo de cómo se arma la matriz.

