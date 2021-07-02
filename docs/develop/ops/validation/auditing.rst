================================
Reproducibilidad y auditabilidad
================================

Reproducibilidad se refiere a la habilidad de poder recrear exactamente el mismo modelo que se está considerando. La misma requiere que el modelo esté correctamente documentado, que los datos utilizados para su entrenamiento estén disponibles en su misma forma que se encontraron cuando se entrenó (vea :ref:`rst_dataset_versioning` ), y toda la especificación de los requerimientos de software para recrear el ambiente en el que fue entrenado. Reproducibilidad es una propiedad escencial no solo para poder replicar los resultados que se encontraron durante desarrollo, pero también considerando implicaciones de alta disponibilidad y recuperación ante desastres del servicio del del modelo. 

Auditabilidad
-------------

La auditabilidad de un modelo está relacionada con la Reproducibilidad, pero agrega otros requerimientos. Para que un modelo sea auditable, es necesario que se pueda acceder a todo el historial del modelo que está desplegado en producción y **de todas sus versiones anteriores**. Esto incluye:

:Documentación: La documentación del modelo.
:Modelo: Esto incluye todos los elementos que componen el modelo, siendo la rutina de entrenamiento, la rutina de inferencia, liberias utilizadas junto con todas sus versiones especificadas, el modelo generado y persistido.
:Conjunto de datos: TODO
:Pruebas de calidad: TODO
:Explicaciones: La auditabilidad debe también poder ofrecer un entendimiento de cada una de las partes del sistema, incluyendo explicaciones de por qué el modelo se comporta de la manera que se comporta. Si bien la interpretación de modelos de aprendizaje automático es un área de investigación que requiere extenso entrenamiento y capacitación, se deberá disponer de informes de interpretabilidad para que una audiencia más amplia pueda comprenderlos.
:Metricas: TODO

Si bien no todas las organizaciones tienen requerimientos de auditabilidad, es fácil ver las ventajas que ofrece para cualquier organización desde un punto de vista de observabilidad de la operación.

Herramientas
------------

En general, las organizaciones implementan herramientas específicas que posibilitan el rastreo y versionamiento de todos los modelos de aprendizaje automático junto con toda su metadata. Algunas herramientas son de código abierto, como `MLFlow <https://mlflow.org/>`_ , otras se ofrecen como servicios gratuitos como ser `Weights & Biases <https://wandb.ai/site>`_ , mientras que otras son provistas bajo alguna modalidad de pago por uso como ser `Azure Machine Learning Services <https://azure.microsoft.com/en-us/services/machine-learning/>`_ , `AWS SageMaker <https://aws.amazon.com/sagemaker/>`_ o `GCP Vertex <https://cloud.google.com/vertex-ai>`_ .


