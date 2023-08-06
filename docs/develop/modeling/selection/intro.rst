====================
Selección del modelo
====================

Una vez que disponemos de un modelo entrenado, es importante poder evaluarlo en el contexto en el que finalmente será utilizado y, sobre todo, compararlo con otros modelos existentes o con el estado actual del proceso de negocio donde esperamos utilizarlo. Esto nos dará una idea de si es una buena idea seleccionar este modelo e implementarlo dentro del proceso de negocio en cuestión.

En general entonces, el proceso de selección puede divirse en dos subprocesos:

:Evaluación del modelo: Se trata del proceso en el cual evaluamos la performance del modelo utilizando diferentes técnicas, tanto quantitativas como qualitativas.
:Selección del modelo: Se trata del proceso en el cual, tomando las métricas de evaluación collectadas anteriormente, tomamos una decisión sobre cual es el mejor modelo con el que desearemos continuar.

Métrica de evaluación
---------------------

Al momento de evaluat y seleccionar un modelo es importante determinar la(s) métrica(s) con la(s) cual(es) compararemos los mismos. Cada métrica puede capturar distintas cualidades del modelo y por ende estas cualidades terminaran impactando la performance del proceso de negocio en cuestión. Por ejemplo, la métrica `accuracy` podría ser una mala elección en un problema de detección de anomalías. Desafortunadamente, no existe una métrica de oro que podamos utilizar siempre. Por lo tanto, es importante definir la métrica (o las métricas) teniendo en cuenta el problema a resolver, prestando especial atención a las consecuencias de su elección.

Podemos, sin embargo, distinguir 3 grandes grupos de métricas:

Clasificación
^^^^^^^^^^^^^

Diferentes métricas de performance responden a diferentes tipos de modelos y suposiciones sobre lo que se busca optimizar. Las métricas de clasificación más comunes son:

.. csv-table:: Métricas de clasificación
   :header: "Métrica", "Descripción"
   :widths: 20, 80

   "Accuracy", "Mide la frecuencia con la que el clasificador hace la predicción correcta. Es la relación entre el número de verdaderos positivos y el número total de predicciones."
   "Per-Class Accuracy", "En general, cuando hay diferentes números de muestras por clase, el accuracy promedio por clase será diferente del accuracy."
   "Log-loss", "Está íntimamente ligada a la teoría de la información: es la información mutua entre la distribución de los valores verdaderos y las predicciones."
   "AUC-ROC", "La curva ROC muestra la sensibilidad del clasificador graficando la tasa de verdaderos positivos contra la de falsos positivos. Muestra cuántas clasificaciones positivas correctas se pueden obtener a medida que permite más y más falsos positivos."
   "Precision", "Responde a la pregunta: 'De todos los elementos que se predicen como relevantes, ¿cuántos son realmente relevantes?' (verdadero positivos dividido todo lo clasificado como positivo - verdaderos positivos y falsos positivos)"
   "Recall", "Responde la pregunta: 'De todos los elementos que son verdaderamente relevantes, ¿cuántos son predichos por mi clasificador?' (verdaderos positivos dividido todo lo que es positivo - verdaderos positivos y falsos negativos)."
   "AUC-PR", "El área bajo la curva PR (AU-PR) es útil cuando los verdaderos negativos son mucho más comunes que los verdaderos positivos (es decir, TN »TP). Solo se centra en las predicciones en torno a la clase positiva (que se estima que es la de interés)."
   "F1-Score", "Computa la media harmónica entre Precision y Recall. A diferencia de la media aritmética, la media armónica se inclina hacia el menor de los dos elementos. Por lo tanto, la F1 será pequeño si alguno de los dos valores es pequeño. Sin embargo, Precision y Recall tratan todos los elementos por igual. No hay elementos mas relevantes que los otros."
   "Matthews Correlation Coefficient", "Tiene en cuenta los verdaderos y falsos positivos y negativos y, en general, se considera una métrica “justa” que se puede utilizar incluso si las clases son de tamaños muy diferentes. El MCC es un coeficiente de correlación entre las clasificaciones binarias verdaderas y predichas; devuelve un valor entre -1 y +1."


Regresión
^^^^^^^^^

Diferentes métricas de performance responden a diferentes tipos de modelos y suposiciones sobre lo que se busca optimizar. Las métricas de regresión más comunes son:

