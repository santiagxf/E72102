==================
Control de calidad
==================

  "One test is worth a thousand expert opinions"

  -- Tex Johnson, Test Pilot at Boeing.

Hoy en día, gracias a la práctica de Ingeniería de Software, contamos con un conjunto maduro de herramientas y metodologías para el aseguramiento de la calidad en sistemas de software. Sin embargo, su contrapartida en el mundo de datos y modelos de aprendizaje automático no ha alcanzado tal madurez aún. Esto genera desafíos en las organizaciones para incorporar estas tecnologías en los procesos de negocio con la seguridad, confianza y robustes que se requiere.

.. note:: Si bien se menciona el proceso de control de calidad dentro del proceso de operacionalización del modelo, es importante mencionar que la práctica de control de calidad debe implementarse a lo largo de todo el proceso de desarrollo. El equipo del proyecto de desarrollo debe asegurarse que existen prácticas en cada una de las fases que aseguran la correcta calidad del mismo, favoreciendo el concepto **fail-fast, move-quickly** (fallar temprano, moverse rápido) del desarrollo ágil. Vea :ref:`rst_agile`

En general, la práctica de control de calidad o *testing* consiste en aplicar el modelo a un conjunto de datos previamente curado para validar las salidas contra los requerimientos de negocio. Se suelen utilizar multiples conjuntos de datos para validar diferentes cualidades del modelo y asegurar su correcto desenvolvimiento en diferentes escenarios, situaciones límite o condiciones de borde.

.. note:: Las prácticas ágiles utilizan el proceso de validación no solo para validación técnica sino que también para crear documentación y validar el producto de acuerdo a los lineamientos de la organización. En particular, esto significa que todos los origines de datos utilizados, modelos, o cualquier otra pieza utilizada por el modelo debe ser identificada ya que podría contener implicaciones legales (como derechos de autor y derechos de uso).

Sobre el ambiente de validación
-------------------------------
En muchas organizaciones los ambientes de desarrollo y verificación son distintos, siendo los ultimos ambientes donde los desarrolladores responsables del modelo de aprendizaje automático no tienen acceso para realizar modificaciones. Con el objetivo de que nuestras pruebas provean de la mayor predictibilidad de lo que sucederá cuando el modelo esté finalmente productivo, intentaremos que el ambiente de verificación sea tan similar como sea posible al ambiente de producción.

Teniendo esto en mente, pueden existir algunas diferencias entre los ambientes de desarrollo y verificación:

Dependencias
^^^^^^^^^^^^
Es muy común que nuestros modelos hayan sido desarrollados con la ayuda de librerias de software específicas. Muchas de ellas pueden provenir de provedores que son `autoridad (authoritative) <https://en.wikipedia.org/wiki/Domain_authority>`_ como ser TensorFlow o PyTorch. Sin embargo, otras librerias más puntuales podrían provenir de desarolladores independientes. Cuando una pieza de software es desplegada en producción, todas sus dependencias también sos desplegadas a producción. Por esta razón, y particularmente por razones de seguridad, las organizaciones solo permiten el despliegue de librerias vía una *lista blanca (white-list)*, es decir, librerias que son conocidas por la organización. Si bien muchas de estas organizaciones pueden implementar procesos automáticos de validación y *white-listing* de librerias, esto compromete la velocidad de inovación de los equipos de desarrollo y por lo tanto debe ser tenido en cuenta no solo en la fase de validación sino también durante todo el desarrollo.


Conjunto de datos de validación
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
La forma en la que se genera y el tamaño del conjunto de datos de validación dependerá del escenario de negocio particular en el que estamos trabajando. En algunas organizaciones el conjunto de datos puede provenir del mundo real mientras que en otros escenarios puede generarse sintéticamente debido a cuestiones de seguridad o porque se desea construir verificaciones más robustas.

.. warning:: El conjunto de datos de validación es especialmente diseñado para el proposito de control de calidad y no debe confundirse con el conjunto de datos, también llamado de validación, utilizado durante la fase de entrenamiento del modelo.

