### Predicción del Tiempo de Atención de una Emergencia

#### Introducción

Este bloque está dedicado a aprender sobre regresiones, en particular: 

- Regresiones lineales
- Regresiones de Huber
- Regresiones polinomiales

Vamos a hablar de la diferencia entre las regresiones de Huber y lineales, lo que distingue a las regresiones de Huber son los valores extremos, elegimos una regresión robusta basada en los valores extremos en una variable.

Un conocimiento esperado importante es adecuar el modelo de regresión al tipo de base de datos que utilicemos, en particular, cuando hay presencia de valores extremos en alguna variable va a ser más adecuado usar regresión de Huber. 

## Valores extremos vs Outliers

**Ejemplo**: Supongamos que tengamos una base de datos que consiste en fotos de sillas. Si por alguna razón aparece una foto de una taza de atún o un vaso, este sería un outlier. Si aparece una silla curiosa, una silla artística, este sería un valor extremo. 

Un outlier es un valor que no es parte de nuestra distribución. 

**Ejemplo**: Si estamos estudiando el ingreso de las personas en México. Lo que gana Carlos Slim no es un outlier. Es un valor extremo. Si alguien pone el número de granos de arena en todo el mundo en esta distribución, este es un outlier.

En este curso no haremos distinción entre un outlier y un valor extremo. A los outliers lo consideraremos como un valor extremo y parte de la naturaleza del fenómeno que estamos estudiando.

## Valores extremos

