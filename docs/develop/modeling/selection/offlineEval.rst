Evaluación offline
==================

La evaluación offiline es una estimación que podemos usar para estimar qué tan bien creemos que el algoritmo puede funcionar en la práctica. Es decir, no es una garantía de performance sino una estimación. En particular, podemos utilizarla para estimar que tan seguros estamos de que un determinado modelo es mejor que el otro al tener en cuenta la incertidumbre y los origenes de variabilidad.


Origenes de variabilidad
------------------------
Una buena metodología que determine si dos algorimtos de aprendizaje automático son diferentes o no debe poder estimar el poder predictivo de cada uno de ellos a pesar de los diferentes orígenes de variabilidad que pueden existir.
 
- **Variabilidad en el conjunto de datos de evaluación:** Hace referencia a la variación aleatoria en la selección del conjunto de datos de validación en donde evaluamos nuestros modelos.
- **Variabilidad en el conjunto de datos de entrenamiento:** Hace referencia a la variación aleatoria en la selección del conjunto de datos de entrenamiento con los que entrenamos nuestros modelos. Algoritmos que son especialmente sensibles a este tipo de variabilidad se los suele llamar inestables (Breiman 1994, 1996).
- **Variabilidad interna del algoritmo de aprendizaje:** Por ejemplo, si consideramos algoritmos como las redes neuronales, numerosos parámetros, como ser los pesos con los que se inicializa la red, son determinantes para asegurar la correcta convergencia del modelo. Estos parámetros a menudo son inicializados con determinadas distribuciones probabilísticas. 
- **Variabilidad por el error inherente de clasificación:** Hace referencia a la probabilidad de que las etiquetas que tenemos disponibles en nuestros conjuntos de datos no sean efectivamente correctas. Por lo tanto, si nuestros valores verdaderos tienen una probabilidad de error `e`, entonces ningún algoritmo de aprendizaje automático podrá tener una performance mejor que `e`.

Para asegurarnos que nuestras comparaciones son confiables, una prueba estadística debe ser realizada que tenga en cuenta todos estos origenes de variaciones. 

Técnicas
--------

Pruebas de diferencia o de no-inferioridad [1]_ [2]_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Tradicionalmente, las métricas son comparadas utilizando una prueba de hipótesis de diferencia (inequidad) o no-inferioridad. En una prueba de hipótesis de diferencia intentamos probar que existe una diferencia estadísticamente significativa entre las métricas. En una prueba de no-inferioridad, intentamos probar que un modelo de aprendizaje nuevo no es peor que el anterior.

.. note:: Las pruebas de hipótesis de equidad o no-superioridad, aunque configuraciones válidas, no resultarán útiles en nuestro caso dado al `principio de refutabilidad <https://es.wikipedia.org/wiki/Falsabilidad>`_.

En los problemas de clasificación, en general trabajamos con métricas que resultan ser proporciones, como ser `accuracy` y `precision`. En estos casos las pruebas de hipótesis que realizamos son pruebas de diferencias entre proporciones donde tratamos de inferir las proporciones de toda la población P\ :sub:`0` y P\ :sub:`1`, a partir de las proporciones de las muestras que obtuvimos, p\ :sub:`0` y p\ :sub:`1`.

En una prueba de diferencia de proporciones se evaluan dos hipótesis: la hipótesis nula H\ :sub:`0` que establece que no existe diferencia entre las dos métricas de `accuracy` (P\ :sub:`1` - P\ :sub:`0` = 0), y una hipótesis alternativa H\ :sub:`1`  que establece que las métricas de `accuracy` son distintas (P\ :sub:`1` - P\ :sub:`0` > 0). Una prueba direccional (one tail) es a menudo útil para establecer la dirección de la diferencia. Por el principio de refutabilidad, nos interesa el caso en donde H\ :sub:`0` es rechazada en favor de H\ :sub:`1`, indicando que el modelo que estamos evaluando efectivamente ofrece una mejora con respecto al anterior.

En general, ejecutaremos esta prueba con un nivel de significancia del 95% (1-α = probabilidad de correctamente aceptar la hipótesis nulas - verdadero negativo) y un poder estádistico (1-β = probabilidad de correctamente rechazar la hipótesis nula o un verdadero positivo) de un 80% o más. El poder de un test es importante ya que experimentos con un poder bajo nos llevarán a conclusiones incorrectas sobre los resultados.

