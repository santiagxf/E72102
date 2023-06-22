Interpretación y explicaciones
==============================

A pesar de su amplia adopción, los modelos de aprendizaje automático - y especialmente aquellos basados en aprendizaje profundo - siguen siendo cajas negras a la hoja de entender como toman las decisiones que toman [1]_ . Sin embargo, comprender las razones detrás de las predicciones es importante para evaluar la confianza, que es fundamental si uno planea tomar acciones basadas en una predicción o al elegir si implementar un nuevo modelo en el contexto de una organización o proceso de negocio. Esta comprensión también proporciona información sobre el modelo, que se puede utilizar para transformar un modelo o una predicción que no son confiables en uno confiable.

Técnicas de interpretación
--------------------------

Mimic
^^^^^

Una de la técnicas más sencillas de implementar es la de "imitación". Esta técnica consiste en entrenar un nuevo modelo, interpretable, que realiza las mismas predicciones que el modelo que queremos interpretar, el cual es de caja negra. El objetivo es que, al interpretar el modelo "imitador", podamos deducir las razones por la cual el modelo "imitado" predice lo que predice. Si bien es sencillo de implementar, numerosos estudios demuestran que esta técnica no es confiable ya que no existe ninguna garantía de que el modelo "imitado" esté siguiendo el mismo patrón que el modelo "imitador". Y, en caso de que así lo fuera, entonces sería conveniente finalmente utilizar el modelo "imitador" en su lugar (ya que es un modelo interpretable). 

Saliency maps
^^^^^^^^^^^^^

En el contexto de aprendizaje profundo, los *saliency maps* se introdujeron por primera vez en el artículo titulado "Deep Inside Convolutional Networks: Visualizing Image Classification Models and Saliency Maps" [2]_. Este método se deriva del concepto de *saliency* en las imágenes el cual se refiere a características únicas (píxeles, resolución, etc.) de la imagen en el contexto del procesamiento visual. Estas características únicas representan las ubicaciones visualmente atractivas en una imagen. El mapa es, finalmente, una representación topográfica de tales pixeles. 

"El propósito del mapa es representar el nivel de atractividad en cada lugar del campo visual mediante una número escalar y guiar la selección de ubicaciones donde el modelo presta atención, según la distribución espacial de dicha atractividad. Los mapas de predictores (feature maps) proporciona información que se puede propagar ascendentemente al mapa, modelado como una red neuronal dinámica" - Laurent Itti, Christof Koch y Ernst Niebur.

Existen diferentes técnicas para generar estos mapas:

- **Basados en perturbaciones:** La idea de estos métodos es obstruir o perturbar los datos de entrada con el objetivo de medir como esta perturvación se propaga en el error del modelo. La intuición nos podría confirmar que aquellas áreas de los datos donde el modelo presta atención generarán errores más grandes cuando son perturbadas. Librerías como `SHAP` y `LIME` utilizan esta técnica.
- **Basados en gradientes:** Los métodos basados en gradientes explotan la forma en la que se entrenan los modelos de aprendizaje automático utilizando SGD. Computan los gradientes de las predicciones con respecto a los datos de entrada. Existen numerosos métodos para computar estos gradientes, cada uno explotando diferentes propiedades para generarlos. Puede encontrar mas detalle sobre estos métodos en `Pixel Attribution (Saliency Maps) <https://christophm.github.io/interpretable-ml-book/pixel-attribution.html>`_. Librerías como `AllenNLP-Interpret <https://guide.allennlp.org>`_ utilizan esta técnica.


**Referencias:**

.. [1] `Why Should I Trust You?: Explaining the Predictions of Any Classifier <https://arxiv.org/abs/1602.04938>`_
.. [2] `Deep Inside Convolutional Networks: Visualising Image Classification Models and Saliency Maps. <https://arxiv.org/abs/1312.6034>`_


.. toctree::
    :maxdepth: 1
    :caption: Ejemplos
    :glob:

    code/*
