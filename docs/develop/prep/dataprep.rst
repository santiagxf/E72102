========================
Preparación de los datos
========================

Motivación
----------
TODO

Verificación
------------
El resultado del proceso de preparación de datos es un nuevo conjunto de datos con las propiedades y calidad de datos deseada. Cuando el proceso de preparación de datos está automatizado o forma parte de una rutina de entrenamiento, cómo en :doc:`../../projects/mlops/intro`, resulta interesante disponer de un proceso de verificación que se asegure que el conjnuto de datos de salido tiene las propiedades que se esperan. Una forma de realizar esto es a través del concepto de `expectativas` o `expectations`.

Expectativas
^^^^^^^^^^^^
Una `expectativa` o `expectation` es una directiva que describe una propiedad verificable en un conjunto de datos. Si está familiarizado con el desarrollodo de código, al igual que `assertion` describe el comportamiento deseado del código, `expectation` describe el comportamiento deseado en los datos. Su utilización nos permite no solo mejorar la calidad de los datos al hacer explicito nuestras demandas/suposiciones sobre los mismos sino que también es una forma efectiva para los propietarios de los datos de comunicar qué deben y qué no deben esperar de los datos los ingenieros de datos/cientificos de datos al utilizar tales conjuntos. 

Ejemplos
^^^^^^^^

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/expectations.ipynb
