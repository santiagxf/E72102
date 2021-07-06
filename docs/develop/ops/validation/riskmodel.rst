================
Modelo de riesgo
================

Como mencionamos, un correcto proceso de validación debe calificar los riesgos asociados al depliegue y cuantificar sus magnitides. Estas cuantificaciones son utilizadas para implementar un efectivo modelo de gobierno, políticas, procedimientos y controles para asegurar que los riesgos son minimizados. 

¿Que es un riesgo?
------------------
Un riesgo es una perdida potencial en la que una organización podría incurrir al tomar decisiones, de forma parcial o total, basadas en la salida de un modelo de aprendizaje automático; perdidas asociadas a errores de desarrollo, implementación o uso de tales modelos.

Responsabilidades de la alta gerencia
-------------------------------------
Es responsabilidad de la gerencia de datos el establecer un framework para la administración del riesgo de los modelos de aprendizaje automático. Tal framework debe estar documentado de forma apropiada. Sin embargo, son los propietarios del producto responsable finalmente por la ejecución y mantenimiento de este framwork asi como también de la designación de roles y responsabilidades. Los propietarios deben poder entender las capacidades del modelo, sus limitaciones y el potencial impacto relacionado con la incertidumbre del modelo que es quantificada mediante pruebas de calidad. Esto hace extremadamente importante que los resultados de la fase de validación estén en un formato que la gerencia pueda interpretar. Vea las secciones :ref:`rst_auditability` e :doc:`interpretation/intro` para mas detalle como asegurar que la alta gerencia pueda interpretar los resultados de los modelos.

Técnicas para la estimación del riesgo
--------------------------------------
No existe una forma estandar para estimar el riesgo de un modelo de aprendizaje automático. Cada organización puede tener un modelo de riesgo distinto que incluso esté afectado por el dominio en el que opera o la industria en los casos en los que esté regulada. Dos ejemplos de modelos de riesgos son Matriz de costos y Failure Modes and Effects Analysis (FMEA).

Matríz de costos
^^^^^^^^^^^^^^^^
La matríz de costos permite a los equipos de proyecto evaluar el costo promedio de operar un modelo de aprendizaje automático comparado contra su contrapartida ideal (un modelo perfecto - aunque imposible).

Aunque calcular este costo resulte muy importante, es crítico entender que su quantificación puede resultar ordenes de magnitud fuera de su valor verdadero. En algunas organizaciones, el riesgo podría resultar en una responsabilidad legal que conlleve a un riesgo financiero, comprometa la seguridad de las personas o posibilite una nueva amenaza de seguridad para la organización.

Las siguientes consideraciones impactan un modelo de riesgo:
 - Errores de programación, errores en el diseño, entrenamiento o evaluación del modelo.
 - Errores de programación en el post-procesamiento de la salida del modelo.
 - Incompatibilidad entre el modelo y su entorno de ejecución.
 - Mala calidad en los datos de entrenamiento.
 - Mala representación de los datos de producción en los datos de entrenamiento.
 - Uso incorrecto del modelo por mala interpretación de su salida.
 - Ataques adversarios
 - Riesgos de reputación debido a sezgo en el modelo o el uso antiético de la tecnología de aprendizaje automático.

Estos riesgos, a su vez, pueden aplificarse por:
 - Amplia utilización del modelo en la organización.
 - Amplia superficie de despliegue: Cuanto más grande es la cantidad de ubicaciones en las que se despliega un modelo, más alto será el riesgo.
 - Despliegue del modelo en ambientes que cambian frecuentemente: Esto puede representar un problema especialmente en sistemas que cambian tan rapidamente que los sistemas de alerta y monitoreo no logran emitir una advertencia a tiempo. Incluso, esta frecuencia de cambios podría modificar las condiciones de ejecución solo *ligamente* lo cual, si bien no representaría un problema grave que se debe resolver inmediatamente, el modelo nunca termina ejecutandose en sus condiciones normales o esperadas.
 - Complejas interacciones entre diferentes modelos: Probablemente son una de las condiciones más complejas a la hora de evaluar el riesgo. En algunos casos las interacciones pueden ser directas y evidentes, como ser que la salida de un modelo es consumida como un predictor de otro modelo. Incluso podria ser que la salida de un modelo representa los datos de entrenamiento de otro modelo. Sin embargo, este podría no ser siempre el caso y tener modelos que interactuan entre si en procesos de negocio donde incluso la ineración sucede a traves de personas.

Failure Modes and Effects Analysis (FMEA)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Mitigación del riesgo
---------------------

======================================  ==================================
Riesgo                                  Mitigación
======================================  ==================================
Amplia superficie de despliegue         :ref:`rst_canary_releases`
Amplia utilización del modelo           | :ref:`rst_canary_releases`
                                        | :ref:`rst_progressive_rollouts`
Complejas interacciones entre modelos   None
Ambientes que cambian frecuentemente    | :ref:`rst_mlops`
                                        | :ref:`rst_blue_green_deployment`
======================================  ==================================



Referencias:
`PRA’s 4 Key Principles of Model Risk Management <https://www.sas.com/content/dam/SAS/en_gb/doc/whitepaper1/4-key-principles-model-risk-management.pdf>`_
`Stress Test Model Management — Bank of England <https://www.bankofengland.co.uk/-/media/boe/files/prudential-regulation/letter/2017/stress-test-model-management.pdf?la=en&hash=0B16C05C121B299D8FC3ACB600D52FF9D8A3154A>`_

