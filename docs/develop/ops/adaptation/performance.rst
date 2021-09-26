===========
Performance
===========
En algunas organizaciones podemos tener requerimientos de performance específicos para nuestros modelos. Esto puede ser el caso por ejemplo de un sitio web que debe mostrar las recomendaciones de compras en un determinado lapso de tiempo para millones de usuarios. Una de las formás más directas de alcanzar este tipo requerimientos es a través de :doc:`../deployment/scaling`. En otros casos, puede ser que los requerimientos de performance tengan que ver con que el modelo debe ejecutarse en un dispositivo que tiene limitaciones de consumo de energia, como es un teléfono celular. Si estamos diseñando un modelo que predice la próxima palabra que el usuario va a escribir, esta predicción debe realizarse antes que el usuario termine de tipearla. Incluso, es importante tener en mente que los recursos que consumen nuestros modelos *tienen un costo*, el cual podría ser no despreciable y por el cúal las organizaciones deben pagar. 

En cualquier caso, estas restricciones nos llevarán a implementar diferentes optimizaciones para mejorar la performance del modelo y su utilización de recursos. Revisaremos en esta sección varias técnicas para alcanzar este objetivo. Por supuesto, una opción para que nuestros modelos se ejecuten más rápidamente es utilizar modelos más simples. Sin embargo, cuando esto no es un opción, tenemos varias alternativas:

.. note:: El siguiente contenido es opcional. Los métodos que se listan aqui son recientes y avanzados, aunque se utilizan cada vez más en modelos de aprendizaje profundo.

Optimización de los procesos de datos
-------------------------------------

TODO


Optimizaciones de ejecución
---------------------------
Debido a la forma que funciona el lenguaje Python, la ejecución de un modelo en este lenguaje será mas lento que si lo hiciera en un lenguaje como C. Otras opciones incluyen la utilización de herramientas de optimización como ser `NVIDIA TensorRT <https://developer.nvidia.com/tensorrt>`_, un SDK para la implementaci[on de modelos basados en aprendizaje profundo de alta performance.

Quantization
------------
Quantization es una técnica que consiste en bajar la precisión de punto flotante utilizada por nuestro modelo para que tenga requerimientos menores de memoria cuando es deplegado en producción, aunque manteniendo mayoritariamente la precisión del mismo de cuando se entrenó con precisión de 32-bits. 

Pruning
-------
Pruning es una técnica en la que se eliminan pesos (weights) de una red neuronal (e incluso capas completas) en aquellos casos donde estos pesos no afectan fuertemente las predicciones del modelo. Esto le permite mantener una presición similar al modelo original, aunque con menos costo computacional.

Distillation
------------
Distillation es una técnica en la cual se entrena un modelo *estudiante* para que imite otro modelo, el cual es mas grande y potente.

Ejemplos
--------

.. toctree::
  :maxdepth: 1
  :titlesonly:
  :glob:

  code/*