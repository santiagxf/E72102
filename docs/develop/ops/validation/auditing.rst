================================
Reproducibilidad y auditabilidad
================================

La reproducibilidad y auditabilidad de un modelo de aprendizaje automático están relacionadas entre si, pero suponen alcances distintos a la hora de implementarlas.

Reproducibilidad
----------------

Reproducibilidad se refiere a la habilidad de poder recrear exactamente el mismo modelo que se está considerando. La misma requiere que el modelo esté correctamente documentado, que los datos utilizados para su entrenamiento estén disponibles en su misma forma que se encontraron cuando se entrenó (vea :ref:`rst_dataset_versioning` ), y toda la especificación de los requerimientos de software para recrear el ambiente en el que fue entrenado. Reproducibilidad es una propiedad escencial no solo para poder replicar los resultados que se encontraron durante desarrollo, pero también considerando implicaciones de alta disponibilidad y recuperación ante desastres del servicio del del modelo. 

.. _rst_auditability:

Auditabilidad
-------------

La auditabilidad de un modelo está relacionada con la Reproducibilidad, pero agrega otros requerimientos. Para que un modelo sea auditable, es necesario que se pueda acceder a todo el historial del modelo que está desplegado en producción y **de todas sus versiones anteriores**. Esto incluye:

:Documentación: El equipo de desarrollo debe ofrecer detallada documentación sobre el modelo de tal forma que persona fuera del equipo pueda entender como el modelo opera, identificar sus suposiciones claves y limitaciones asi como tambien ser capaz de replicar los resultados que se reportaron. Esto incluye los casos en donde el modelo ha sido adquirido a un proveedor.
:Modelo: Esto incluye todos los elementos que componen el modelo, siendo la rutina de entrenamiento, la rutina de inferencia, liberias utilizadas junto con todas sus versiones especificadas, el modelo generado y persistido. También incluye debe indicar cualquier dependencia que tenga con otro modelo de aprendizaje automático.
:Conjunto de datos: Cada uno de los conjuntos de datos utilizados para entrenar y validar el modelo deben de ser referenciados de forma única. Los datos deben estar acompañados por evaluaciones de calidad y relevancia. En el caso de que el conjunto de datos no sea 100% representativo, es importante que se documenten estas suposiciones para hacer evitente las limitaciones del modelo.
:Pruebas de calidad: Un correcto control de calidad debe ser ejecutado para asegurar la robustes y estabilidad del modelo en el tiempo y a lo largo de diferentes condiciones de ejecución. Tanto las rutinas como los resultados de las mismas deben ser documentadas.
:Explicaciones: La auditabilidad debe también poder ofrecer un entendimiento de cada una de las partes del sistema, incluyendo explicaciones de por qué el modelo se comporta de la manera que se comporta. Si bien la interpretación de modelos de aprendizaje automático es un área de investigación que requiere extenso entrenamiento y capacitación, se deberá disponer de informes de interpretabilidad para que una audiencia más amplia pueda comprenderlos. Vea :doc:`interpretation/intro`.
:Metricas: TODO

Si bien no todas las organizaciones tienen requerimientos de auditabilidad, es fácil ver las ventajas que ofrece para cualquier organización desde un punto de vista de observabilidad de la operación.

.. important:: En entidades reguladas, en general existe una división interna de la organización que debe ser responsable por el mantenimiento del inventario de todos los modelos dentro de la organización. Esto incluye modelos *implementados y en uso*, *en desarrollo* y *recientemente comisionados*.

Herramientas
------------

En general, las organizaciones implementan herramientas específicas que posibilitan el rastreo y versionamiento de todos los modelos de aprendizaje automático junto con toda su metadata. Algunas herramientas son de código abierto, como `MLFlow <https://mlflow.org/>`_ , otras se ofrecen como servicios gratuitos como ser `Weights & Biases <https://wandb.ai/site>`_ , mientras que otras son provistas bajo alguna modalidad de pago por uso como ser `Azure Machine Learning Services <https://azure.microsoft.com/en-us/services/machine-learning/>`_ , `AWS SageMaker <https://aws.amazon.com/sagemaker/>`_ o `GCP Vertex <https://cloud.google.com/vertex-ai>`_ .