El siguiente [artículo](https://www.rieti.go.jp/jp/publications/dp/14e033.pdf) nos muestra la siguiente distribuciones. 

![[Captura de pantalla 2024-12-06 a la(s) 10.10.10 a.m..png]]

Nótese que tanto la línea verde y azul tiene el mismo promedio. También (un acto de fé) tienen la misma desviación estándar. Es decir, contar las veces que se aleja de la media y cuántas veces lo hace. 

Si nos vamos muy alejados de la media, en este caso el 0, se puede notar  $y_{lap} = g(x) > y_{gauss} = f(x)$, es decir, a medida que $x$ crece para ambos lados, la distribución de Laplace es mayor que la distribución Gaussiana.

En palabras, si hablamos del modelo de Laplace en comparación con la Gaussiana y pensando en histogramas, es muy probable encontrarse con casos extremos en la distribución de Laplace comparado con la Gaussiana. 

El ejemplo concreto que aparece en el artículo mencionado habla de crecimiento de empresas financieras en japón, en este caso, los registros de empresas que crecieron mucho o muy poco es mucho más probable en la distribución de L en comparación con la G. En este caso, el análisis al que llevaron en el artículo concluyó que la distribución empírica de estos crecimientos se parecen más a una distribución de L. Nosotros que argumentamos que esto se debe a la naturaleza del fenómeno, que está muy propenso a valores extremos.

Los valores extremos en una campana de Gauss decrece exponencialmente su probabilidad. A la distribución de Laplace no le pasa esto. 

### Kurtosis

Gráficamente, una de las cosas que distingue la distribución de Laplace era el rápido descenso a la izquierda o a la derecha de su eje de simetría. Sin embargo, estadísticamente, lo que distingue a estas dos distribuciones no es esto, sino el valor alto que tienen sus colas. Esto es la Kurtosis. 

Si tienes Kurtosis se calcula relativa a la distribución gaussiana. 

Detalles técnicos de la Kurtosis o Curtosis se pueden consultar en el tema [Las distribuciones gaussianas](https://drive.google.com/file/d/1Ieu_cJkifPj5J0B6ZhMMpvWM_6KFmoGF/view) de las notas del curso o en [[Notas RL#Las distribuciones gaussianas]]

En conclusión, empíricamente se puede definir la Curtosis como la frecuencia de los valores extremos. 

---

Las demás notas de la clase están en este [colab](https://colab.research.google.com/gist/OliverRiemann/b7f523a2f3a586ca5779a88727b076e6/1_response_time_paris_fire_brigade.ipynb#scrollTo=MOfWHxj0IdEz) (que de hecho es un gist en github) 


# Otras aplicaciones

Este problema se podría relacionar con muchas otras aplicaciones 

- Tiempo de entrega de un paquete
- Tiempo de recorrido

Un problema de regresión no necesariamente es un problema de regresión lineal, es un problema donde nuestra variable objetivo es continua.

# Dificultades

Cuáles hipótesis se cumplen y cuáles no se cumplen

- Hipótesis geométricas
- Hipótesis estadísticas
- Evaluación

Si no me equivoco esta sección es muy parecida a la de [[Notas RL#^567d48]] 

## Hipótesis geométricas


Pensemos en el problema de valuación de una propiedad

| $m^2$ | $MDP$ |
| ----- | ----- |
| 400   | 5.5   |
| x     | y     |
Nuestro modelo sería $y = \frac{5.5}{400}x$. 

Un modelo de regresión lineal de tres dimensiones equivale a aproximar el valor de una variable continua en función de dos variables. Así como la siguiente imagen: 

![[Captura de pantalla 2024-12-27 a la(s) 2.10.16 p.m..png]]

La primera hipótesis es esta: Existe una familia de $\beta{s}$ tal que $$y = \beta_1 x_1 + \dots + \beta_d x_d$$
¿Cuándo un fenómeno no es lineal? (Ejemplo de las casas y su antigüedad)

Por ejemplo, si yo tengo una variable X y una variable Y y encuentro que la correlación entre ellas es -0.8. Es decir, $Corr(X,Y) \leq 0$. Un fenómeno de las regresiones lineales es que es posible que al realizar una regresión es que esta correlación cambie de signo. 
## Hipótesis estadísticas

No solamente existe una regresión lineal entre las variables ($\hat{Y} = \beta X$), sino que la diferencia entre estas dos $\epsilon = Y - \hat{Y}$, donde $Y = \beta X + \epsilon$  debe seguir una campana de Gauss con media 0 ($N(0,\sigma^2$)). 

![[Captura de pantalla 2024-12-27 a la(s) 3.41.41 p.m..png]]

La única manera de verificar esta hipótesis es hacer una regresión lineal y verificar el histograma de los errores. 

Una manera en la que no se cumple los errores es verificar el _skewness_. Es decir, que tan _cargada_ está el histograma del error, esto puede ser a la izquierda y la derecha. 

![[Captura de pantalla 2024-12-27 a la(s) 3.53.33 p.m..png]]

También vale la pena reflexionar sobre qué significa que nuestro error sea mayor o menor a cero y cuál es nuestro error grave. 

# Valores extremos en el error

La Kurtosis en este caso es muy útil, pues analiza la presencia de valores extremos en alguna distribución. Para el caso de analizar la Kurtosis de la distribución de los errores, esto nos puede ayudar a distinguir si necesitamos una regresión lineal o una regresión robusta. 

En este caso de estudio en particular podemos notar que: 

$$\epsilon \sim Lap(\mu, \sigma^2)$$

Nótese que no estamos hablando de valores extremos en las coordenadas o en el valor objetivo, sino del error. 

# Regresión de Huber

La regresión de Huber hace lo siguiente: El error de un conjunto de parámetros en un registro $x_i$ respecto a la predicción $y_i$ es igual al error cuadrático algunas veces y algunas veces al error absoluto. Nótese que esto se puede hacer solamente si no lo hacemos para todos los registros. Este parámetro se conoce como $\delta$. Es decir: 


$$
    Error(\beta;y_i, \hat{y_i}) = \begin{cases}
        (y_i - \hat{y_i})^2, & \text{si } |y_i-\hat{y_i}|\leq \delta\\
        |y_i-\hat{y_i}|, & \text{si } |y_i-\hat{y_i}|>\delta
        \end{cases}
$$
Este _hiperparametro_ es interpretable y se puede calibrar de manera relativamente intuitiva, en particular, para calcular el valor de las casas, como las variables de respuesta $y$ tiene como unidades MDP ($) y nos podemos preguntar ¿cuántos millones de pesos (de error) consideramos como un valor extremo? 

Este $\delta$ lo bajaríamos si la kurtosis sube.

La clase siguiente la seguiremos en este [colab](https://colab.research.google.com/gist/OliverRiemann/b7f523a2f3a586ca5779a88727b076e6/1_response_time_paris_fire_brigade.ipynb) 






