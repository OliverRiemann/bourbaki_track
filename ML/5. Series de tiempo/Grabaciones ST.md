- ¿Cómo son las bases de datos? (Supervisado o no)
- Ruido blanco vs Auto-regresivo
- ARMA (estacionarios), ARIMA (retornos)
- Componentes de una serie de tiempo

# Cómo se ve la base de datos

Sea $$S = \{z_1, z_2, \dots, z_T\}$$
donde S es un conjunto de datos _ordenados_

![[Captura de pantalla 2024-12-12 a la(s) 4.11.04 p.m..png]]

En la gráfica anterior el eje de las $x$ está el tiempo $t$ en alguna escala (semanas, segundos, trimestres, años) y en el eje vertical $y$ está el valor que estamos registrando. 

Podríamos pensar en una base de datos supervisados con la siguiente estructura

| $X$      | $Y$      |
| -------- | -------- |
| 1        | $z_1$    |
| 2        | $z_2$    |
| $\vdots$ | $\vdots$ |
| T        | $z_T$    |
El problema con esta base de datos, como lo hemos aprendido con las anteriores lecciones de machine learning es que las variables explicativas son solo un dígito, no tenemos mucha información sobre nuestros registros.

En este caso usaremos la siguiente estructura de base de datos.

| $X_1$       | $X_2$       | $\dots$  | $X_p$     | $Y$       |
| ----------- | ----------- | -------- | --------- | --------- |
| $z_1$       | $z_2$       | $\dots$  | $z_p$     | $z_{p+1}$ |
| $z_2$       | $z_3$       | $\dots$  | $z_{p+1}$ | $z_{p+2}$ |
| $\vdots$    | $\vdots$    | $\ddots$ | $\vdots$  | $\vdots$  |
| $z_{t-p+1}$ | $z_{t-p+2}$ | $\dots$  | $z_t$     | $z_{t+1}$ |
| $\vdots$    | $\vdots$    | $\ddots$ | $\vdots$  | $\vdots$  |
| $z_{T-p}$   | $z_{T-p+1}$ | $\dots$  | $z_{T-1}$ | $z_T$     |

Nótese cómo mezclamos de cierta manera las variables explicativas y la variable objetivo.

Esto es esencialmente explicar una observación con las $p$ observaciones anteriores. 

$$z_t \approx \hat{z_t} = f(z_{t-1}, z_{t-2}, \dots, z_{t-p}) $$

Podemos quizá entrenar una [[Grabaciones RL|regresión]], es decir:  $$\hat{z_t} = f(z_{t-1}, z_{t-2}, \dots, z_{t-p}) = \beta_1z_{t-1} + \dots + \beta_pz_{t-p}$$
Esto es lo que se conoce como un modelo _autoregresivo_ pues estoy haciendo una regresión conmigo mismo. Esto es la parte AR de ARMA, ARIMA, ARCH, etc.

Ya que hemos construido nuestra base de datos, ahora la siguiente pregunta es cómo elegimos a nuestra $p$.  Lo que estamos buscando es una estadística que se refleje en toda la serie de tiempo. 

# ACF 

Vamos a calcular la correlación que existe en las siguientes dos columnas. 

| $X$         | $X^´$     |
| ----------- | --------- |
| $z_1$       | $z_{1+p}$ |
| $z_2$       | $z_{2+p}$ |
| $\vdots$    | $\vdots$  |
| $z_t$       | $z_{t+p}$ |
| $\vdots$    | $\vdots$  |
| $z_{T-p-1}$ | $z_{T-1}$ |
| $z_{T-p}$   | $z_T$     |

