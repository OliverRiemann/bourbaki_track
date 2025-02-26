[Gist de la clase del martes](https://colab.research.google.com/gist/OliverRiemann/8aac85d5c54a637d09ef686f0ed68be7/estrategia-exploraci-n-explotaci-n_multi_armed_bandit.ipynb)

Bandido multibrazos. Cómo podemos aproximar la campaña más adecuada. 

Supongamos que tenemos una serie de experimentos $\{X_1, X_2, \dots, X_k\}$, donde los posibles valores son $-1 \text{ y } 1$ y un presupuesto $N$, lo que busca el bandido multibrazos, es básicamente lo siguiente: $$k^* = \arg\left(\max_{k \in K}\{\mathbb{P}(X_k = 1)\}\right)$$ Es decir, buscamos qué experimento es el que maximiza la probabilidad de éxito.

La estrategia más ingenua hace lo siguiente: 

| $X_1$    | $X_1$    | $\dots$  | $X_k$    |
| -------- | -------- | -------- | -------- |
| 1        | -1       | $\ddots$ | 1        |
| $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ |
|          |          |          |          |
Donde la longitud de la tabla es $\frac{N}{K}$ y $\mathbb{P}(X_i = 1)= \frac{1s}{N/K}$

La estrategia epsilon-greedy funciona de la siguiente manera: 

- Fijamos un umbral de explotación, digamos $\epsilon \in (0,1)$, simulamos una variable aleatoria de Bernoulli con probabilidad $\epsilon$ 
-  Si ganamos en este lanzamiento elegimos uno de los experimentos de manera aleatoria uniforme.
- Si perdemos este lanzamiento elegimos aquella acción que hasta este momento ha maximizado la recompensa.

![[Captura de pantalla 2025-01-30 a la(s) 4.29.49 p.m..png]]

## Aprendizaje por refuerzo

- Proceso de decisión de Markov
- Relación con aprendizaje supervisado
- Q-learning (algoritmo). Esencialmente Bandidos Multi-brazos + Ecuaciones de Bellman.

### Proceso de decisión de Markov

Podemos pensarlo como muchos nodos $\{S_1, S_2, \dots, S_D\}$, donde cada uno de estos nodos representa un problema distinto de bandidos multi-brazos. Podemos representar las características de un problema de bandidos multi-brazos por flechas que conectan a cada uno de estos nodos. A cada una de estas flechas les llamaremos acciones.

![[Captura de pantalla 2025-01-30 a la(s) 5.03.02 p.m..png]]

Un proceso de Markov, $$M = \left(S, A, p, r\right)$$ Donde $p$ es una función de probabilidad $$p(S,a,S') = \mathbb{P}(S'|S,a)$$ es decir, la función $p$ calcula la probabilidad de llegar al estado $S'$ dado que estamos en el estado $S$ y ejecutamos la acción $a$. 

![[Captura de pantalla 2025-01-30 a la(s) 5.39.42 p.m..png]]


En el ejemplo de las campañas publicitarias tendríamos la siguiente situación; suponiendo que cada uno de los nodos representa el mes en el que estamos pautando, es un diferente problema multi-brazos en el que tenemos que decidir cuál de las acciones es mejor. 

Estos estados corresponden a diferentes momentos. 

Otro ejemplo de esto es el ajedrez, donde cada nodo representa una posición del tablero, en este caso las acciones corresponderían a mover una pieza. En este caso la función $p$ sería la probabilidad de llegar a una posición dado que de una posición anterior ejecutamos cierto movimiento.
# Políticas
$$\pi: S \to A$$
una política es una función que a cada estado me regresa una acción. Nuestro objetivo es encontrar una $\pi^*$ (similar a $k^*$) que maximice nuestras recompensas.
# SL vs RL





