===========
Performance
===========
En algunas organizaciones podemos tener requerimientos de performance especificos para nuestros modelos. Esto puede ser el caso por ejemplo de un sitio web que debe mostrar las recomendaciones de compras en un determinado lapso de tiempo para millones de usuarios. En otros casos, puede ser que los requerimientos de performance tengan que ver con que el modelo debe ejecutarse en un dispositivo que tiene limitaciones de consumo de energia, como es un teléfono celular. En ambos, puede ser que tengamos que implementar diferentes optimizaciones para mejorar la performance del modelo.

Por supuesto, una opción para que nuestros modelos se ejecuten más rápidamente es utilizar modelos más simples. Sin embargo, cuando esto no es un opción, tenemos varias alternativas:

.. note:: El siguiente contenido es opcional. Los métodos que se listan aqui son recientes y avanzados, aunque se utilizan cada vez más en modelos de aprendizaje profundo.

Optimizaciones de ejecución
---------------------------
Debido a la forma que funciona el lenguaje Python, la ejecución de un modelo en este lenguaje será mas lento que si lo hiciera en un lenguaje como C.

Quantization
------------
Quantization es una técnica que consiste en bajar la precisión de punto flotante utilizada por nuestro modelo para que tenga requerimientos menores de memoria cuando es deplegado en producción, aunque manteniendo mayoritariamente la precisión del mismo de cuando se entrenó con precisión de 32-bits. 

Pruning
-------
Pruning es una técnica en la que se eliminan pesos (weights) de una red neuronal (e incluso capas completas) en aquellos casos donde estos pesos no afectan fuertemente las predicciones del modelo. Esto le permite mantener una presición similar al modelo original, aunque con menos costo computacional.

Distillation
------------
Distillation es una técnica en la cual se entrena un modelo *estudiante* para que imite otro modelo, el cual es mas grande y potente.