Los conjuntos de datos generados sintéticamente son útiles para validar condiciones específicas del modelo, como ser valores extremos en algunos predictores, valores faltantes o cuyo valor es cero, etc). Los conjuntos de datos provenientes del mundo real en general contienen datos que fueron colectados por procesos controlados y suelen ser llamados *dorados* o *golden-dataset*. Estos conjuntos de datos son de extremado valor para la organización ya que en general tienen un costo elevado para ser generados. Puede ser que la organización haya tenido que pagar por ellos, pagar a personas para que los curen o incluse para collectar feedback y *labels* o *valores verdaderos*.

Ejemplos
~~~~~~~~

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/data_gen.ipynb

Protecciones
------------
Las protecciones o *guardrails* son verificaciones que se pueden instrumentar en los procedimientos de consumo de datos y generación de salida para asegurarse que determinadas variables tienen valores dentro de rangos específicos. Por ejemplo, si tenemos un modelo que predice las RPM de una bomba, sabemos que la misma no podría ser negativa y tampoco podría mostrar valores exageradamente altos.

.. _rst_testing_predictors:

Control de rango de predictores
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Consiste en la verificación de los rangos de los valores de los predictores con los que se alimenta nuestro modelo. Esto puede suceder en 2 momentos: en tiempo de entrenamiento o en tiempo de inferencia. 

Predictores con valores fuera de rango en tiempo de entrenamiento/reentrenamiento pueden evidenciar problemas de cálidad de datos y en general requieren de una inspeccción de los procesos de ingesta o transformación de datos. Valores fuera de rango en tiempo de inferencia puede suponer un error en los procesos de ingesta de datos pero también un cambio en la definición de los datos (por ejemplo, una variable que pasó de medirse de pascales a hectopascales).

Control de rango de predicciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
De igual forma que el control de rango en los predictores, podemos realizar el mismo control sobre la salida del modelo. Aquí la interpretación es distinta ya que un modelo que genera predicciones fuera del rango esperado debería, aunque no siempre, representar un problema de generalización.

Se pueden tomar varias estrategias para resolver este problema:
 - Retornar la predicción fuera de rango.
 - Reemplazar la predicción por un valor específico.
 - No retornar valor alguno.

.. warning:: Es recomendable siempre notificar a la aplicación que consume la predicción sobre este error.

Independientemente del casos, la cantidad de veces que el modelo comete este tipo de error puede ser una métrica de calidad que podemos monitorear y controlar a través del `Aseguramiento de métricas`_ .

Conformal predictions
^^^^^^^^^^^^^^^^^^^^^
Se trata de una técnica que utiliza la experiencia previa para determinar los niveles de confianza con los que un modelo realiza predicciones. Básicamente intenta responder la pregunta de *¿qué tan buenas son las predicciones que realiza nuestro modelo?* o, si nuestras predicciones son números, *¿qué tan cerca estimamos que esté la predicción al valor verdadero?*.

.. note:: Para más información sobre esta técnica recomendamos la lectura de: `A Tutorial on Conformal Prediction <https://www.jmlr.org/papers/v9/shafer08a.html>`_

Aseguramiento de métricas
-------------------------
Sobre los sets de datos de validación se colectan métricas, tanto estadísticas como de ejecución:

* Estadísticas

  * Accuracy
  * Precision
  * Recall
  * Coefficient of determination

* Ejecución

  * Latencia promedio de ejecución
  * Latencia (percentil 95)
  * Memoria promedio consumida

Para cada una de estas métricas se deben diseñar pruebas o tests que deberán fallar cuando los valores están fuera de los rangos aceptados. Por ejemplo, un test podría fallar si *Accuracy* está por debajo del 85%, o si hay un 5% de inferencias que tardan más de 300 milisegundos en ejecutarse. Adicionalmente estas métricas son comparadas con la versión anterior del modelo (si hubiera una) para constatar que la performance del mismo no ha sido dañada en alguna dimensión.