El tamaño del efecto se calcula utilizando alguna medida estadística especifica como podría ser la correlación de Pearson para relación entre variables o la distancia de Cohen para la diferencia entre grupos. El tamaño del efecto al comparar dos grupos de datos puede ser cuantificado utilizando la medida de Cohen's d. Esta medida calcula un coeficiente estandar que describe la diferencia en termino del número de desviaciones estandars en que las médias son diferentes. Un valor que generalmente se utiliza es 0.8 o un valor superior, lo cual ya es un tamañao de efecto bastante grande.


Prueba de McNemar
^^^^^^^^^^^^^^^^^

La prueba de McNemar es especialmente útil cuando no podemos acceder a entrenar el mismo modelo múltiples veces debido a las restricciones de computo. Los modelos de aprendizaje profundo en general suelen tener estas características. **El objetivo de la prueba es determinar si dos modelos cometen el mismo tipo de errores o no**. Esto es importante porque no hace ninguna suposición de que cual de los modelos es mejor que el otro. Esto deberemos identificarlo de otra manera. Sin embargo, este test nos sirve para saber si vale la pena o no volver a implementar un modelo en producción por ejemplo.

La prueba de McNemar se base en una matrix de contingencia de 2x2 donde en las filas tenemos las diferentes instancias de datos, y en las columnas tenemos un idicador mencionando si el modelo realizó una predicción correcta o no:

+-----------+------------+------------+
| Instancia | Modelo A   | Modelo B   |
+===========+============+============+
| 1         | Correcto   | Correcto   |
+-----------+------------+------------+
| 2         | Incorrecto | Correcto   |
+-----------+------------+------------+
| (...)     | Incorrecto | Incorrecto |
+-----------+------------+------------+
| 4         | Correcto   | Correcto   |
+-----------+------------+------------+

En base a esta tabla, el valor estádistico de McNemar se calcula, para dos modelos A y B:

.. math::
    
    statistic = \frac{ {( C _ {A,B} - C _ {B,A})}^2 }{ (C _ {A,B} + C _ {B,A}) }

Donde :math:`C _ {i,j}` es la cantidad de instancias que el modelo *i* clasificó correctamente y el modelo *j* incorrectamente. Este valor estadístico tiene una distribución de Chi con 1 grado de libertad. En la librería `statmodels` disponemos de la implementación del mismo:

.. code::

    from statsmodels.stats.contingency_tables import mcnemar
    
    result = mcnemar(table, exact=True)
    print('Estadistico=%.3f, p-value=%.3f' % (result.statistic, result.pvalue))

Utilizando el `p-value` que se retorna, con un nivel de confidencia del 95% por ejemplo, podemos rechazar la idea de que los modelos cometen los mismos errores (son distintos) si el valor es menor a 0.05. De lo contrario no podremos derivar ninguna conjetura.

Ejemplos
~~~~~~~~

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/mcnemar.ipynb


5×2 Cross-Validation
^^^^^^^^^^^^^^^^^^^^
Como el nombre sugiere, este método ejecuta 5 veces 2-fold cross validation para cada uno de los modelos a comparar. Las diferencias en las predicciones son luego utilizadas para computar un valor estadístico de la siguiente forma:

.. math::

    t = \frac{{p _ 1}^{(1)}}{\sqrt{\frac{1}{5}\sum_{i=1}^{5}s_i^2}}

Donde:

- :math:`{p_1}^{(1)}` es la diferencia en la performance de los modelos para la primera partición en la primera iteración.
- :math:`s_i^2` es la varianza estimada de la diferencia en la performance de la iteración numero *i*. Esta varianza se puede computar como :math:`({p _ i}^{(1)} - {p _ i})^2 + ({p_i}^{(2)}-{p_i})^2`
- :math:`{p_i}^{(j)}` es la diferencia en la performance de los modelos para la partición j en la iteración i.
- :math:`p_i = \frac{p_i^1+p_i^2}{2}`

Lo importante de este método es que, bajo la hipótesis nula (la cual indica que los dos modelos son estadísticamente similares), la diferencia de la performance debería seguir una distribución normal. Con esta suposición, el valor estadístico debería seguir una distribución *t* con 5 grados de libertad.

Ejemplos
~~~~~~~~

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/5x2.ipynb


.. [1] Approximate Statistical Tests for Comparing. Supervised Classification Learning Algorithms. Thomas G. Dietterich tgd@cs . orst . edu.
.. [2] Liu, Hsueh, Hsieh and Chen (2002)