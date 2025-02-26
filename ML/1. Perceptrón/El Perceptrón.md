
El caso de uso es la clasificación de tejidos cancerígenos. 

En este caso vamos a trabajar un modelo de clasificación binario.

Errores graves: En el caso del tejido se refiere a los falsos negativos, es decir, que prediga que no es cancer cuando sí lo es. 

Los falsos positivos es que diga que tiene cancer cuando no lo tiene. 
## Sutilezas

- Bases de datos: 
	- Base de datos supervisada: [Se define por su uso de conjuntos de datos etiquetados para entrenar algoritmos que clasifiquen datos o predigan resultados con precisión.](https://www.ibm.com/mx-es/topics/supervised-learning)
	- Una base de datos supervisada [es una base de datos en donde no solamente tenemos nuestros registros además de lo que queremos predecir ](https://www.youtube.com/watch?v=g8gQHaI0fQ4&ab_channel=AdminEscuela)$$(x, y)$$
- Imágenes inestables
	- No es un problema que se puede resolver con técnicas de reconocimiento de imágenes clásicas; como es el caso con la huella digital, el reconocimiento facial, pues la imágen pueden estar rotadas, es decir, tenemos poco control con lo que hace la cámara. 
	- Intentamos que el algoritmo reconozca los patrones
- Errores del segundo tipo
	- Necesitamos mitigar los errores graves, lo que representa un problema dificil de tratar.

## Altamente costoso

Las bases de datos etiquetadas son costosas. En tiempo, esfuerzo y dinero. 

El ejemplo que menciona el profesor es una base de datos de los registros sean préstamos y la etiqueta sea si se pagó o no el préstamo. Notese que si no se hizo el pago del préstamo este representa una pérdida del dinero registrado, por lo cual dicha base de datos sería costosísima.

Continuamos en el siguiente 