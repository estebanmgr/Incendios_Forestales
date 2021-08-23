# Incendios_Forestales
Para este utilicé la base de datos de incendios forestales en la zona de Algeria con el fin de preecir la posibilidad de ocurrencia un incendio y así poder ayudar a los recursos destinados para combatirlos y poder disminuir su devastadoras consecuencias, para esto:
* Limpié y analicé los datos para asegurarme que existiera una homogeneidad en los mismos y que no tuviesemos valores faltantes que tratar así poder entrenar correctamente los distintos modelos de clasificación.
* Utiliar y entrenar distintos modelos de clasificación (Regresión logistica, Nearest neighbors, Suport vector machine (Linear, rbf, sigmoide y poly), Naive bayes, Arbol de decisiones y Random forest) para luego poder contrastar los resultados con una parte de los datos que no han sido utilizarlos y así medir su precisión.

## Recursos y códiigo utilizado 
**Versión de Python:** 3.7  
**Paquetes:** pandas, numpy, sklearn, matplotlib, seaborn   
**Artículo del dataset utilizado:** Datos obtenidos de la página web: https://archive.ics.uci.edu/ml/datasets/Algerian+Forest+Fires+Dataset++

Faroudja ABID et al. , â€œPredicting Forest Fire in Algeria using Data Mining Techniques: Case Study of the Decision Tree Algorithmâ€, International Conference on Advanced Intelligent Systems for Sustainable Development (AI2SD 2019) , 08 - 11 July , 2019, Marrakech, Morocco

# Explicación de datos utilizados
El dataset consta de 122 filas y 14 columnas (o variables):

Day: día del mes que se tomó la muestra de datos  
Month: Mes del año en el que se tomaron las muestras   
Year: Año en el que se tomaron los datos   
Temperature: Temperatura registrada (Medida en grados C)   
RH: Humedad relativa registrada   
WS: Velocidad del viento   
Rain: Ocurrencia de lluvia en la zona   
FFMC: Codigo de humedad del combustible fino muerto   
DMC: Humedad del mantillo   
DC: Indice de sequía   
ISI: Evalúa el riesgo de propagación de un incendio forestal y su peligrosidad   
BUI: Cantidad de combustible disponible para que arder.   
FWI: Riesgo en caso de ocurrencia de un incendio forestal (vá del 0 al 100)   
Classes: Ocurrencia o no de un incendio.

## Limpiando el Dataset
Despues de importar el dataset fue necesario limpiarlo para que el modelo pueda entrenarse mejor y que no se encuentren valores desvirtuados, valores faltantes y exista homogeneidad en las columnas y filas. Hice los siguientes cambios en las variables y en los datos:

*	Dividí todo el dataset en dos partes ya que el archivo contenía información de los incendios forestales de Abbes y de Algeria (cada uno con 122 filas) y luego de hacer esto encontraos que en el dataset de Algeria no se encontraron valores faltantes ni valores erroneos sin embargo en el apartado de Abbes su se encontraron más problemas con lo cual hicimos lo siguiente:
  1. Se cambiaron los nombres de las columnas de ambos datasets para unificarlos (Actualmente existían nombres de columnas con espacios incluidos)
  2.  Existían tambien distintos nombres en la columna de Classes con lo cual se procedió a unificar los nombres
  3.  Habian 3 columnas con el tipo de datos incorrectos, con lo cual se cambió dicho formato para que sea el correcto (de object a float e int según el caso)
  4.  Se rellenaron algunos pocos valores faltantes con el pomedio de la columna del dataset de Algeria (eran muy pocos los valores faltantes)
  5.  Se eliminan las columnas de "Día" y de "Año" ya que aportan poca información relevante al estudio
  6.  Se separan las variables en dependientes e independientes para hacer el análisis completo

## Aálisis exploratorio de los datos (EDA)
Analicé la distribución de los datos, la correlación entre ellos y las estadisticas descriptivas de las variables numericas. A continuación podeis ver algunas de los gráficos obtenidos. 

![alt text](https://github.com/estebanmgr/Incendios_Forestales/blob/main/Im%C3%A1genes%20Algeria/Incendios%20en%20meses.png "Incendios en meses")
![alt text](https://github.com/estebanmgr/Incendios_Forestales/blob/main/Im%C3%A1genes%20Algeria/FFMC%20vs%20Incendios.png "FFMC vs Incendios")
![alt text](https://github.com/estebanmgr/Incendios_Forestales/blob/main/Im%C3%A1genes%20Algeria/Lluvia.png "Lluvia")
![alt text](https://github.com/estebanmgr/Incendios_Forestales/blob/main/Im%C3%A1genes%20Algeria/Temperatura%20vs%20incendios.png "Temperatura vs Incendios")
![alt text](https://github.com/estebanmgr/Incendios_Forestales/blob/main/Im%C3%A1genes%20Algeria/Temperaturas%20en%20meses.png "Temperatura en meses")


## Creando el modelo 

Primero transformé las variables categóricas (variables resultado) en dos categorías, 0 y 1 (no incendio o incendio), también realice una división del dataset en conjunto de entrenamiento y evaluación con un tamaño de muestra de evaluación de un 30% ya que el tamaño de las muestras no era lo suficientemente amplio.   

Prové con varios modelos y evalue los resultados utilizando el accuracy en cada uno para luego elaborar la martiz de confusión como segundo método de evaluación.   

Prové los siguientes modelos:
*	**Regresión logistica** 
*	**Nearest neighbors** 
*	**Support Vector Machine** – Dentro de este modelo prové con los kernels "linear", "sigmoide", "rbf" y "poly". 
*	**Naive bayes** 
*	**Arbol de decisiones**
*	**Random forest**  

## Resultados de los modelos.
El modelo de Random Forest, Arbol de Decisión y Regresión Logística fueron los que mejores resultador arrojaron en comparación con los otros modelos tanto en el conjunto de entrenamiento como en el conjunto de evaluación, a mayores de esto dicho modelo se probó con los datos de Abbes (datos que no se había untlizado anteriormente) obteniendo los siuientes resultados de precisión

*	**Regresión logistica** : Accuracy = 93.44%
*	**Nearest neighbors** : Accuracy = 86.88%
*	**Support Vector Machine linear** : Accuracy = 90.98%
*	**Support Vector Machine sigmoide** : Accuracy = 77.05%
*	**Support Vector Machine rbf** : Accuracy = 86.88%
*	**Support Vector Machine poly** : Accuracy = 87.70%
*	**Naive bayes** : Accuracy = 91.80%
*	**Arbol de decisiones** : Accuracy = 95.90%
*	**Random forest**  : Accuracy = 96.72%

## Area de mejora a futuro
* Es necesaro aumentar el tamaño de la muestra ya que 122 observaciones son muy pocas para entrenar un modelo.
* Sería bueno elaborar una API mediante flask en el que se puedan ingresar los datos de las variables y te arroje en tiempo real si hay posibilidad de que ocurra un incendio o no, de esta manera se pueden destinar mejor los equipos de bomberos y guardias forestales para minimizar los daños ocasionados.
