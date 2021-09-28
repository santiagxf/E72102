Evaluación offline
==================

Origenes de variabilidad
------------------------
Una buena metodología que determine si dos algorimtos de aprendizaje automático son diferentes o no debe poder estimar el poder predictivo de cada uno de ellos a pesar de los diferentes orígenes de variabilidad que pueden existir.
 
- **Variabilidad en el conjunto de datos de evaluación:** Hace referencia a la variación aleatoria en la selección del conjunto de datos de validación en donde evaluamos nuestros modelos.
- **Variabilidad en el conjunto de datos de entrenamiento:** Hace referencia a la variación aleatoria en la selección del conjnuto de datos de entrenamiento con los que entrenamos nuestros modelos. Algoritmos que son especialmente sencibles a este tipo de variabilidad se los suele llamar inestables (Breiman 1994, 1996).
- **Variabilidad interna del algoritmo de aprendizaje:** Por ejemplo, si consideramos algorimos como la redes neuronales, numerosos parámetros, como ser las pesos con los que se inicializa la red, son determinantes para asegurar la correcta convergencia del modelo. Estos parámetros a menu son inicializados con determinadas distribuciones probabilísticas. 
- **Variabilidad por el error inherente de clasificación:** Hace referencia a la probabilidad de que las étiquetas que tenemos disponibles en nuestros conjuntos de datos no sean efectivamente correctas. Por lo tanto, si nuestros valores verdaderos tienen una probabilidad de error `e`, entonces ningún algoritmo de aprendizaje automático podrá tener una performance mejor que `e`.

Para asegurarnos que nuestras comparaciones son confiables, una prueba estadística debe ser realizada que tenga en cuenta todos estos origenes de variaciones. 


Prueba de hipótesis [1]_
------------------------
Tradicionalmente, las métricas son comparadas utilizando una prueba de hipótesis de diferencia (inequidad) o superioridad. En una prueba de hipótesis de diferencia intentamos probar que existe una diferencia estadísticamente significativa entre las métricas. En una prueba de superioridad, intentamos probar que un modelo de aprendizaje es significativamente superior que el otro.

.. note:: Las pruebas de hipítesis de equidad o no-superioridad, aunque configuraciones válidas, no resultarán útiles en nuestro caso dado al `principio de refutabilidad <https://es.wikipedia.org/wiki/Falsabilidad>`_.

En los problemas de clasificación, en general trabajamos con métricas que resultan ser proporciones, como ser `accuracy` y `precision`. En estos casos las pruebas de hipótesis que realizamos son pruebas de diferencias entre proporciones donde tratamos de inferir las proporciones de toda la población P\ :sub:`0` y P\ :sub:`1`, a partir de las proporciones de las muestras que obtuvimos, p\ :sub:`0` y p\ :sub:`1`.

En una prueba de diferencia de proporciones se evaluan dos hipótesis: la hipótesis nula H\ :sub:`0` que establece que no existe diferencia entre las dos métricas de `accuracy` (P\ :sub:`1` - P\ :sub:`0` = 0), y una hipótesis alternativa H\ :sub:`1`  que establece que las métricas de `accuracy` son distintas (P\ :sub:`1` - P\ :sub:`0` > 0). Una prueba direccional (one tail) es a menudo útil para establecer la dirección de la diferencia. Por el principio de refutabilidad, nos interesa el caso en donde H\ :sub:`0` es rechazada en favor de H\ :sub:`1`, indicando que el modelo que estamos evaluando efectivamente ofrece una mejora con respecto al anterior.

En general, ejecutaremos esta prueba con un nivel de significancia del 95% (1-α = probabilidad de correctamente aceptar la hipótesis nulas - verdadero negativo) y un poder estádistico (1-β = probabilidad de correctamente rechazar la hipótesis nula o un verdadero positivo) de un 80% o más. El poder de un test es importante ya que experimentos con un poder bajo nos llevarán a conclusiones incorrectas sobre los resultados.

El tamaño del efecto se calcula utilizando alguna medida estadística especifica como podría ser la correlación de Pearson para relación entre variables o la distancia de Cohen para la diferencia entre grupos. El tamaño del efecto al comparar dos grupos de datos puede ser cuantificado utilizando la medida de Cohen's d. Esta medida calcula un coeficiente estandar que describe la diferencia en termino del número de desviaciones estandars en que las médias son diferentes. Un valor que generalmente se utiliza es 0.8 o un valor superior, lo cual ya es un tamañao de efecto bastante grande.

Prueba de McNemar
-----------------

5×2 Cross-Validation
--------------------


.. [1] Approximate Statistical Tests for Comparing. Supervised Classification Learning Algorithms. Thomas G. Dietterich tgd@cs . orst . edu.