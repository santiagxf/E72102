.. _rst_model_validation:

=====================
Validación del modelo
=====================
En sistemas complejos, introducir un modelo de aprendizaje automático puede tener consecuencias importantes en los procesos de negocio de la organización, dificiles de cuantificar. En el diseño de software convencional, si un sistema se desvía del comportamiento deseado o esperado, en general es posible buscar la/las lineas de código que están generando esta desviación y correjilas. Sin embargo, en sistemas basados en aprendizaje automático, no tenemos *una linea de código* para cambiar. Incluso determinar *que tan bien y que tan mal* un modelo se comporta puede ser desafiante. Es importante poder anticipar los riesgos que conlleva un modelo en producción y mitigarlos. Esto incluye contemplar malfuncionamientos y ataques maliciosos. 

En general, deveríamos de preguntarnos:
 - ¿Qué sucedería si el modelo funciona de la peor forma posible?
 - ¿Qué sucedería si usuarios mal intencionados pueden obtener los datos de entrenamiento o la lógica con la que funciona el modelo?
 - ¿Cuales son los riesgos financieros, de negocio, legales y de reputación asociados?

Un proceso de validación correcto debería:
 #. Calificar los riesgos asociados al depliegue y cuantificar sus magnitides.
 #. Cuantificar los recursos necesarios para operar el modelo.
 #. Asegurarse que el modelo cumple con los requisitos mínimos de cálidad de la organización.
 #. Identificar los requerimientos de seguridad, reproducibilidad y auditoria.

Industrias reguladas puede requerir que el equipo que realiza la validación del modelo sea distinto al equipo que lo desarrolló. Por lo tanto, es importante que los mismos tengan suficiente entreamiento en las tecnologías de aprendizaje automático para poder entender los riesgos e implementar las validaciones apropiadas que ayuden a alcanzar un despliegue exitoso.

.. note:: En aquellas organizaciones no reguladas, es bastante común encontrar que estas validaciones son realizadas por los mismos equipos que desarrollan los modelos. Par asegurar que no existen sezgos, el proceso de validación debe ser diseñado por el equipo de arquitectura de datos. 

.. toctree::
    :maxdepth: 2
    :caption: En esta sección
    :hidden:
    
    Modelo de riesgo <riskmodel>
    Control de calidad <testing>
    Reproducibilidad y auditabilidad <auditing>
    Seguridad <security>