========
Robustes
========

La performance de un modelo de aprendizaje automático puede degradarse significativamente cuando se los expone a pequeñas variaciones en los datos de entrada que se le suministran. Un modelo de aprendizaje automático se dice `robusto` cuando el mismo mantene el comprotamiento deseado ante pequeñas perturbaciones, tales como el ruido, muestras fuera de la distribución de entrenamiento (out-of-distribution) e incluso ejemplos adversarios (:ref:`rst_adversarial_examples`).

.. note::
  Note que las perturbaciones pueden realizarse sobre los datos de entrada y sobre algunos aspectos del modelo, como puede ser eliminar alguna de las capas de la red neuronal. En cualquier caso, el concepto de robustes siempre está asociado a algún tipo de perturbación.
  
