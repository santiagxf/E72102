================
Modelo de riesgo
================

Matríz de costos
----------------
La matríz de costos permite a los equipos de proyecto evaluar el costo promedio de operar un modelo de aprendizaje automático generado con datos vía validación crusada, comparado contra su contrapartida ideal (un modelo perfecto - aunque imposible).

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
 - Complejas interacciones entre diferentes modelos.
 - Despliegue del modelo en ambientes que cambian frecuentemente: Esto puede representar un problema especialmente en sistemas que cambian tan rapidamente que los sistemas de alerta y monitoreo no logran emitir evidencia a tiempo.

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