Si calculamos $Corr(X, X')$, estamos preguntándonos cómo se relaciona $t-p$ con $t$.  Esperamos observar algo como la siguiente gráfica

(Nótese: 
- Cómo el rango de la función es $\left[-1, 1\right]$
- Cómo el dominio de la función es $\left[0, \inf \right]$
- Cómo esperamos que $$\lim_{p \to \infty} ACF_S(p) = 0$$)

![[Imágenes/Captura de pantalla 2024-12-30 a la(s) 9.13.36 a.m..png]]

### Ruido blanco

Cuando no influye el tiempo anterior, cuando el $AC(1), AC(2), \dots, AC(n) = 0$, es decir, los eventos anteriores no influyen para la situación actual o las futuras.

Lo siguiente que veremos en esta clase lo haré en este [colab](https://colab.research.google.com/gist/OliverRiemann/fb885e172961d925227fffc434dd56d2/regresi-n-ruido-y-series-de-tiempo.ipynb#scrollTo=IjVm5hNxnPrC) 

El Ruido blanco se ve algo así: 

![[Pasted image 20241230134409.png]]

Y su gráfica de autocorrelación se ve algo así: 
![[Pasted image 20241230134601.png]]

Mientras que la simulación de un proceso autorregresivo (AR) se ve así: 

![[Pasted image 20241230134440.png]]

Y su gráfica de autocorrelación correspondiente se ve algo así: 
![[Pasted image 20241230134510.png]]

## Tain vs Test

Dividir entre Train y Test en un modelo de serie de tiempo necesariamente tiene que corresponder a lo que vemos en la siguiente gráfica: 

![[Captura de pantalla 2024-12-30 a la(s) 2.10.51 p.m..png]]

Es decir, el test tiene que ser el pasado inmediato, a diferencia de los demás modelos que puede ser un sampleo aleatorio. 

# $AR(p) + MA(q) = ARMA(p,q)$
Cuando aplicamos un modelo autorregresivo (AR) de orden p a la siguiente tabla

| $X_1$       | $X_2$       | $\dots$  | $X_p$     | $Y$       |
| ----------- | ----------- | -------- | --------- | --------- |
| $z_1$       | $z_2$       | $\dots$  | $z_p$     | $z_{p+1}$ |
| $z_2$       | $z_3$       | $\dots$  | $z_{p+1}$ | $z_{p+2}$ |
| $\vdots$    | $\vdots$    | $\ddots$ | $\vdots$  | $\vdots$  |
| $z_{t-p+1}$ | $z_{t-p+2}$ | $\dots$  | $z_t$     | $z_{t+1}$ |
| $\vdots$    | $\vdots$    | $\ddots$ | $\vdots$  | $\vdots$  |
| $z_{T-p}$   | $z_{T-p+1}$ | $\dots$  | $z_{T-1}$ | $z_T$     |
Nos regresa el modelo $\beta_1, \beta_2, \dots \beta_p$. 

Para cada uno de nuestros registros nosotros podemos comparar $$z_{t+1} \ \text{vs.}\ \widehat{z_{t+1}}\left(= \beta_1 z_t + \beta_2 z_{t-1} + \dots + \beta_p z_{t-p}\right)$$
Donde definimos $$\epsilon_{t+1} = z_{t+1} - \widehat{z_{t+1}}$$
En el caso de las regresiones lineales, nosotros suponemos que 

$$\epsilon_{t+1} \sim N(0, \sigma^2)$$
Si en nuestro error resulta que se parece más a una distribución de Laplace, entonces hubiera sido mejor entrenar un modelo de autorregresión con la regresión de Huber.

A continuación vamos a construir una base de datos utilizando los errores anteriores a un registro, como se muestra en la siguiente tabla.

| $X_1$       | $\dots$  | $X_p$     | $X_1^{'}$          | $\dots$  | $X_q^{'}$        | $Y$       |
| ----------- | -------- | --------- | ------------------ | -------- | ---------------- | --------- |
| $z_1$       | $\dots$  | $z_p$     | $\epsilon_1$       | $\dots$  | $\epsilon_q$     | $z_{p+1}$ |
| $z_2$       | $\dots$  | $z_{p+1}$ | $\epsilon_2$       | $\dots$  | $\epsilon_{p+1}$ | $z_{p+2}$ |
| $\vdots$    | $\ddots$ | $\vdots$  | $\vdots$           | $\ddots$ | $\vdots$         | $\vdots$  |
| $z_{t-p+1}$ | $\dots$  | $z_t$     | $\epsilon_{t-q+1}$ | $\dots$  | $\epsilon_t$     | $z_{t+1}$ |
| $\vdots$    | $\ddots$ | $\vdots$  | $\vdots$           | $\ddots$ | $\vdots$         | $\vdots$  |
| $z_{T-p}$   | $\dots$  | $z_{T-1}$ | $\epsilon_{T-q}$   | $\dots$  | $\epsilon_{T-1}$ | $z_T$     |
Con esto podemos entrenar un nuevo de modelo de regresión del tipo $ARMA(p,q)$ donde 
$$\widehat{z_{t+1}} = \beta_1 z_t + \dots + \beta_p z_{t-p} + \theta_1 {\epsilon_{t-1}} + \dots + \theta_q \epsilon_{t-q} $$
La primera parte corresponde al modelo autorregresivo ($AR(p)$) junto con los errores que comete el modelo de autorregresión ($MA(q)$).

## La interpretación del _hiperparámetro_ q

Supongamos que $$\theta_1 = \theta_2 =  \dots =  \theta_q = \frac{1}{q}$$ entonces $MA(q)$ sería
$$\sum_1^q \frac{\epsilon_{t-i}}{q}$$ 
En una serie de tiempo, nuestra predicción del moving average

![[Captura de pantalla 2024-12-30 a la(s) 3.27.26 p.m..png]]

se haría cada vez más _regular_, lo que hace entonces nuestro hiperparametro q es no permitir que haya saltos muy descontrolados.

## Series de tiempo estacionarias ($\neq$ Estacionales)

Los modelos ARMA con dos parámetros p y q son las series de tiempo Estacionarias, lo cual no es lo mismo que estacionales. 

Algunos ejemplos de estacionales son por ejemplo: 

- En cada navidad aumentan la venta de boletos de avión
- Cada halving en bitcoin aumenta $x$ cosa
-  Las glaciaciones de la tierra

$$ARMA(p,q) \iff \text{Estacionario}$$
### Estacionario (Stationarity)

Un proceso estocástico es estacionario si

Proceso estocástico: $z_1, z_2, \dots, z_T$ 

1. $\mathbb{E}[z_1] = \mathbb{E}[z_2] = \dots = \mathbb{E}[z_T]$ 
	1. Un proceso estocástico _no_ estacionario sería, por ejemplo, una serie de tiempo como la siguiente, que tiene tendencia (trend): ![[Captura de pantalla 2024-12-30 a la(s) 4.33.50 p.m..png]]
2. $\mathbb{V}[z_1] = \mathbb{V}[z_2] = \dots = \mathbb{V}[z_T]$ donde $\mathbb{V}$ es la varianza. 
	1. En la siguiente serie de tiempo la varianza _no_ es constante pero sí tiene valor esperado constante: ![[Captura de pantalla 2024-12-30 a la(s) 4.44.34 p.m..png]]
3. $Corr(z_{t-i},z_t) = Corr(z_{t^{'}-i}, z_{t^{'}})$
	1. Básicamente que siempre que haya una ventana de tiempo $i$, la observación $z_{t-i}$ afecte tanto a la variable $z_t$ tanto como la variable $z_{t^{'}-i}$  afecta a $z_{t^{'}}$.

Lo que se hace normalmente es lo siguiente: Dada una serie de tiempo hacemos una serie de tests estadísticos para demostrar que es Estacionaria. Si no es estacionaria, buscamos formas de convertirla en estacionaria.

 Dada una serie de tiempo _no_ estacionaria $z_1, z_2, \dots, z_T$, existen dos transformaciones comunes para volverla estacionaria: 

- $\overline{z_t} = z_t - z_{t-1}$ 
- $\overline{z_t} = \ln({z_t})$ 

Supongamos que tenemos una serie de tiempo
$$z_t = m\cdot t + \epsilon_t$$
donde $\epsilon_t \sim N(\mu, \sigma^2)$ 

Si realizamos la primera transformación obtendríamos

$\overline{z_t} = z_t - z_{t-1} = m + \epsilon_t - \epsilon_{t-1}$ 

La cual es estacionaria ¿Por qué?

---

AQUÍ ME FALTAN NOTAS 

---

Las siguientes notas, correspondientes al 13/12/2024 están en el siguiente [colab]()