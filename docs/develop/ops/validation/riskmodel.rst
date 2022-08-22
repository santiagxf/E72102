================
Modelo de riesgo
================

Como mencionamos, un correcto proceso de validación debe calificar los riesgos asociados al depliegue y cuantificar sus magnitudes. Estas cuantificaciones son utilizadas para implementar un modelo de gobierno, políticas, procedimientos y controles efectivos para asegurar que los riesgos son minimizados. 

¿Que es un riesgo? [1]_
-----------------------
Un riesgo es una perdida potencial en la que una organización podría incurrir al tomar decisiones, de forma parcial o total, basadas en la salida de un modelo de aprendizaje automático; perdidas asociadas a errores de desarrollo, implementación o uso de tales modelos.

Responsabilidades de la alta gerencia [2]_
------------------------------------------
Es responsabilidad de la gerencia de datos el establecer un marco de trabajo para la administración del riesgo de los modelos de aprendizaje automático. Tal marco debe estar documentado de forma apropiada. Sin embargo, finalmente son los propietarios del producto responsables por la ejecución y mantenimiento de este marco de trabajo asi como también de la designación de roles y responsabilidades. Los propietarios deben poder entender las capacidades del modelo, sus limitaciones y el potencial impacto relacionado con la incertidumbre del modelo, la cual debería ser quantificada mediante pruebas de calidad. Esto hace extremadamente importante que los resultados de la fase de validación estén en un formato que la gerencia pueda interpretar. Vea las secciones :ref:`rst_auditability` e :doc:`../interpret/intro` para más detalle cómo asegurar que la alta gerencia pueda interpretar los resultados de los modelos.

Técnicas para la estimación del riesgo
--------------------------------------
No existe una forma estandar para estimar el riesgo de un modelo de aprendizaje automático. Cada organización puede tener un modelo de riesgo distinto que incluso esté afectado por el dominio o, en los casos en los que esté regulada, la industria en el que la misma opera. 

Un modelo de riesgos debería de considerar:
 - Errores de programación, en el diseño, de entrenamiento o en la evaluación del modelo.
 - Errores de programación en las rutinas de post-procesamiento de la salida del modelo.
 - Incompatibilidad entre el modelo y su entorno de ejecución.
 - Mala calidad en los datos de entrenamiento.
 - Mala representación de los datos de producción en los datos de entrenamiento.
 - Uso incorrecto del modelo por mala interpretación de su salida.
 - Ataques adversarios. Vea :doc:`security`.
 - Riesgos de reputación debido a sesgo en el modelo o el uso antiético de la tecnología de aprendizaje automático.

Existen situaciones en las cuales un riesgo puede tener un impacto mucho mayor debido a la forma en la que se consumo el modelo, el alcance del despliegue o incluso si sus efectos impactan en otros procesos de negocio.

Los riesgos deben ser amplificados cuando existe:
 - Amplia utilización del modelo en la organización.
 - Amplia superficie de despliegue: Cuanto más grande es la cantidad de ubicaciones en las que se despliega un modelo, más alto será el riesgo.
 - Despliegue del modelo en ambientes que cambian frecuentemente: Esto puede representar un problema especialmente en sistemas que cambian tan rápidamente que los sistemas de alerta y monitoreo no logran emitir una advertencia a tiempo. Incluso, esta frecuencia de cambios podría modificar las condiciones de ejecución solo *ligeramente* lo cual, si bien no representaría un problema grave que se debe resolver inmediatamente, el modelo nunca termina ejecutándose en sus condiciones normales o esperadas.
 - Complejas interacciones entre diferentes modelos: Probablemente son una de las condiciones más complejas a la hora de evaluar el riesgo. En algunos casos las interacciones pueden ser directas y evidentes, como ser que la salida de un modelo es consumida como un predictor de otro modelo. Incluso podría ser que la salida de un modelo representa los datos de entrenamiento de otro modelo. Sin embargo, este podría no ser siempre el caso y tener modelos que interactúan entre si en procesos de negocio donde incluso la interacción sucede a través de personas.


Analizaremos aquí dos ejemplos de modelos de riesgos, que son Matriz de costos y Failure Modes and Effects Analysis (FMEA).

