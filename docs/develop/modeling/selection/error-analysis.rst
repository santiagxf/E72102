.. _rst_error_analysis:

===================
Análisis de errores
===================

Más allá del valor de la métrica específica, es importante entender cómo nuestro modelo se comporta. La práctica de análisis de errores trata de identificar cómo nuestro modelo comete los errores y cómo se distribuyen esos errores dentro del conjunto de datos y, en particular, en algunos subconjuntos con determinados atributos. En muchos casos es importante diseñar *pruebas* que dividan el conjunto de datos en subpoblaciones o *slices* basandose en atributos protegidos (los cuales prodrían o no ser predictores utilizados por el modelo). Esta técnica también suele utilizarse para asegurar que nuestro modelo sea justo (*fairness*), un procedimiento mandatorio para cualquier modelo que utilize datos de personas ya que podría haber requerimientos de negocio, regulatorios o legales que penalizen a la organización por no realizarlo. Por ejemplo, podríamos preguntarnos "¿Cúal es la performance de nuestro modelo de reconocimiento de voz cuando el interlocutor tiene un acento determinado?".

.. note:: Si está interesado en la temática de equidad en modelos de aprendizaje automático puede obtener más detalle en el artículo: `¿Qué significa que un modelo sea justo? <https://santiagof.medium.com/qu%C3%A9-significa-que-un-modelo-sea-justo-793be6741b95>`_ .

Hacer este tipo de preguntas llevan a nuestro análisis de performance mucho más lejos que cuando miramos simplemente una métrica en particular como la presición o el coeficiente de determinación. 

Tomarse el tiempo para entender cómo y por qué nuestro modelo comete errores tiene numerosos beneficios incluyendo:

 - Puede ayudarnos a identificar zonas donde no tenemos suficiente cantidad de datos. Por ejemplo, si nuestro modelo comete muchos errores clasificando frutas pero no clasificando animales, entonces podríamos querer aumentar el conjunto de datos con más imágenes de frutas.
 - Si sabemos que nuestro modelo tiene especiales complicaciones manejando determinado tipo de casos, podríamos decidir imponer algunas restricciones en su uso para prevenir fallas más gráves en los procesos de negocio que lo utilizan. Vea :doc:`../../ops/validation/riskmodel`. 
 - Puede ayudarnos a identificar problemas fundamentales en nuestro modelo que nos hagan replantearnos si el modelo debería llegar a producción. Por ejemplo, si nuestro modelo comete determinados errores con determinado género de las personas, quizás deberíamos evaluar no utilizarlo.

Ejemplos
--------

.. toctree::
  :maxdepth: 1
  :titlesonly:

  code/error_analysis.ipynb
  code/what_if.ipynb
  code/model_analysis.ipynb
  code/fairlearn.ipynb