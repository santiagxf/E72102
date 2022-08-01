====================
Velocidades de datos
====================

.. important:: La velocidad de los datos no solo es importante en el diseño de las arquitecturas de datos que los deben procesar, sino que también tienen un impacto en el diseño de modelos de aprendizaje automático. Por ejemplo, podemos estar muy tentados en utilizar un determinado predictor en nuestros modelos y, que incluso, ofrece un poder predictivo muy alto. Sin embargo, podría ser que la velocidad a la que este dato llega a la plataforma es demasiada lenta. Un predictor que se calcula una vez al mes podría no ser útil si debemos esperar justamente 1 mes para conocer su valor.

.. _rst_data_batch:

Datos en lotes (batch)
----------------------

Mover datos en grandes cantidades conlleva tiempo. Aspectos como la velocidad de la red, el tamaño de los datos, la cantidad de archivos, y los tiempos de lectura y escritura de los sistemas de almacenamiento impactan en el tiempo total que le toma a un conjunto de datos en moverse de una ubicación a la otra.

Desafios de los datos en lotes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Aunque el procesamiento por lotes es eficiente, rentable y rápido, tiene algunas desventajas:

:Costos: El costo operativo del procesamiento por lotes puede ser bajo, pero el costo total inicial de establecer la infraestructura en primer lugar es relativamente más alto.
:Volumenes: La gran cantidad de datos que estos procesos suelen utilizar pone desafios importantes sobre la infraestructura que los procesa. Arquitecturas específicas han surgido como resultado de estos requerimientos, tales como MapReduce. Sin embargo, continua existiendo una tensión entre la eficiencia del procesamiento y la capacidad de escalar eficientemente el costo de infraestructura a medida que los datos aumentan.
:Recuperación ante errores: El procesamiento por lotes suele ser procesos largos que involucran la ejecución de varios pasos sobre grandes volumenes de datos. Como consecuencia, si alguno de estos pasos genera un error, es posible que los datos queden en un estado donde la mitad han sido procesados y la otra mitad no. En estas situaciones, simplemente reiniciar el proceso podria llevar a duplicidad de datos. 
:Identificación de problemas: El hecho de que estos procesos demoren tiempo de procesamiento hace que identificar problemas no sea sencillo. Reproducir un problema podria tardar horas, lo cual dificulta la capacidad de detectarlo.
:Complejidad: La gran cantidad de datos que se procesan sobre numerosos origenes de datos propone desafios de complejidad a la hora de administrar estos tipos de sistemas.

.. _rst_data_stream:

Datos en alta velocidad (stream)
--------------------------------

Los datos que se mueven a alta velocidad (también denominados datos calientes - o stream) son conjuntos de datos donde las muestras se generan constantemente y a una velocidad elevada, haciendo que los mismos crezcan en tamaño rápidamente.

El desafío de la velocidad
^^^^^^^^^^^^^^^^^^^^^^^^^^

Los datos con estas características proponen desafíos importantes en las arquitecturas de datos ya que la velocidad de generación hace que los mismos solo pueden ser leidos una sola vez, procesados (si es necesario), y almacenados. En algunos casos, la cantidad de información (data por la velocidad x el tamaño) que los datos son leidos, procesados y descartados inmediatamente. Es más, los computos que se pueden hacer sobre estos datos deben ser muy sencillos ya que computos complejos retrasarian la llegada y procesamiento de los siguientes datos de la secuencia.

Otros desafios incluyen:

:Escalabilidad y tolerancia: Los sistemas deprocesamiento en alta velocidad tienen presiones de escalabilidad importantes. Fallas en el sistema de procesamiento, demoras en las comunicaciones, pueden hacer que periodos donde no se reciben datos estén seguidos de periodos donde el sistema es inundado con información que no se puedo enviar en el momento correcto.
:Ordenamiento: Las comunicaciones no son perfectas y en muchos casos la información que llega en alta velocidad puede no estar en orden. Para muchas aplicaciones, el orden es de vital importancia, como podría ser por ejemplo un bot que procesa mensajes de un chat. Asegurar el procesamiento en orden es primordial.
:Garantias de procesamiento: Las dificultades de los medios de comunicación pueden hacer que un mensaje o instancia de dato sea enviado mas de una vez. Los sistemas de procesamiento deben poder asegurar que cada instancia de datos se procesa una vez y solo una vez.