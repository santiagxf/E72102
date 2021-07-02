.. _rst_model_validation:

=====================
Validación del modelo
=====================
En sistemas complejos, introducir un modelo de aprendizaje automático puede tener consecuencias importantes en los procesos de negocio de la organización, dificiles de cuantificar. En el diseño de software convencional, cuando un sistema se desvia del comportamiento deseado, en general buscaremos las lineas de código que están causando este comportamiento para luego ser correjido. Sin embargo, en sistemas basados en modelos de aprendizaje automático, no tenemos *una linea de código* para cambiar. Incluso determinar *que tan bien y que tan mal* un modelo se comporta puede ser desafiante. Es importante poder anticipar los riesgos que conlleva un modelo en producción y mitigarlos. Esto incluye contemplar malfuncionamientos y ataques maliciosos.

En general, deveríamos de preguntarnos:
 - ¿Qué sucedería si el modelo funciona de la peor forma posible?
 - ¿Qué sucedería si usuarios mal intencionados pueden obtener los datos de entrenamiento o la lógica con la que funciona el modelo?
 - ¿Cuales son los riesgos financieros, de negocio, legales y de reputación asociados?

En la mayoría de las organizaciones, el equipo que realiza la validación del modelo es distinto que al equipo que lo desarrolló y por lo tanto es importante que los mismos tengan suficiente entreamiento en las tecnologías de aprendizaje automático para poder entender los riesgos e implementar las validaciones apropiadas que ayuden a alcanzar un despliegue exitoso.


.. toctree::
    :maxdepth: 2
    :caption: En esta sección
    
    Modelo de riesgo <riskmodel>
    Control de calidad <testing>
    Reproducibilidad y auditabilidad <auditing>
    Seguridad <security>
    Vinculación de datos en inferencia <augmentation>