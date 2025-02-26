El tema de esta semana es Topic Modeling

- Introducción
- Modelos generativos y medida del coseno
- Latent Dirichlet Allocation
- Sistema de recomendación de libros
- Dudas y problemas
- Sistemas de recomendación (Una hora)

# Topic modeling

Topic modeling es una herramienta parecida al _clustering_, la sutileza que lo diferencia en este caso nuestros registros son textos. Este caso en un sistema _no_ supervisado.

## Sistema de recomendación

Son problemas típicamente no supervisados. 

Algunos ejemplos paradigmáticos son: 

- Google: Sistemas de ranking (Page rank). 
- Netflix: Collaborative filtering
- Amazon: Content-based
- TikTok: Online Learning
- Waze: Optimización de rutas

## Dataset

El dataset con el que trabajaremos esta semana consiste en que cada registro es un resumen de un libro. Por ejemplo: Si tenemos un registro que habla de un evento histórico como la revolución francesa, quisiéramos recomendar libros que contengan palabras similares. 
## Dificultades

A continuación vamos a describir una de las dificultades que se presentan al entrenar un modelo de aprendizaje no supervisado. 

- Función objetivo: Ya que es un aprendizaje no supervisado, no existe $y$ con la que podamos comparar $\hat{y}$, por lo cual no podemos definir una función objetivo la cual queremos optimizar.
- Métrica de evaluación: No tenemos matriz de confusión, no tenemos una idea de cuál es nuestro error $\epsilon$ 
- Maldición de la dimensión: Las nociones de distancia no funciona correctamente debido a la maldición de la dimensión. Utilizando la distancia euclideana:   $$dist(x,x´) = ||x-x´||_2$$ El problema con esta distancia es el siguiente: $$\mathbb{P}(dist(x,x´´) = \delta)) \approx 1$$ para cada $x´´$ en nuestras observaciones y para un $\delta$ dado. Esto se cumple cuando $d \rightarrow \inf$.

## Modelos generativos

Hasta ahora hemos usado $$\mathbb{P}(Y|X)$$ es decir, condicionado a las características $X$ qué tan probable es que $Y$ pertenezca a un cluster. En este caso $Y \in \{T_1, \dots, T_K\}$. En un modelo generativo calcularíamos la siguiente probabilidad $$\mathbb{P}(X|Y)$$ es decir, condicionado al tópico $Y$, cuál es la probabilidad de que aparezcan las características $X$.

El modelo generativo más sencillo es el siguiente $$\mathbb{P}(X|Y) = \mathbb{P}(X_1|Y)\mathbb{P}(X_2|Y)\dots\mathbb{P}(X_d|Y)$$ En este modelo se asume que todas las palabras u observaciones son independientes entre sí. La independencia la podemos interpretar intuitivamente como la correlación. Este modelo se parece mucho a un concepto que se parece al concepto de [[Grabaciones ST|Ruido blanco]]. 

Un modelo generativo más realista que el ruido blanco sería cuando hay una dependencia entre las palabras. Incluso podríamos considerar un modelo generativa cuando consideramos la dependencia entre las dos palabras anteriores. 

Esto podría llevar al sobreajuste, pues si consideramos muchas palabras anteriores, ofreceríamos una predicción estadística no significativa.

Este tema lo seguiremos trabajando el el siguiente [colab](https://colab.research.google.com/gist/OliverRiemann/3da8e78a5300a3aa04f7f8ae02b0f7ce/modelos-de-lenguaje-usando-n-gramas.ipynb) 

## K-means (clustering)

Nuestra base de datos es un conjunto de registros de tamaño N como el siguiente $$S = \{x_1, \dots, x_N\}$$ Donde $x_i \in \mathbb{R}^d$ 

## Programación

La codificación de este algoritmo lo voy a hacer en este [colab](https://colab.research.google.com/gist/OliverRiemann/82efaaac7b6929414fa6443eef47d47f/recomendaci-n_de_libros_usando_lda.ipynb) 

## Knowledge check

La siguiente gráfica es un modelo de representación gráfica de un modelo _smoothed_ de LDA.
 
![[Captura de pantalla 2024-12-21 a la(s) 11.05.39 a.m..png]]
1. ¿En qué problema aplicarías el algoritmo visto esta semana?
	- Respuesta: En una base de datos supervisada, donde los artículos vendidos se ponen en categorías para hacerle separación por tópicos.
# Latent Dirichlet Allocation

Supongamos que tenemos una base de datos con textos: $\{T_1, T_2, \dots, T_N\}$, cuando hacemos Topic modeling obtenemos una familia de distribuciones por cada uno de los tópicos $\{\mu_1, \mu_2, \dots, \mu_k\}$ donde para cada $\mu_i$ tenemos $\mu_i = \{\mu_{1,i}, \mu_{2,i}, \dots, \mu_{d,i}\}$, es decir, para cada tópico $\mu$ tenemos la probabilidad de que aparezca la palabra $1$ en el tópico $i$ (y eso para todas las palabras). 