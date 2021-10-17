==================
Equipos y personas
==================

Roles
-----
Cuando llevamos adelante un proyecto basado en datos, es necesario identificar los siguientes roles. Note que no siempre todos los roles están instanciados en personas distintas siendo muchos casos donde una persona ejecuta más de uno. En general, esto dependerá del tamaño de la organización y de su madurez/estructura.

Experto de negocio (SME)
^^^^^^^^^^^^^^^^^^^^^^^^
El experto de negocio, también llamado Subject Matter Expert o SME, es la persona que tiene el conocimiento práctico sobre la problematica que se quiere resolver y quien puede no solo reconocer el valor para la organización del problema que se quiere resolver sino que también puede verificar cuando una solución es aceptable. Entre las responsabilidades del rol está:

- Provee las preguntas de negocio, objetivos, KPI y las métricas sobre las cuales los modelos de aprendizaje automático deben ser diseñados.
- Evalúa constantemente que la performance del modelo está alineada (resuelve) la necesidad de negocio inicial.

Cientifico de datos
^^^^^^^^^^^^^^^^^^^
Son quienes construyen modelos de aprendizaje automático que solucionan el problema de negocio (hipótesis). En general:

- Generan entregables que pueden ser desplegados en ambientes productivos.
- Evalúan la performance del modelo (en conjunto con las métricas definidas por el experto de negocio) para asegurarse que se resuelve la problemática de negocio.
- Desarrollan test para asegurar la performance de los modelos.

Ingeniero de datos
^^^^^^^^^^^^^^^^^^
Este rol, mayoritariamente técnico, define los procesos de consumo, integración y uso de datos para los modelos de aprendizaje automático. En general:

- Definen los procesos de transformación de datos.
- Monitorean la integración continua de datos en la plataforma.

Arquitecto de Datos
^^^^^^^^^^^^^^^^^^^
Se trata de un rol técnico, pero con una visión mas macro del **data state** de una organización. Este rol define las técnologías, procesos y prácticas que se utilizarán en la organización para instanciar cualquier sistema que instancie o consuma datos.

- Asegura una plataforma escalable y flexible para el desarrollo de proyectos basados en datos.
- Definen las técnologias, interfaces y metodologías sobre las que la organización instanciará sus datos.
- Introduce e integra nuevas tecnologías a la plataforma cuando las mismas mejoran la performance o capacidades.

Arquitecto de Aprendizaje Automático 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- Asegura una plataforma escalable y flexible para el desarrollo del ciclo de vida completo de modelos de aprendizaje automático, desde su desarrollo hasta su productivización, incluyendo su monitoreo.
- Introduce e integra nuevas tecnologías a la plataforma cuando las mismas mejoran la performance o capacidades.
- Utilizan tableros de control con los recursos utilizados por los diferentes modelos y herramientas de monitoreo para identificar problemas y diagnosticar fallas en pipelines; con el objetivo de ajustar la infraestructura.

Ingeniero de Operaciones
^^^^^^^^^^^^^^^^^^^^^^^^
Este rol colabora con el Arquitecto de Aprendizaje Automático, Ingenieros de Datos y Científicos de Datos para construir sistemas que puedan operacionalizar la puesta en producción del modelo.

- Construyen los sistemas operacionales donde se construyen y despliegan los modelos, así como también asegurar su performance, seguridad y disponibilidad.
- Son responsables de los pipelines de Integración Continua/Despliegue Continuo.

Ingeniero de software
^^^^^^^^^^^^^^^^^^^^^

- Integra los modelos de aprendizaje automático en los sistemas transaccionales y aplicaciones de la organización.
- Asegura la compatibilidad de los modelos con otras piezas de software que no están basadas en aprendizaje automático.
- Asiste en el versionamiento y test automático.

Auditor/Gerente de riesgos
^^^^^^^^^^^^^^^^^^^^^^^^^^

- Evalúa y minimiza el riesgo de la compañía como resultado del despliegue de un modelo de aprendizaje automático en producción.
- Asegura el cumplimiento con normativas y regulaciones internas y externas antes del despliegue de un modelo de aprendizaje automático en producción

.. note:: Realizan su trabajo utilizando herramientas de reportería que incluyen todos los modelos de aprendizaje automático (actuales y anteriores) incluyendo su linaje.


