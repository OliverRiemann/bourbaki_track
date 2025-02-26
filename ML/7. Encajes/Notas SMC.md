Las siguientes notas son una bitácora de las clases sobre los métodos de Monte Carlo tanto clásicos como cadenas de Markov. 

1. Introducción a las ideas de la simulación de Monte Carlo (una hora)
2. Aproximación de $\pi$ utilizando el método de Monte Carlo (una hora).
3. Muestreos de datos y simulaciones MC o MCMC (dos horas).
4. Estimación del riesgo en vuelos (dos horas).
5. Dudas y complementos sobre el método de Monte Carlo para cadenas de Markov (dos horas).

# Simulación de datos y aproximación de Monte Carlo

El caso particular de uso es cuando las bases de datos no son lo suficientemente grandes como para generar una aproximación del fenómeno que deseamos modelar. Comenzaremos con un tipo de simulación similar a la que supondremos cuando trabajamos con una base de datos clásica

## Método de Monte Carlo y los procesos estocásticos i.i.d.

En la semana VI del curso hablamos sobre las técnicas de procesos autoregresivos para hacer previsiones univariadas a través del tiempo. En esa semana se introdujo el concepto de [[Grabaciones ST#Ruido blanco|ruido blanco]] el cual será utilizado nuevamente en esta sección.

**Teorema (Ley de  los grandes números)**: Sea X una variable aleatoria con varianza finita $\sigma^2$ y $X_1, X_2, \dots$ una familia de variables aleatorias independientes e identicamente distribuidas con $X$ entonces lo siguiente se cumple para todo $\epsilon$: $$\mathbb{P}\left(\left|\frac{X_1 + \dots + X_N}{N} - \mathbb{E}[X]\right| > \epsilon\right) = \frac{\sigma^2}{N\epsilon^2}$$
La probabilidad en esta ecuación está calculada utilizando a la variable aleatoria $X$.

En particular a medida que $N$ se hace más grande entonces el promedio empírico será cada vez más cercano a la varianza. 

