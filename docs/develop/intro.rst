========================================================
Ciclo de desarrollo de modelos de aprendizaje automático
========================================================

El modelo de aprendizaje automático propiamente dicho es tan solo una pequeña parte dentro de un proyecto que está basado en aprendizaje automático. Si incluso mantenieramos lo mínimo indispensable, encontrariamos que necesitaríamos datos sobre los cuales entrenar nuestro modelo, infraestructura donde ejecutarlo y alguna forma de consumirlo.

.. figure:: _images/infraestructure.png
  :alt: Infraestructura relacionado con Machine Learning

  *Componentes dentro de una solución de aprendizaje automático*

Proceso
-------
El proceso de desarrollo es un proceso iterativo, y es importante entender que en general no entraremos en este proceso *una vez*, sino que lo haremos **multiples veces**. Desarrollar y desplegar nuevas versiones de los modelos de aprendizaje automático es central para implementar `mejora continua <https://es.wikipedia.org/wiki/Proceso_de_mejora_continua>`_. Existen varias razones para iterar y desplegar nuevas versiones de los modelos incluyendo su degradación de performance en el tiempo, cambios en los esquemas de los datos, etc. En algunos casos puede ser que las consideraciones de negocio hayan cambiado, que el proceso de recolección de datos haya mejorado o que simplemente nuestros científicos de datos encontraron una mejor forma que resuelve el problema.

.. figure:: _images/ml_process.png
   :alt: Proceso de desarrollo de modelos de aprendizaje automático
   :align: center

   *Proceso de desarrollo de modelos de aprendizaje automático*

Iteraciones
-----------
En algunas organización, estas iteraciones pueden darse bastante rápido. Por ejemplo, es posible que nuevas muestras de datos estén disponibles todos los días y que existen requerimientos de negocio para reentrenar el modelo considerando estas nuevas observaciones. Si bien reentrenar no implica volver a realizar ingeniería de predictores o selección de modelos, si requerirá verificar que el conjunto de datos luce como se espera, por ejemplo. En este caso, disponer de procesos automáticos para implementar todo el ciclo que describiremos a continuación es fundamental. Lo importante es que el **que tan lejos llegaremos con nuestro modelo está controlado por cuantas veces iteramos sobre el proceso, en lugar de por el tiempo invertimos en cada iteración**. Esto es un cambio importante en la filosofía de desarrollo. Vea :ref:`rst_mlops` para una visión mas ámplia sobre este último concepto.

Desafios:
 - Los modelos de aprendizaje automático son una combinación de codigo y datos.
 - El desarrollo de estos modelos requiere involucrar multiples roles y personas dentro de la organización.
 - Se deben integrar una gran cantidad de piezas para poder cubrir el ciclo de desarrollo de un modelo de aprendizaje automático.



