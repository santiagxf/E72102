==================
Control de calidad
==================
Hoy en día, gracias a la práctica de Ingeniería de Software, contamos con un conjunto maduro de herramientas y metodologías para el aseguramiento de la calidad en sistemas de software. Sin embargo, su contrapartida en el mundo de datos y modelos de aprendizaje automático no ha alcanzado tal madurez aún. Esto genera desafíos en las organizaciones para incorporar estas tecnologías en los procesos de negocio con la seguridad, confianza y robustes que se requiere.

.. note:: Si bien se menciona el proceso de control de calidad dentro del proceso de operacionalización del modelo, es importante mencionar que la práctica de control de calidad debe implementarse a lo largo de todo el proceso de desarrollo. El equipo del proyecto de desarrollo debe asegurarse que existen prácticas en cada una de las fases que aseguran la correcta calidad del mismo, favoreciendo el concepto **fail-fast, move-quickly** (fallar temprano, moverse rápido) del desarrollo ágil. Vea :ref:`rst_agile`

La práctica de control de calidad o *testing* consiste en aplicar el modelo a un conjunto de datos previamente curado para validar las salida contra los requerimientos de negocio. 

.. note:: Las prácticas ágiles utilizan el proceso de validación no solo para validación técnica sino que también para crear documentación y validar el producto de acuerdo a los lineamientos de la organización. En particular, esto significa que todos los origines de datos utilizados, modelos, o cualquier otra pieza utilizada por el modelo debe ser identificada ya que podría contener implicaciones legales (como derechos de autor y derechos de uso).

Conjunto de datos de validación
-------------------------------
La forma en la que se genera y el tamaño del conjunto de datos de validación dependerá del escenario de negocio particular en el que estamos trabajando. En algunos escenarios el conjunto de datos puede generarse sintéticamente mientras que en otros puede provenir del mundo real. 

.. warning:: El conjunto de datos de validación es especialmente diseñado para el proposito de control de calidad y no debe confundirse con el set de datos, también llamado de validación, utilizado durante la fase de entrenamiento del modelo.

Los conjuntos de datos generados sintéticamente son útiles para validar condiciones específicas del modelo, como ser valores extremos en algunos predictores, valores faltantes o cuyo valor es cero, etc). Los conjuntos de datos provenientes del mundo real en general contienen datos que fueron colectados por procesos controlados y suelen ser llamados *dorados* o *golden-dataset*. Estos conjuntos de datos son de extremado valor para la organización ya que en general tienen un costo elevado para ser generados. Puede ser que la organización haya tenido que pagar por ellos, pagar a personas para que los curen o incluse para collectar feedback y *labels* o *valores verdaderos*.

Ejemplos
^^^^^^^^

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/data_gen.ipynb

Protecciones
------------
TODO

Control de rango de predictores
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
TODO

Control de rango de predicciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
TODO

Conformal predictions
^^^^^^^^^^^^^^^^^^^^^
TODO

Aserción de métricas
--------------------
Sobre los sets de datos de validación se colectan métricas, tanto estadísticas como de ejecución:
 - Estadisticas:
   - Accuracy
   - Precision
   - Recall
   - Coefficient of determination
 - Ejecución:
   - Latencia promedio de ejecución
   - Latencia (percentil 95)
   - Memoria promedio consumida

Para cada una de estas métricas se deben diseñar tests (también conocidos como *expectations* o *assertions*) que deberán fallar cuando los valores están fuera de los rangos aceptados. Por ejemplo, un test podría fallar si *Accuracy* está por debajo del 85%, o si hay un 5% de inferencias que tardan más de 300 milisegundos en ejecutarse. Adicionalmente estas métricas son comparadas con la versión anterior del modelo (si hubiera una) para constatar que la performance del mismo no ha sido dañada en alguna dimensión.

.. note:: En muchos casos, todas estas métricas son recolectadas para el conjunto de datos de validación en su totalidad como también para diferentes cortes (cohorte) de datos donde las instancias tienen atributos protegidos. Vea `Análisis de errores`_ para más detalle.

Ejemplos
^^^^^^^^

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/expectations.ipynb

Análisis de errores
-------------------
En muchos casos, es importante diseñar tests que dividan el conjunto de datos en subpoblaciones o *slices* basandose en atributos protegidos (los cuales prodrían o no ser predictores utilizados por el modelo). La práctica de analisis de errores trata de identificar como nuestro modelo comete los errores y cómo se distribuyen esos errores dentro del conjunto de datos y dentro de cada uno de los subconjuntos que generamos. Esta técnica también suele utilizarse para asegurar que nuestro modelo sea justo (*fairness*), un procedimiento mandatorio para cualquier modelo que intervenga con datos de personas ya que podría haber requerimientos de negocio, regulatorios y legales que penalizen a la organización por no realizarlo.

Ejemplos
^^^^^^^^

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/error_analysis.ipynb
  code/what_if.ipynb
  code/fairlearn.ipynb

Champion/Challenger
-------------------
TODO.

Dependencias
------------
Es muy común que nuestros modelos hayan sido desarrollados con la ayuda de librerias de software especificas. Muchas de ellas pueden provenir de provedores que son `autoridad (authoritative) <https://en.wikipedia.org/wiki/Domain_authority>`_ como ser TensorFlow o PyTorch. Sin embargo, otras librerias más puntuales podrían provenir de desarolladores independientes. Cuando una pieza de software es desplegada en producción, todas sus dependencias también sos desplegadas a producción. Por esta razón, y particularmente por razones de seguridad, las organizaciones solo permiten el despliegue de librerias vía una *lista blanca (white-list)*, es decir, librerias que son conocidas por la organización. Si bien muchas de estas organizaciones pueden implementar procesos automáticos de validación y *white-listing* de librerias, esto compromete la velocidad de inovación de los equipos de desarrollo y por lo tanto debe ser tenido en cuenta no solo en la fase de validación sino también durante todo el desarrollo.
