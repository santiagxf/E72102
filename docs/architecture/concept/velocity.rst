====================
Velocidades de datos
====================

.. important:: La velocidad de los datos no solo es importante en el diseño de las arquitecturas de datos que los deben procesar, sino que también tienen un impacto en el diseño de modelos de aprendizaje automático. Por ejemplo, podemos estar muy tentados en utilizar un determinado predictor en nuestros modelos y, que incluso, ofrece un poder predictivo muy alto. Sin embargo, podría ser que la velocidad a la que este dato llega a la plataforma es demasiada lenta. Un predictor que se calcula una vez al mes podría no ser útil si debemos esperar justamente 1 mes para conocer su valor.

Datos en lotes (batch)
----------------------

Mover datos en grandes cantidades conlleva tiempo. Aspectos como la velocidad de la red, el tamaño de los datos, la cantidad de archivos, y los tiempos de lectura y escritura de los sistemas de almacenamiento impactan en el tiempo total que le toma a un conjunto de datos en moverse de una ubicación a la otra.

Desafios de los datos en lotes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Datos en alta velocidad (stream)
--------------------------------
Los datos que se mueven a alta velocidad (también denominados datos calientes - o stream) son conjuntos de datos donde las muestras se generan constantemente y a una velocidad elevada, haciendo que los mismos crezcan en tamaño rápidamente.

El desafío de la velocidad
^^^^^^^^^^^^^^^^^^^^^^^^^^

Los datos con estas características proponen desafíos importantes en las arquitecturas de datos ya que la velocidad de generación hace que los mismos solo pueden ser leidos una sola vez, procesados (si es necesario), y almacenados. En algunos casos, la cantidad de información (data por la velocidad x el tamaño) que los datos son leidos, procesados y descartados inmediatamente. Es más, los computos que se pueden hacer sobre estos datos deben ser muy sencillos ya que computos complejos retrasarian la llegada y procesamiento de los siguientes datos de la secuencia.

Tiempo real (real-time)
^^^^^^^^^^^^^^^^^^^^^^^