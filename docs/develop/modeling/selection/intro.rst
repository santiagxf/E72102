====================
Selección del modelo
====================

Una vez que disponemos de un modelo entrenado, es importante poder evaluarlo en el contexto en el que finalmente será utilizado y, sobre todo, compararlo con otros modelos existentes o con el estado actual del proceso de negocio donde esperamos utilizarlo. Esto nos dará una idea de si es una buena idea seleccionar este modelo e implementarlo dentro del proceso de negocio en cuestión.

Métrica de comparación
----------------------

Al momento de seleccionar un modelo es importante determinar la métrica con la cual los vamos a comparar. Diferentes métricas nos pueden apuntar en direcciones distintas. Por ejemplo, la métrica `accuracy` podría ser una mala elección en un problema de detección de anomalías. Desafortunadamente, no existe una métrica de oro que podamos utilizar siempre por lo cual es importante definir la métrica teniendo en cuenta el problema a resolver. 

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
   "F1-Score", "Compita la media harmónica entre Precision y Recall. A diferencia de la media aritmética, la media armónica se inclina hacia el menor de los dos elementos. Por lo tanto, la F1 será pequeño si alguno de los dos valores es pequeño. Sin embargo, Precision y Recall tratan todos los elementos por igual. No hay elementos mas relevantes que los otros."
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
   "Mean Absolute Error (MAE)", "Es el valor esperado del valor absoluto de la diferencia entre el valor verdadero y las predicciones. Si los outliers no son tan comunes es una buena opción. "
   "Root Mean Squared Error (RMSE)", "Se define como la raíz cuadrada de la distancia cuadrática promedio entre los valores reales y los predichos. RMSE puede ser la métrica más común, pero tiene algunos problemas. Más importante aún, debido a que es un promedio, es sensible a outliers."
   "Median Absolute Percentage Error (MAPE)", "Nos da una medida relativa del error típico. Alternativamente, podríamos calcular el percentil 90 del error porcentual absoluto, lo que daría una indicación de un comportamiento 'casi en el peor de los casos'."
   "Root Mean Squared Log Error", "Es la raíz cuadrada del error logarítmico cuadrático."
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


.. _rst_error_analysis:

Análisis de errores
-------------------

Más allá del valor de la métrica específica, es importante entender cómo nuestro modelo se comporta. La práctica de análisis de errores trata de identificar cómo nuestro modelo comete los errores y cómo se distribuyen esos errores dentro del conjunto de datos y, en particular, en algunos subconjuntos con determinados atributos. En muchos casos es importante diseñar *pruebas* que dividan el conjunto de datos en subpoblaciones o *slices* basandose en atributos protegidos (los cuales prodrían o no ser predictores utilizados por el modelo). Esta técnica también suele utilizarse para asegurar que nuestro modelo sea justo (*fairness*), un procedimiento mandatorio para cualquier modelo que utilize datos de personas ya que podría haber requerimientos de negocio, regulatorios o legales que penalizen a la organización por no realizarlo. Por ejemplo, podríamos preguntarnos "¿Cúal es la performance de nuestro modelo de reconocimiento de voz cuando el interlocutor tiene un acento determinado?".

Hacer este tipo de preguntas llevan a nuestro análisis de performance mucho más lejos que cuando miramos simplemente una métrica en particular como la presición o el coeficiente de determinación. 

Tomarse el tiempo para entender cómo y por qué nuestro modelo comete errores tiene numerosos beneficios incluyendo:
 - Puede ayudarnos a identificar zonas donde no tenemos suficiente cantidad de datos. Por ejemplo, si nuestro modelo comete muchos errores clasificando frutas pero no clasificando animales, entonces podríamos querer aumentar el conjunto de datos con más imágenes de frutas.
 - Si sabemos que nuestro modelo tiene especiales complicaciones manejando determinado tipo de casos, podríamos decidir imponer algunas restricciones en su uso para prevenir fallas más gráves en los procesos de negocio que lo utilizan. Vea :doc:`../../ops/validation/riskmodel`. 
 - Puede ayudarnos a identificar problemas fundamentales en nuestro modelo que nos hagan replantearnos si el modelo debería llegar a producción. Por ejemplo, si nuestro modelo comete determinados errores con determinado género de las personas, quizás deberíamos evaluar no utilizarlo.

Ejemplos
^^^^^^^^

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/error_analysis.ipynb
  code/what_if.ipynb
  code/model_analysis.ipynb
  code/fairlearn.ipynb


Comparando multiples modelos
----------------------------

Estimar una métrica para un modelo particular puede realizarse utilizando las típicas técnicas de separación de :ref:`rst_training_datasets`. Sin embargo, comparar multiples modelos puede resultar un poco más complejo en la práctica que simplemente comparar la misma métrica sobre el conjunto de datos de validación. En muchos casos, necesitamos estimar que tan seguros estamos de que la métrica efectivamente tiene ese valor, es deci, estimar la incertidumbre. Revisaremos varios ejemplos en :doc:`offlineEval`


.. toctree::
    :maxdepth: 1
    :caption: En esta sección
    :hidden:
 
    Evaluación offline <offlineEval>