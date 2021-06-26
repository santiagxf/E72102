.. _rst_model_validation:

=====================
Validación del modelo
=====================
En sistemas complejos, introducir un modelo de aprendizaje automático puede tener consecuencias importantes en los procesos de negocio de la organización, dificiles de cuantificar. Es importante poder anticipar los riesgos que conlleva un modelo en producción y mitigarlos. Esto incluye contemplar malfuncionamientos y ataques maliciosos.

En general, deveriaos de preguntarnos:
 - ¿Que sucedería si el modelo funciona de la peor forma posible?
 - ¿Que sucedería si usuarios mal intencionados pueden obtener los datos de entrenamiento o la lógica con la que funciona el modelo?
 - ¿Cuales son los riesgos financieros, de negocio, legales y de reputación asociados?

.. toctree::
    :maxdepth: 2
    :caption: En esta sección
    
    Modelo de riesgo <riskmodel>
    Control de calidad <testing>
    Reproducibilidad y auditabilidad <auditing>
    Seguridad <security>
    Aumento de datos en inferencia <augmentation>