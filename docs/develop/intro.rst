========================================================
Ciclo de desarrollo de modelos de aprendizaje automático
========================================================

.. image:: _images/infraestructure.png
  :alt: Infraestructura relacionado con Machine Learning

Iteración
---------
Como vimos, el proceso de desarrollo es un proceso iterativo. Desarrollar y desplegar nuevas versiones de los modelos de aprendizaje automático es central para implementar mejora continua. Existen varias razones para desplegar nuevas versiones de los modelos incluyendo la degradación de su performance en el tiempo. En algunos casos puede ser que las consideraciones de negocio hayan cambiado, que el proceso de recolección de datos haya mejorado o que simplemente nuestros científicos de datos encontraron un mejor modelo que resuelve el problema.

En algunas organización, estas iteraciones pueden darse bastante rápido. Por ejemplo, es posble que nuevas muestras de datos estén disponibles todos los días y que existen requerimientos de negocio para reentrenar el modelo considerando estas nuevas observaciones. Si bien reentrenar no implica volver a realizar ingeniería de predictores o selección de modelos, si requerirá verificar que el conjunto de datos luce como se espera, por ejemplo. En este caso, disponer de procesos automáticos para implementar todo el ciclo que describiremos a continuación es fundamental. Vea :ref:`rst_mlops` 