.. csv-table:: Métricas de regresión
   :header: "Métrica", "Descripción"
   :widths: 20, 80

   "Variance", "Es la proporción de variación que tiene en cuenta un modelo para el conjunto de datos determinado. Es el porcentaje de reducción de la varianza de los datos originales con respecto a la varianza de los errores. Cuando la media de los errores es 0, es igual que el coeficiente de determinación."
   "R2", "R cuadrado es el coeficiente de determinación o el porcentaje de reducción de los errores cuadráticos en comparación con un modelo que predice la media."
   "Spearman Correlation", "Es una medida no paramétrica de la monotonicidad de la relación entre dos conjuntos de datos. A diferencia de la correlación de Pearson, la correlación de Spearman no asume una relación linear entre las variables. Como sucede con otros coeficientes de correlación, este varía entre -1 y + 1, y 0 implica que no hay ninguna correlación. Las correlaciones de -1 o +1 implican una relación monotónica exacta. Las correlaciones positivas implican que cuando aumenta x, también lo hace y. Las correlaciones negativas implican que cuando aumenta x, y disminuye."
   "Mean Absolute Error (MAE)", "Es el valor esperado del valor absoluto de la diferencia entre el valor verdadero y las predicciones. Si los outliers no son tan comunes es una buena opción debido a su simple interpretación."
   "Root Mean Squared Error (RMSE)", "Se define como la raíz cuadrada de la distancia cuadrática promedio entre los valores reales y los predichos. Dado que los errores estan al cuadrado, RMSE es útil cuando errores grandes deben ser penalizados mas fuertemente. RMSE puede ser la métrica más común, pero tiene algunos problemas. Por ejemplo, es uná métrica que no necesariamente aumenta con un aumento en la varianza del error, sino que lo hace con la varianza de la distribución de las magnitudes de los errores. Más importante aún, debido a que los errores estan al cuadrado, es especialmente sensible a outliers. Finalmente, RMSE tiende a incrementar en magnitud con el tamaño del conjunto de datos, lo cual hace dificultoso compararla en conjuntos de datos de diferentes tamaños."
   "Median Absolute Percentage Error (MAPE)", "Nos da una medida relativa del error típico. Alternativamente, podríamos calcular el percentil 90 del error porcentual absoluto, lo que daría una indicación de un comportamiento 'casi en el peor de los casos'."
   "Root Mean Squared Log Error", "Es la raíz cuadrada del error logarítmico cuadrático. El logaritmo reduce naturalmente el rango dinámico de una variable (en este caso el error), por lo que las diferencias se conservan mientras que la escala no se sesga de manera tan dramática."
   "Normalized Root Mean Squared Log Error", "Es el error logarítmico cuadrático medio dividido por el rango de la variable a predecir."

Sistemas de recomendación
^^^^^^^^^^^^^^^^^^^^^^^^^

Las métricas en los sistemas de recomendación evaluan la capacidad de realizar recomendaciones relevantes para el usuario. En aquellos casos donde el orden de las recomendaciones no es relevante, las siguientes métricas pueden ser utilizadas:

.. csv-table:: Métricas en sistemas de recomendación
   :header: "Métrica", "Descripción"
   :widths: 20, 80

   "Precision@k", "Mide la proporción de items que son relevantes entre los K primeros items recomendados. Responde la pregunta 'de los primeros K elementos recomendados al usuario, cuantos son realmente relevantes."
   "Recall@k", "Recall@k o HitRatio@k es la facción de los primeros K items recomendados que son relevantes entre todos los items relevantes para el usuario. Notar que cuanto mas grande es K, más alta sera la métrica ya que hay mayor probabilidad de recomendar algo que es relevante."
   "F1@k", "F1@k es la média armónica entre Precision@k y Recall@k, lo cual simplifica la evaluación al combinar ambas métricas en una sola. Es interesante ver que F1 no considera los verdaderos negativos en su calculo (los items que el sistema no recomendó porque son irrelevantes)."
   "Matthews correlation coefficient (MCC)", "Es una métrica simétricamente opuesta a F1. Mide la correlación entre lo que se predice y la realidad. Cuando el sistema de recomendación es perfecto, MCC es 1. Cuando el systema predice incorrectamente siempre, MCC = -1."


En algunos casos donde los algoritmos de recomendación retornan una lista rankeada de recomendaciones - y sobre todo considerando aquellos casos donde items mas cercanos al final de la lista tienen menos probabilidades ser ser notados por el usuario - las siguientes métricas pueden ser utilizadas:

.. csv-table:: Métricas en sistemas de recomendación (ranking)
   :header: "Métrica", "Descripción"
   :widths: 20, 80

   "Average precision (AP@k)", "Mientras precision@k (P(k)) considera solo el subconjunto de las primeras *k* recomendaciones, *average precision* premia el ubicar recomendaciones correctas sobre el principio de la lista. Es el promedio de todas las precision@k para k [1..k]"
   "Mean average precision (MAP)", "Mientras *AP* puede computarse sobre un usuario dado, *MAP* computa el promedio sobre todos los usuarios del sistema."
   "Mean reciprocal rank (MRR)", "Es una métrica relevante en aquellos sistemas donde a) existe solo un elemento relevante para recomendar, y b) solo el primer item recomendado por el sistema es utilizado. "
   "Discounted cumulative gain (DCG)", "Es una métrica de calidad de rankeo. Utiliza el concepto de *ganancia acumulativa*, la cual es la suma de los valores de relevancia de todos los resultados de la lista. Finalmente, DCG penaliza los items de gran relevancia que aparecen más abajo en la lista de recomendaciones al reducir el valor de su relevancia de forma logarítmicamente proporcional a la posición del item."


Comparando multiples modelos
----------------------------

Estimar una métrica para un modelo particular puede realizarse utilizando las típicas técnicas de separación de :ref:`rst_training_datasets`. Sin embargo, comparar multiples modelos puede resultar un poco más complejo en la práctica que simplemente comparar la misma métrica sobre el conjunto de datos de validación. En muchos casos, necesitamos estimar que tan seguros estamos de que la métrica efectivamente tiene ese valor, es deci, estimar la incertidumbre. Revisaremos varios ejemplos en :doc:`offlineEval`


.. toctree::
    :maxdepth: 1
    :caption: En esta sección
    :hidden:

    Evaluación offline <offlineEval>
    Análisis de errores <error-analysis>
