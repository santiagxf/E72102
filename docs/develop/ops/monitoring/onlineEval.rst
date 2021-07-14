.. _rst_online_evaluation:

===================
Evaluación en linea
===================
De igual forma que evaluamos la performance de nuestro modelo durante su desarrollo/validación para estimar su performance, una vez que un modelo de aprendizaje automático alcanza producción, deberemos de instrumentar mecanismos que nos aseguren de que dicha performance que estimamos durante el desarrollo continua siendo la performance real que la organización obtiene como parte del algún proceso de negocio. Este procedimiento se lo conoce como **evaluación en linea**.

Degradación del modelo
----------------------
Degradación del modelo hace referencia a la situación donde un modelo de aprendizaje automático tiene una performance menor cuando se ejecuta en producción en comparación con la performance que pudimos medir durante nuestra fase de validación. Esta degradación puede manifestarse de forma abrupta en el mismo momento que el modelo alcanza producción o de forma gradual, a medida que pasa el tiempo.

Probablemente una degradación abrupta es el resultado de una incorrecta publicación del modelo debido a versiones de librerias, utilización de los resultados de las predicciones, o que los predictores que el modelo tiene como entrada no se condicen con aquellos con los que el modelo de aprendizaje automático se entreno.

Una degradación gradual, en general, tiene que ver con la evolución de los datos que nuestro modelo consume. La performance de un modelo de aprendizaje automático en producción es un reflejo de que tan bien los datos de entrenamiento de condicen con los datos productivos. Dado que en general el mundo es dinámico, es posible que en algún momento el modelo deje de poder capturar los patrones que los (nuevos) datos exhiben. Cuando un modelo de aprendizaje automático es desplegado de forma productiva, detectar estos cambios en la distribución de los datos es clave para asegurarse que las predicciones que generamos son válidas y que pueden ser consumidas de forma segura por otros procesos dentro de la organización.

Valores verdadedores o etiquetas
--------------------------------
Los valores verdaderos (o ground truth) es simplemente la respuesta correcta a la pregunta de negocio que el modelo se suponia que debía responder. Por ejemplo, si estamos diseñando un modelo que predice si un cliente debería recibir o no un correo electrónico promocional, el valor verdadero para el modelo sería si finalmente el usuario tomó la promoción que le enviamos o no. Esta información es de mucho interes porque básicamente nos permite calcular que tan bueno o malo es nuestro modelo en resolver este problema de negocio en la realidad.

Evaluación de perfomance en linea
---------------------------------
En algunos casos, obtener los valores verdaderos de las predicciones es muy rápido, por ejemplo, cuando mostramos una publicidad en un sitio web - si el usuario le hace click antes de irse de la página entonces la predicción será correcta y si no lo hace entonces será incorrecta. Por el contrario, en otros procesos de negocio podría tomar tiempo determinar cual es el valor correcto. Este es el caso de un sistema de detección de fraudes por ejemplo, donde podría tomar meses antes de saber si la transacción es efectivamente fraudulenta o no. Esta demora en obtener los valores verdaderos no es trivial porque además condicionará que tan frecuentemente podemos reentrenar nuestro modelo.

En los casos donde la valores verdaderos de la variable objetivo no están disponibles, una alternativa para la evalución en linea es la evaluación de desviaciones covariable. Vea :ref:`rst_covariate_shift`

.. note:: La evaluación via desviaciones covariables se basa en el principio de que el modelo solo performará correctamente si los datos con los que fué entrenado (muestra) reflejan correctamente el comportamiento y valores en el mundo real (población). Por lo tanto, si una comparación entre los datos que se utilizaron durante el entrenamiento y los datos que el modelo ve en producción arrojan diferencias, entonces tenemos evidencia para sostener la idea que el modelo no performará bien.

Si bien esta alternativa nos permite detectar desviaciones, la solución a este problema no es tan sencilla de implementar. Al no disponer de los valores verdaderos en la variable objetivo, reentrenar el modelo no es una opción en el corto plazo. Intervención manual será requerida en este caso ya que es necesario identificar los factores que están causando la desviación en los datos de entrada. Los desarroladores del modelo pueden evaluar la situación y aplicar técnicas para corregirlo incluyendo eliminar algunos predictores o cambiar la estrategia de muestreo (resampling). Aquí es donde se vuelve piramidal la estrategia de :ref:`rst_alerts` 

