.. _rst_online_evaluation:

===================
Evaluación en linea
===================

Valores verdadedores (ground truth)
-----------------------------------
Los valores verdaderos (o ground truth) es simplemente la respuesta correcta a la pregunta de negocio que el modelo se suponia que debía responder. Por ejemplo, si estamos diseñando un modelo que predice si un cliente debería recibir o no un correo electrónico promocional, el valor verdadero para el modelo sería si finalmente el usuario tomó la promoción que le enviamos o no. Esta información es de mucho interes porque básicamente nos permite calcular que tan bueno o malo es nuestro modelo en resolver este problema de negocio en la realidad.

En algunos casos, obtener este valor verdadero de la predicción es muy rápido, por ejemplo, cuando mostramos una publicidad en un sitio web - si el usuario le hace click antes de irse de la página entonces la predicción será correcta y si no lo hace entonces será incorrecta. Por el contrario, en otros procesos de negocio podría tomar tiempo determinar cual es el valor correcto. Este es el caso de un sistema de detección de fraudes por ejemplo, donde podría tomar meses antes de saber si la transacción es efectivamente fraudulenta o no.

En los casos donde la valores verdaderos de la variable objetivo no están disponibles, una alternativa para la evalución en linea es la evaluación de desviaciones covariable. Vea :ref:`rst_covariate_shift`

.. note:: La evaluación via desviaciones covariables se basa en el principio de que el modelo solo performará correctamente si los datos con los que fué entrenado (muestra) reflejan correctamente el comportamiento y valores en el mundo real (población). Por lo tanto, si una comparación entre los datos que se utilizaron durante el entrenamiento y los datos que el modelo ve en producción arrojan diferencias, entonces tenemos evidencia para sostener la idea que el modelo no performará bien.

Si bien esta alternativa nos permite detectar desviaciones, la solución a este problema no es tan sencilla de implementar. Al no disponer de los valores verdaderos en la variable objetivo, reentrenar el modelo no es una opción en el corto plazo. Intervención manual será requerida en este caso ya que es necesario identificar los factores que están causando la desviación en los datos de entrada. Los desarroladores del modelo pueden evaluar la situación y aplicar técnicas para corregirlo incluyendo eliminar algunos predictores o cambiar la estrategia de muestreo (resampling). Aquí es donde se vuelve piramidal la estrategia de :ref:`rst_alerts` 
