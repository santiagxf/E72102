.. _rst_data_adquisition:

====================
Adquisición de datos
====================


Datos en alta velocidad (stream)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Los datos que se mueven a alta velocidad (también denominados datos calientes - o stream) son conjuntos de datos (generalmente secuenciales) cuya velocidad y frecuencia de generación y captura es tan alta que los mismos solo pueden ser leidos una sola vez. Es más, los computos que se pueden hacer sobre estos datos deben ser muy sencillos ya que computos complejos retrasarian la llegada y procesamiento de los siguientes datos de la secuencia.

Es relativamente sencillo detectar cambios abruptos en la distribución de los datos utilizando técnicas de detección de desviaciones. Sin embargo, estas técnicas presentan dificultades cuando dichas desviaciones suceden de forma gradual y sostenida en el tiempo. Algo que es común en los origenes de datos de alta velocidad.

Para detectar estas pequeñas fluctuaciones en los datos en general se utilizan técnicas que entran en algunas de las siguientes 3 categorías.

Memoria parcial:
Los métodos de memoria parcial utilizan alguna variación de la idea de ventana de tiempo (rolling window). En cada momento se mantiene una ventana que contine solo las observaciones más recientes, las cuales son utilizadas para el proceso de aprendizaje. Uno de los puntos más críticos de estas técnicas es la elección del tamaño de la ventana a considerar. Para detectar