.. _rst_model_retrain:

Reentrenamiento del modelo
--------------------------
Ya sea por degradación abrupta o gradual o simplemente porque hemos colectado nuevos datos, deberemos decidir frecuentemente reentrenar nuestro modelo para capturar los nuevos patrones que se exiben en los datos. No existe una regla de que tan frecuentemente deberíamos de realizar este reentrenamiento. En general esto depende de la industria en la que estamos, del rol que cumple el modelo y de la magnitud de sus degraciones. En algunos casos, como ser modelos que modelan características físicas como la dinámica de una bomba, no esperariamos que estos modelos se degraden en el tiempo ya que en general las reglas de la dinámica de fluidos continuan siendo las mismas. Sin embargo, en otros casos, como podría ser la personalización de la experiencia en una pagina de e-commerce, podriamos necesitar reentrenar el modelo frecuentemente para capturar cambios de habitos en las personas.

Sabemos que reentrenaremos nuestro modelo al menos cada vez que detectamos una degradación de la performance. Sin embargo, en el resto de las situaciones, esta decisión dependerá de:
 - ¿Que tan sencillo es obtener los valores verdaderos (ground truth) para el nuevo set de datos?
 - ¿Cúal es el costo de un proceso de entrenamiento?
 - ¿Qué tan sencillo es actualizar la versión de nuestro modelo en los ambientes en donde se ejecuta?
 - ¿Que tan riesgoso es introducir una nueva versión del modelo?

.. warning:: Reentrenamiento del modelo hace referencia al caso donde necesitamos disparar el proceso de entrenamiento bajo un conjunto de datos actualizado. Esto no incluye los casos donde el esquema de los datos haya cambiado, o necesitamos actualizar versiones de librerias, sistemas operativos, etc. Si bien en estos casos también sucederá un reentrenamiento del modelo, muchas otras partes del proceso también deberán dispararse como ser: documentación, análisis de dependencias, análisis de performance, etc.

Ambiente de reentrenamiento
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Una vez que hemos identificado la necesidad de reentrenar un modelo productivo, una pregunta que nos podría sugir es *¿en qué ambiente debería suceder esto? ¿en desarrollo o en producción?*. 

La idea de que este reentrenamiento suceda en desarrollo está fundada en que construiremos una nueva versión del modelo de aprendizaje automático, y esta versión debe fluir desde desarrollo hasta producción pasando por cada uno de sus ambientes. Adicionalmente, quisieramos reutilizar todo el procedimiento que en un comienzo le dió vida a la primera versión del modelo.

Por otro lado, la idea de que este reentrenamiento suceda en producción está fundada en que el modelo se encuentra productivo y este reentrenamiento solo busca actualizar el *conocimiento* con los datos más frescos. Adicionalmente, no queremos que los desarrolladores tengan control para introducir nuevos cambios, nuevas arquitecturas o cualquier otra modificación que quizás requiera otro tipo de análisis que demore la publicación del modelo. Piense en el caso de un modelo de aprendizaje que quizás se reentrena con nuevos datos de forma diaria.

La respuesta a la pregunta dependerá de la organización en la que estemos trabajando y la naturaleza del problema. En general, el reentrenamiento sucede en producción cuando:
 - La frecuencia de entrenamiento es alta.
 - Se dispone de un procedimiento automático para el reentrenamiento del modelo, validación, despliegue y liberación. Vea :doc:`../../../projects/mlops/cicd` para más detalles de los requerimientos para implementar este tipo de automatizaciones.
 - La :doc:`../validation/riskmodel` esta bien definida e identifica un bajo riesgo para el despliegue del modelo de forma automática.
 - Cuestiones de seguridad de datos hacen más sencillo implementar este proceso en producción que en desarrollo, donde los desarrolladores no tienen acceso al modelo.

