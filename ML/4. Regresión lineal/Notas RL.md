## Introducción 

El curso es una invitación al forecasting en presencia de outliers así como
sus aplicaciones, nuestro ejemplo principal es la regresión de Huber sin
embargo hablaremos de algunos otros, el curso está dividido en clases de
la siguiente manera:

1. ¿Qué modelan las regresiones lineales y qué son los valores extremos? (una hora). ([[Grabaciones RL#Introducción]])
3. Limpieza da la base de datos de Bomberos en París (una hora).
4. Descripción formal de las regresiones robustas y de Huber (dos horas).
5. Implementación para la predicción de tiempos de respuesta de los vehículos de emergencia en París (dos horas).
6. Dudas y complementos (dos horas).

## ¿Por qué es difícil el forecast en presencia de outliers?

### Notación 

Fijemos un conjunto finito $\Omega$. Una distribución de probabilidad es una asignación numérica $\mathbb{P}$ a cada elemento $A \subset \Omega$ tal que si $A, B$ son dos subconjuntos: 

1. $0 \leq \mathbb{P}(A) \leq 1 = \mathbb{P}(\Omega)$ 
2. $\mathbb{P}(A^\complement) = 1-\mathbb{P}(A)$
3. $\mathbb{P}(A\cup B) = \mathbb{P}(A) + \mathbb{P}(B)$, si $A \cap B = \emptyset$

A la pareja $(\Omega, \mathbb{P})$ se le llamará un espacio de probabilidad

- _Distribución uniforme_: Supongamos que $\Omega$ es un conjunto de tamaño $m$. Definamos la siguiente ley de probabilidad $$\mathbb{P}_{unif}(\omega_1, \dots, \omega_6) = \frac{i}{m}$$Por ejemplo: Cuando $m=6$ esto corresponde a la probabilidad de obtener algún resultado cuando lanzamos un dado. 
- **Distribución de Bernoulli**:  Supongamos que $\Omega$ es un conjunto de tamaño $2$. Sea $0 \leq p \leq 1$ un número arbitrario. Definimos $\mathbb{P}_{Bernoulli}(\omega_1) = 1-p$ y $\mathbb{P}_{Bernoulli} = p$. Para fijar notación supongamos que tenemos una moneda cargada tal que cada 10 lanzamientos, 8 son sol, en este caso $p = \frac{2}{10}$ 

## De la regla de 3 a regresión lineal^hipotesis

^567d48


En esta sección hablaremos del modelo matemático más simple que es el
modelo lineal, dos ejemplos importantes de estos modelos son las reglas
de tres y las regresiones lineales.

#### La regla de tres directa

La regla de tres es el modelo matemático más simple para explicar un fenómeno, las regresiones lineales son una generalización de esta explicación.

Ejemplo: 

Si 3 kilos de fruta cuestan 70 pesos,

- ¿cuánto cuestan 8 kilos de fruta?
- ¿cuánto cuestan 2 kilos de fruta?

Nótese que podemos representar esta pregunta como una tabla de la forma siguiente 

| Kilos | Precio |
| ----- | ------ |
| 3     | 70     |
| 8     |        |
| 2     |        |

O como una relación lineal: $$y = \frac{70}{3}x$$ donde x es la cantidad de kilos 

![[Pasted image 20241205131406.png]]
Lo primero que debemos notar es que el problema es tal que si la cantidad de kilos de fruta crece, el precio también. De igual manera si la cantidad de kilos disminuye, también lo hará el precio.
Esta observación es muy importante para saber si debemos de utilizar una
regla de tres directa o no.

Notemos que hemos construido el primer ejemplo de un modelo matemático, es decir nuestra función que a $x$ kilos de fruta le asigna la cantidad $\frac{70}{3}x$ pesos. 

Un ejemplo donde no se utiliza la regla de tres directa es el siguiente: 

Si 2 trabajadores terminan un trabajo en 8 horas 

- ¿cuánto se tardarían 5 trabajadores?
- ¿cuánto se tardaría 1 trabajador?

La tabla se vería de la siguiente manera: 


| Trabajadores | Tiempo |
| ------------ | ------ |
| 2            | 8      |
| 5            |        |
| 1            | 16     |

En este caso la relación lineal se vería de esta manera: $$y = \frac{16}{x}$$
#### La regla de tres directa con sesgo

Ahora generalizaremos las reglas de tres a modelos más complejos, geométricamente consideramos rectas que no precisamente atraviesan el origen del plano cartesiano. 

**Ejemplo**: Si solo por subir a un taxi (banderazo) se cobran 50 pesos y por recorrer 6 kilómetros nos cobran en total 122 pesos. 

- Cuánto costará un trayecto de 10 kilómetros en taxi?
- ¿Cuánto costará un trayecto de 2 kilómetros en taxi?

_(Solución explicada)_ Nuevamente estamos en un problema
tal que si la cantidad de kilómetros aumenta, también lo hará el costo, sin embargo esta vez es necesario hacer una pequeña modificación antes de usar la regla de tres directa.
A la cantidad de 122 pesos es necesario restarle los 50 pesos que cobran solo
por subirnos al taxi, es decir que por los 6 kilómetros recorridos pagamos 72
pesos.

Esto se puede expresar por medio de la siguiente ecuación donde $y$ representa el costo total y $x$ la cantidad de kilómetros recorridos: $$y = \frac{72}{2}x + 50$$
#### Un ejemplo sencillo multi-dimensional

Regresando a los ejercicios del primer día de clases, hasta el momento
hemos hablando sobre las reglas de tres utilizado el plano cartesiano sin
embargo es posible trabajar en dimensiones más grandes como lo muestra
el siguiente ejemplo:

**Ejemplo**: 

Si por subir a un taxi nos cobran 50 pesos, por recorrer cada kilómetro nos cobran 12 pesos y por cada diez minutos de trayecto nos cobran 2 pesos, escribir la ecuación que define el precio de un trayecto donde $y$ será el costo, $x$ será la cantidad de kilómetros y $z$ la cantidad de minutos del trayecto.

La ecuación que define el precio puede ser expresada mediante la siguiente ecuación: $$y = 12x+\frac{2}{10}z+50$$![[Captura de pantalla 2024-12-05 a la(s) 1.30.58 p.m..png]]

Como se puede ver en el ejemplo anterior, entre más elaborados resulten los problemas será necesario agrandar la dimensión de nuestras representaciones gráficas, vale la pena notar que eventualmente será imposible dibujarlas pues solo podemos dibujar objetos que viven en tres dimensiones.

#### Las distribuciones gaussianas

Diremos que una variable $S = \{\epsilon_1,\epsilon_2,...,\epsilon_N \}$ satisface una distribución gaussiana cuando su tabla de frecuencias dibuja una campana de Gauss.

Definition 03.2. La ley de probabilidad Gaussiana o normal con parámetros $(\mu, \sigma^2)$ se define para los intervalos $(-\infty, x]$  de la siguiente manera:

$$\mathbb{P}_{Gauss,\mu,\sigma^2}(-\infty, x) = \frac{1}{\sigma \sqrt{2\pi}}\int_{-\infty}^{x}\left(exp\left(\frac{(t-\mu)^2}{2\sigma^2}\right)\right)dt$$

Una distribución que utilizaremos esta lección es la siguiente: 

Definition 03.3. La ley de probabilidad Gaussiana o normal con parámetros $(\mu, 2b^2)$ se define para los intervalos $(-\infty, x]$  de la siguiente manera:

$$\mathbb{P}_{Laplace,\mu,\sigma^2}(-\infty, x) = \frac{1}{2b}\int_{-\infty}^{x}e^{-\frac{|t-\mu|}{b}}dt$$
Recordemos que en este curso estamos utilizando indistintamente la noción de variable aleatoria y de conjunto de observaciones S. Hasta el momento hemos utilizado los dos momentos principales de una variable aleatoria, a saber su valor esperado y su varianza. En esta sección hablaremos de otro momento asociado a una variable aleatoria que nos permite medir el tamaño de las colas en una distribución, es decir nos permite medir qué tan probables son los eventos alejados del promedio que exceden la desviación estándar.

Definición 03.4 Sea $S = \{x_1, x_2, \dots, x_{N}\}$, definimos la kurtosis de S como: $$\kappa_S = \frac{\frac{1}{N}\sum_{i\leq{N}}(x_i - \mu_S)^4}{\left(\frac{1}{N}\sum_{i\leq{N}}(x_i - \mu_S)^2\right)^2}-3 $$
Example 03.5 

1. La kurtosis de una distribución gaussiana centrada en cero y con varianza uno es igual a cero
2. La kurtosis de una distribución de Laplace centrada en cero con varianza uno es igual a tres.
# Regresiones

Esta parte de las notas incluye los detalles técnicos y las definiciones principales tanto de las regresiones clásicas como de las regresiones robustas.

