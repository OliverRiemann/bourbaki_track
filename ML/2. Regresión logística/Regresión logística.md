El caso de estudio de este modelo son las reseñas de un hotel y nuestro objetivo es determinar si la reseña es falsa o verdadera. 

## Datos no estructurados

Normalmente nos referimos a datos no estructurados cuando hablamos de imágenes, textos, etc. pues no es claro quiénes son nuestras features.

¿Cuál es la diferencia entre entrenar un modelo supervisado a simplemente contar las palabras _negativas_ y _positivas_? La diferencia fundamental, es el hecho de que cuando nosotros _elegimos_ estas palabras positivas y negativas estamos introduciendo un sesgo.  
## Clasificación de textos (automatización)


## Procesamiento del lenguaje natural

En este curso aprenderemos modelos supervisados, modelos no supervisados y modelos autosupervisado. 

Tres tipos de procesamiento del lenguaje natural.

Son muy comunes las bases de datos de textos, por eso son una herramienta muy poderosa para el análisis de datos

Matriz dispersa: Este es un tipo de bases de datos que es dispersa o sparce cuando dado un registro la mayor parte de ella son ceros. 
### Dos etapas

### Etapa 0

Cómo quitarle algunas características que no son representativas.

Etapa dos modelo logístico, predicción. Máxima verosimilitud. 

## Modelo logístico


Dudas: Semana 2, ¿estoy interpretando bien el gain? 

7min: Ganancia

9min: Entropía

# Matriz dispersa

Una matriz donde la mayoría de sus entradas son 0.

Tenemos que mover el umbral de probabilidad para el random forest

Cómo se interpreta la regresión logística. Podemos calcular el momio, es decir, qué tanto le afecta a la función sigmoide.

Mientras más datos tenga, más funciona esto. Mientras

Un árbol de decisión funciona muy bien, el problema es que tiende al sobreajuste. Es decir se aprende el ruido. Si queremos reducir el sobreajuste reducimos la profundidad del árbol. La regresión logística siempre toma en cuenta todas las características.

El perceptrón no es interpretable porque utiliza todas las variables al mismo tiempo

## Regresión ridge

Inducimos una restricción respecto a nuestro conjunto de betas. Depende fundamentalmente de un parámetro $\lambda \in [ 0, \infty)$ la restricción hace dos cosas al mismo tiempo

- Minimizar el error $\hat{y_i} \approx y_i$
- Minimizar $||\beta||_2 \leq \frac{1}{\lambda}$ 

Esta segunda característica dice lo siguiente: "El tamaño del vector $\beta$ no sea demasiado grande comparado con el inverso del hiperparámetro lambda"

Hiperparámetro: Un parámetro que nos da un modelo diferente de ridge.

Restringir nuestras $\beta$ significa restringir nuestro hiperplano. Nótese que esto puede aumentar el error en el conjunto de prueba. 

La función de error es continua y casi convexa. 

El error es continuo respecto a la variable $\lambda$,

## GridSearchCV

Es una función que funciona para cualquier modelo, con el objetivo de encontrar un buen hiperparámetro. En el caso de la regresión logística se podría ver así: 

```
from sklearn.model_section import GridSearchCV
grid_search = GridSearchCV(LogisticRegression(penalty='l2',solver="newton-cg", {'C': 1/lambdas}, cv = 5, return_train_score=False))

grid_search.fit(X,y)
```

El parámetro cv se refiere al _cross validation_, es decir, al hacer una cross validation, una buen imagen es la siguiente: 

![[Pasted image 20241128162313.png]]

# Preguntas

¿Cómo se interpreta una regresión logística?


# Hipótesis de una regresión logística

Las variables de X tienen una relación  X independientes



Okay, here's a pipeline for performing logistic regression with ridge regularization to detect fraudsters, along with a review of your Colab code for potential changes:

**Pipeline:**

1. **Data Preparation:**
    - Load your dataset using `pd.read_csv`. You've already done this in your code.
    - Split the data into features (X) and target (y): `y = df['fraud_flag']`, `X = df.drop('fraud_flag', axis=1)`. You've already done this.
    - One-hot encode any categorical features if present. In this case it seems you only have numerical features, so no need for one-hot encoding, you are using bag of words.
    - Split data into training and testing sets using `train_test_split`. You've already done this.
    - **Important:** Scale your features using `StandardScaler`. This is crucial for logistic regression with regularization to ensure features contribute equally. You can do this using:

content_copy 

```
from sklearn.preprocessing import StandardScaler     scaler = StandardScaler()     X_train = scaler.fit_transform(X_train)     X_test = scaler.transform(X_test)
```

[Use code with caution](https://g.co/legal/generative-code)

2. **Model Training:**
    
    - Import `LogisticRegression` from `sklearn.linear_model`. You've already done this.
    - Create a logistic regression model with ridge regularization by setting `penalty='l2'` (or 'ridge' if using sklearn version >= 1.2). You have done this for searching the best parameters.
    - Train the model using `model.fit(X_train, y_train)`. You've already done this. You could include the parameter `class_weight='balanced'` to address the class imbalance in your dataset.
3. **Hyperparameter Tuning (Optional but Recommended):**
    
    - Import `GridSearchCV` from `sklearn.model_selection`. You've already done this.
    - Define a range of values for the regularization parameter `C` (inverse of lambda). You've already done this.
    - Use `GridSearchCV` to find the best `C` value that maximizes performance on a validation set. You've already done this.
    - Retrain the model with the best `C` value. You've already done this.
4. **Model Evaluation:**
    
    - Predict on the test set using `model.predict(X_test)`. You've already done this.
    - Evaluate performance using metrics like accuracy, precision, recall, F1-score, and AUC. Consider using a confusion matrix to visualize the results. You've already done this using the `evaluacion` function.

**Review of your Colab Code:**

- **Scaling:** You have already scaled the data but it's before splitting in train and test, so you are introducing bias in your model. It is suggested to move this step after the split and apply the fit in the training data and only the transform in the test data.
- **Class Weighting:** Consider using `class_weight='balanced'` in your `LogisticRegression` to address the class imbalance. You've already done this in your hyperparameter search.
- **Hyperparameter Tuning:** You've implemented this well using `GridSearchCV`.
- **Evaluation:** You have a good set of evaluation functions and are considering your problem to choose the correct measures.
- **Visualization:** Consider creating visualizations to help understand the model's behavior, like ROC curve and a plot of coefficient magnitudes. You've already created the ROC curve.

I hope this helps! Let me know if you have any other questions.
