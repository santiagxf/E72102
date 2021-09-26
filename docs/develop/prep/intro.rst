============
Preparación
============

Las técnicas de aprendizaje automático han logrado resolver problemas que serían casi imposibles de resolver escribiendo software de forma manual. Sin embargo, el procesamiento de los datos ocupa una gran cantidad del tiempo total que comprende todo el ciclo de desarrollo de un modelo de aprendizaje automático. Sin datos de buena calidad sobre los cuales aprender, estás técnicas simplemente no funcionan.

¿Por qué es importante focalizarse en los datos?
------------------------------------------------
En los sitemas basados en aprendizaje automático, aquellos que utilizan la mayor cantidad y calidad de datos son los ganadores. Esta realidad hace que muchos equipos de desarrollo se focalizen en la mejora continua de sus datos **data centric** en lugar de la arquitectura del modelo **model centric**.

En general, los equipos que están involucrados en el desarrollo de modelos de aprendizaje automático están familiarizados o bien con las tareas de administración de datos o con las tareas de modelado, pero por separado. 

Existen multiples diferencias entre diseñar una solución de software y diseñar una solución de aprendizaje automático:

.. csv-table:: Diferencias entre diseñar una solución de software y diseñar una solución de aprendizaje automático
   :header: "Caracteristica", "Software", "Modelos de aprendizaje automático"
   :widths: 20, 50, 50

   "Objetivo", "Correctitud", "La optimización de una métrica"
   "Calidad*", "Depende deterministicamente del código", "Depende de los datos, de la arquitectura del modelo y sus hiperparámetros"


.. toctree::
   :maxdepth: 1
   :caption: En esta sección
   :hidden:

   Preparación de datos <dataprep>
   Ingeniería de predictores <engineering>