El reentrenamiento sucede en desarrollo cuando:
 - La frecunecia de entrenamiento es baja.
 - Como parte del reentrenamiento, es necesario actualizar versiones de librerias, paquetes o sistemas operativos o el esquema de datos a cambiado.
 - El proceso de publicación no está automátizado y se requiere intervención de los desarrolladores.
 - La :doc:`../validation/riskmodel` identifica un alto riesgo y complejos procesos de validación deben ponerse en juego para lograr que el modelo sea publicado.


Aprendizaje en linea
^^^^^^^^^^^^^^^^^^^^
El concepto de reentrenamiento no aplica de igual forma a todos los tipos de algoritmos de aprendizaje automático, y este es el caso de `Aprendizaje en linea` u `Online learning`. Se trata de un método en el cual las muestras de datos se presentan al modelo de forma secuencial, en un determinado orden, y donde cada muestra que el modelo vé actualiza su estado para las subsecuentes predicciones futuras [1]_. Como opuesto, las técnicas por lotes generan el mejor predictor al aprender desde el conjunto de datos entero de una sola vez (o en mini-batches). `Online learning` es una técnica que comunmente se utiliza cuando no es viable el entrenamiento del modelo sobre el set de datos completo (datos que se consumen vía streaming por ejemplo), donde es necesario que el modelo se adapte dinámicamente a los nuevos datos o cuando los datos per-se son una función que depende del tiempo (la predicción del valor de un stock por ejemplo).

.. note:: Los modelos de aprendizaje en linea ofrecen sus propios desafíos y están fuera del alcance explorarlos en detalle, aunque los abordaremos desde un punto de vista de su implementación en organizaciones.

Los modelos de aprendizaje en linea, por su definición, no poseen el concepto de reentrenamiento, lo cual resulta atractivo. Sin embargo, también introducen sus propios desafíos. En primer lugar, el orden en que los datos son presentados al modelo tiene un efecto ya que altera todas las prediciones futuras que el mismo hará. Implementar validaciones es también desafiante ya que una vez que un modelo vió una determinada muestra, no es trivial volver al estado anterior. Finalmente, estos métodos pueden sufrir de `catastrophic inference` [2]_ por lo que en general, en el contexto de una organización se implementa un método con el mismo espíritu, aunque más controlado, que se conoce como `Incremental learning`.

Aprendizaje incremental
^^^^^^^^^^^^^^^^^^^^^^^
Aprendizaje incremental o `incremental learning` [3]_ [4]_ es un método de aprendizaje automático en el cual las muestras de datos son constantemente, e incrementalmente, consideradas para extender el conocimiento del modelo. Es una técnica de aprendizaje dinámico que ingesta nuevos conjuntos de datos a medida que se encuentran disponible para actualizar el modelo, pero sin *olvidar* el conocimiento anterior. Muchos algoritmos implementan este tipo de aprendizaje mientras que otros pueden ser fácilmente adaptados.

Al igual que los modelos de `Aprendizaje en linea`_, estos modelos son de especial interes en situaciones donde el conjunto de datos es demasiado grande para entrenar el modelo de una sola vez (ya sea porque los datos no caben en memoria o por restricciones de infraestructura) o en situaciones donde el conjunto de datos se ingesta vía `streaming`. Ejemplos típicos de su uso puede ser la creación de perfiles de usuarios.

En general, los modelos que utilizan aprendizaje incremental conservan el concepto de reentrenamiento, aunque en este caso el modelo con el que se comienza no es un modelo sin entrenar, sino que su versión anterior. Dentro de las dependencias que se identifican en el modelo, se deberá incluir la versión anterior del modelo ya que aquí, el orden en que se realizan los reentrenamientos importa.


.. [1] `Online machine learning, Wikipedia <https://en.wikipedia.org/wiki/Online_machine_learning>`_
.. [2] `Catastrophic inference, Wikipedia <https://en.wikipedia.org/wiki/Catastrophic_interference>`_
.. [3] `Incremental learning, Wikipedia <https://en.wikipedia.org/wiki/Incremental_learning>`_
.. [4] `Brief Introduction to Streaming data and Incremental Algorithms <https://blog.bigml.com/2013/03/12/machine-learning-from-streaming-data-two-problems-two-solutions-two-concerns-and-two-lessons/>`_