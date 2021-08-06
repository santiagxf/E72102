CI/CD
=====

CI/CD o *integración continua, despliegue continuo* (continuous integration, continuous delivery) hace referencia a la práctica integración y despliegue continuo de soluciones de software en diferentes ambientes. Tiene como objetivo la entrega rápida, confiable y repitible de soluciones de software al negocio. Esto se logra a traves de la automátización del proceso que permite integrar las contribuciones que hacen todos los integrates del equipo de forma más fluida e institucionalizar procesos de control de calidad que detectan los errores de forma temprana. Es una práctica que se ha aplicado tradicionalmente a sistemas de software pero que aplica igualmente a sistemas basados en aprendizaje automático.

La automtización que propone CI/CD no solo tiene como objetivo el aumentar la velocidad y eliminar tareas repetitivas, sino que, más importante aun, el alentar a los equipos de desarrollo a desplegar y entregar con mayor frecuencia. 

Existen 4 procesos intrínsecos en CI/CD que se suceden secuencialmente: Integración (Integration) -> Entrega (Delivery) -> Despliegue (Deployment) -> Liberación (Release):

:Integración: Se refiere al proceso en donde la contribuciones (modificaciones) que cada uno de los integrantes del equipo realiza al proyecto se combinan con el respositorio central de código. En general, este proceso se lo conoce como *merge*.
:Entrega: Se refiere al proceso de empaquetar la solución de aprendizaje automático junto a todas sus dependencias para su posterior despliegue en algún ambiente de destino (ya sea un ambiente de calidad, integración, producción, etc).
:Despliegue: Se refiere al proceso de instalar una solución previamente empaquetada en su infraestructura final.
:Liberación: Se refiere al acceso por parte de los usuarios a la funcionalidad en particular.

La automatización de estos 4 subprocesos es una cuestión tanto técnica como de negocio, y es cuando los mismos ganan el adjetivo de *continuo o continua*. En muchos casos la automatización de punta a punta prodría no ser algo que el negocio necesite. Sin embargo, la automátización de alguno podría dictar la automatización de otros. Por ejemplo, no podremos implementar *Despliegue continuo* si no tenemos *Entrega continua*. 

.. note:: A principio podría parecer que **Despliegue** y **Liberación** son dos procesos que suceden al mismo tiempo. Sin embargo, como se vió en :doc:`../../develop/ops/deployment/deployment`, existen casos donde estamos interesados en que los mismos suceden en tiempos distintos.

Componentes
-----------
Al tratarse de una práctica, debe ser adaptada dependiendo de las necesidades de la organización, del equipo y de la naturaleza del negocio en el que operan. En general, es muy útil implementar un acercamiento incremental al concepto, es decir, es preferible comenzar con un flujo de trabajo sencillo pero que funcione y que le permita a los equipos iterar rápidamente, en lugar de comenzar con una implementación compleja que incluso demande una infraestructura grande.

En general encontraremos los siguientes componentes:

Sistema de control de versiones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Un sistema de control de versiones permite que todos los integrantes de un equipo puedan colaborar en un repositorio centralizado de código, mientras se mantiene un registro de los cambios que cada uno realiza. Permite el control de qué y cómo se introducen cambios al repositorio así como también habilita formas de deshacer cambios que no resultaron. En general, el sistema de control de cambios más conocido es Git, y es cada vez más adoptado por la comunidad de ciencia de datos.

A pesar de que Git es ampliamente utilizado para versionamiento de código, no ofrece demasiadas virtudes para versionamiento de otros elementos comunes en los sistemas de aprendizaje automático, como ser datos y modelos. En general, estos elementos se los conoce como artefactos en el contexto de CI/CD, o *ML Artifacts*.

Los artefactos que deberían estar bajo control de versiones (expresión también conocida como *source control*) son:
 - Código para el preprocesamiento de datos.
 - Código para la ejecución del modelo.
 - Hiperparámetros y configuraciones.
 - Datos de entrenamiento y validación.
 - Modelo de aprendizaje entrenado.
 - Ambiente o especificación del ambiente en donde se puede ejecutar el modelo, incluyendo librerias, versiones, variables del entorno, etc.
 - Documentación.
 - Código para la ejecución de pruebas unitarias.

.. note:: La lista completa de artefactos que deberían estar bajo control de versiones depende de las necesidades de :doc:`../../develop/ops/validation/auditing`

Sistema de entrega continua
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Entrega continua es una práctica donde los equipos entregan los desarrollos a producción directamente con cada *check-in* que el equipo genera de forma automática (en realidad, con cada `merge` a la rama `master`).

Uno de los sitemas de integración continua más conocidos es Jenkins, un potente sistema de entrega continua que permite la implementación de flujos de trabajo de CI/CD independientemente del lenguaje de programación, las soluciones de testeo y la infraestructura donde se opera. 

Diseño
------
En aquellas organizaciones donde hay un gran número de modelos en desarrollo, existen posibilidades de que cada uno de estos modelos tengan requerimientos de automatización distintos. Es imperativo disponer de un diseño flexible que impida que cada equipo tenga que terminar construyendo sus propios flujos de CI/CD para cada modelo, principalmente debido a:
 - Gobierno suboptimo.
 - Mantenimiento de cada una de las implementaciones.
 - Diferentes implementaciones pueden tener diferentes prácticas y patrones.