Matríz de costos
^^^^^^^^^^^^^^^^
La matríz de costos permite a los equipos de proyecto evaluar el costo promedio de operar un modelo de aprendizaje automático comparado contra su contraparte ideal (un modelo perfecto - aunque imposible). Esta matriz ofrece adicionalmente una forma de diferenciar los distintos tipos de errores que un modelo puede cometer. 

Ejemplo
*******
Supongamos un problema de riesgo creditício en el cual implementamos un modelo de aprendizaje automático de clasificación que predice si el riesgo de crédito para una persona es *bueno* o *malo*. En este caso podriamos construir una matriz de costos de 2x2 de la siguiente forma:

+------------------------+------------+----------+----------+
|                                     | Valores del modelo  |
+=====================================+==========+==========+
|                                     | Bueno    | Malo     |
+------------------------+------------+----------+----------+
| **Valores verdaderos** | Bueno      | +100     | -100     |
|                        +------------+----------+----------+
|                        | Malo       | -500     | 0        |
+------------------------+------------+----------+----------+

Interpretación:
 En el ejemplo anterior, cada vez que el modelo realiza una predicción correcta la organización recibe un beneficio cuantificado en +100, mientras que rechazar un candidato cuando en realidad su riesgo de crédito era bajo (error de tipo I) tiene un costo de oportunidad de -100. Clasificar de forma correcta a aquellos que tienen una riesgo crediticio malo es neutral, mientras que incorractamente predecir a un candidato como bueno cuando en realidad es malo (error de tipo II) tiene un costo de -500 debido a pérdidas financieras asociadas.

Aunque calcular este costo resulte muy importante, es crítico entender que su quantificación puede resultar ordenes de magnitud fuera de su valor verdadero. En algunas organizaciones, el riesgo podría resultar en una responsabilidad legal que conlleve a un riesgo financiero, comprometa la seguridad de las personas o posibilite una nueva amenaza de seguridad para la organización.


Failure Modes and Effects Analysis (FMEA)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
También conocido como *potential failure modes and effect analysis*, se trata de un procedimiento para identificar todas las posibles fallas que se pueden dar durante un proceso de diseño, desarrollo o implementación de un producto o servicio [3]_ [4]_. Aqui:

:Failure modes,: significa las formas o modos en las que algo puede salir mal - es decir, que se puede dar una falla. Failures o *fallas* son cualquier tipo de error o defecto que afectan a un cliente, y que pueden ser potenciales o reales. Note que una falla puede tener multiples modos.
:Effect analysis,: hace referencia al estudio de las consecuencias de tales fallas.

Las fallas están priorizadas según qué tan severas son sus consecuencias, qué tan frecuentemente pueden ocurrir y qué tan fáciles son de detectar. El proposito de FMEA es el de tomar acciones que eliminen o reduzcan estas fallas, empezando por aquellas que tienen prioridades más altas.

.. important:: Si bien proponemos este método para la fase de validación, es importante entender que FMEA debe también ser utilizado durante la fase de diseño para prevenir fallas. Idealmente, FMEA comienza en las etapas más tempranas del desarrollo y continua a lo largo de todo el proceso de desarrollo del modelo de aprendizaje automático.

FMEA es un método que puede ser aplicado a cualquier disciplina, pero en el ámbito de aprendizaje automático, en general significa identificar qué tipo de errores puede cometer el modelo y cuáles son sus consecuencias. Una vez identificados, se deben cuantificar 3 factores:

- **Severidad (SEV):** La severidad de la falla, medida desde la perspectiva del cliente. Podríamos preguntarnos *¿Qué tan significativo es el impacto para los clientes si la falla ocurre?*
- **Ocurrencia (OCC):** La frecuencia con la cual la falla (real o potencial) puede o podría ocurrir. Podríamos preguntarnos *¿Qué tan frecuente ocurre o ocurriría esta falla debido a este modo?*
- **Detection (DET):** La probabilidad de que detectemos la falla antes de que afecte a algún cliente. Podríamos preguntarnos *¿Qué tan probable es que el sistema detecte la falla antes de que ocurra o cuando se hace presente? ¿Qué tan detectable es este modo?*