.. note:: En muchos casos, todas estas métricas son recolectadas para el conjunto de datos de validación en su totalidad como también para diferentes cortes (cohorte) de datos donde las instancias tienen atributos protegidos. Vea `Análisis de errores`_ para más detalle.

En general, estas métricas suelen ser estimadas utilizando mecanismos robustos ya sea mediante validación cruzada o utilizando :ref:`rst_confidence_intervals`.

Análisis de errores
-------------------
La práctica de analisis de errores trata de identificar cómo nuestro modelo comete los errores y cómo se distribuyen esos errores dentro del conjunto de datos y en particular en algunos subconjuntos con determinados atributos. En muchos casos, es importante diseñar tests que dividan el conjunto de datos en subpoblaciones o *slices* basandose en atributos protegidos (los cuales prodrían o no ser predictores utilizados por el modelo). Esta técnica también suele utilizarse para asegurar que nuestro modelo sea justo (*fairness*), un procedimiento mandatorio para cualquier modelo que intervenga con datos de personas ya que podría haber requerimientos de negocio, regulatorios y legales que penalizen a la organización por no realizarlo. Por ejemplo, podríamos preguntarnos "¿Cúal es la performance de nuestro modelo de reconocimiento de voz cuando el interlocutor tiene un acento determinado?".

Hacer este tipo de preguntas llevan a nuestro análisis de performance mucho mas lejos que cuando miramos simplemente una métrica en particular como la presición o el coeficiente de determinación. 

Tomarse el tiempo para entender cómo y porqué nuestro modelo comete errores tiene numerosos beneficios incluyendo:
 - Puede ayudarnos a identificar zonas donde no tenemos suficiente cantidad de datos. Por ejemplo, si nuestro modelo comete muchos errores clasificando frutas pero no clasificando animales, entonces podríamos querer aumentar el conjunto de datos con más imágenes de frutas.
 - Si sabemos que nuestro modelo tiene especiales complicaciones manejando determinado tipo de casos, podríamos decidir imponer algunas restricciones en su uso para prevenir fallas más gráves en los procesos de negocio que lo utilizan. Vea :doc:`riskmodel`. 
 - Puede ayudarnos a identificar problemas fundamentales en nuestro modelo que nos hagan replantearnos si el modelo debería llegar a producción. Por ejemplo, si nuestro modelo comete determinados errores con determinado género de las personas, quizás deberíamos evaluar no utilizarlo.


Ejemplos
^^^^^^^^

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/error_analysis.ipynb
  code/what_if.ipynb
  code/fairlearn.ipynb

Verificación en producción
--------------------------
En muchas ocaciones, nuestros modelos interactuan con nuestros usuarios o procesos de negocio y por lo tanto es complejo verificar que el comportamiento que finalmente tenga el modelo en la organización es aquel que deseamos. Esto por ejemplo podría ser el caso de un modelo de recomendaciones. Podría ser que nuestro modelo efectivamente cumpla con todos nuestras pruebas de validación pero, *¿cómo podríamos estar seguro que un nuevo modelo o técnica para ofrecer recomendaciones a nuestros usuarios es mejor que la forma actual que tenemos de hacerlo?*. En algunos sitios de e-commerce, un modelo que no tiene la performance que se espera podría significar pérdidas para nada despereciables para la organización.

Para estas situaciones, es posible realizar despliegues controlados de nuestros modelos de aprendizaje automático en producción y experimentar con una porción reducida de usuarios para poder sacar conclusiones. En el capitulo :doc:`../deployment/deployment` revisaremos diferentes técnicas para disponibilizar nuestros modelos y poder verificar que tan buenos o malos son en realidad. En particular, las técnicas más útiles en esta configuración son:

* :ref:`rst_shadow_testing`
* :ref:`rst_ab_testing`
* :ref:`rst_champion_challenger`
* :ref:`rst_testing_interleaving`