.. note:: FMEA es una técnica muy amplia y está fuera del alcance de este curso. Para un detalle más profundo sobre la misma puede revisar `Guide to Failure Mode and Effect Analysis – FMEA en el sitio de Juran <https://www.juran.com/blog/guide-to-failure-mode-and-effect-analysis-fmea/>`_.

Ejemplo
*******
Supongamos el mismo problema de riesgo crediticio que mencionamos anteriormente. Un análisis de FMEA podría ser:

+---------------------+-------------------+-------------------------------+-----+---------------------+-----+---------------------------------+-----+----+
| Area                | Modo de falla     | Efecto en el cliente          | SEV | Causas              | OCC | Mitigación                      | DET | RP |
+=====================+===================+===============================+=====+=====================+=====+=================================+=====+====+
| Datos de entrada    | Variables fuera   | Solicitud denegada            | 10  | Comportamiento      | 1   | :ref:`rst_testing_predictors`   | 1   | 1  |
|                     | de rango          | incorrectamente               |     | errático del modelo |     |                                 |     |    |
+---------------------+-------------------+-------------------------------+-----+---------------------+-----+---------------------------------+-----+----+
| Infraestructura     | Ambiente de       | Solicitud denegada            | 10  | Versiones de        | 8   | :ref:`rst_deployment_bg`        | 3   | 3  |
|                     | despliegue        | incorrectamente               |     | librerias           |     |                                 |     |    |
|                     | incorrecto        |                               |     | incorrectas         |     |                                 |     |    |
+---------------------+-------------------+-------------------------------+-----+---------------------+-----+---------------------------------+-----+----+
| Despliegue          | Modelo errático   | Solicitud denegada o          | 10  | Nueva versión del   | 5   | :ref:`rst_canary_releases`      | 5   | 5  |
|                     |                   | aprobada incorrectamente      |     | modelo              |     | :ref:`rst_ring_rollouts` |     |    |
+---------------------+-------------------+-------------------------------+-----+---------------------+-----+---------------------------------+-----+----+

Interpretación:
 En el ejemplo anterior se muestran un **análisis limitado** del caso de despliegue de un modelo de aprendizaje automático que clasifica solicitudes creditícias. Es importante notar como la columna de *Ocurrencia* y *Detección* cambian sus valores gracias a las técnicas de *Mitigación* y controles que se ponen en práctica. Por ejemplo, si el modelo es reentrenado frecuentemente y desplegado en producción, existen chances de que la nueva versión no funcione correctamente. Una forma de mitigar este riesgo es utilizando ténicas de despliegues controlados como ser :ref:`rst_canary_releases` y :ref:`rst_progressive_rollouts`. Vea a continuación diferentes técnicas que se suelen utilizar para mitigar distintos tipos de riesgos.


Mitigación del riesgo
---------------------
Introducir cambios en un proceso de negocio vía software siempre representará un riesgo. Sin embargo, hay formas de mitigar estos riesgos utilizando diferentes técnicas y controles que se pueden poner en práctica. Por ejemplo:

====================================================  ==================================
Riesgo                                                Mitigación
====================================================  ==================================
Modelos con una amplia superficie de despliegue         :ref:`rst_canary_releases`
Amplia utilización del modelo en la organización        | :ref:`rst_canary_releases`
                                                        | :ref:`rst_ring_rollouts`
Complejas interacciones entre modelos                   Test de regresión
Ambientes que cambian frecuentemente                    | :ref:`rst_mlops`
                                                        | :ref:`rst_deployment_bg`
====================================================  ==================================


Referencias:

.. [1] `Stress Test Model Management — Bank of England <https://www.bankofengland.co.uk/-/media/boe/files/prudential-regulation/letter/2017/stress-test-model-management.pdf?la=en&hash=0B16C05C121B299D8FC3ACB600D52FF9D8A3154A>`_
.. [2] `PRA’s 4 Key Principles of Model Risk Management <https://www.sas.com/content/dam/SAS/en_gb/doc/whitepaper1/4-key-principles-model-risk-management.pdf>`_
.. [3] `Failure mode and effects analysis (FMEA) - ASQ <https://asq.org/quality-resources/fmea>`_
.. [4] `Manufacturing Technology Committee – Risk Management Working Group. Failure Modes and Effects Analysis Guide <https://pqri.org/wp-content/uploads/2015/08/pdf/FMEA_Training_Guide.pdf>`_
