==============
Versionamiento
==============

Como mencionamos, los sistemas basados en aprendizaje automático son una combinación de datos y código:

.. math::

   Sistemas\; de\; AA = codigo + datos

De igual forma que la ingeniería de software necesita versionar el código en las iteraciones para asegurar un control de cambios, en nuestros proyectos basados en datos deberemos de proveer los mísmos mecanismos para los datos.

Herramientas como `Git <https://en.wikipedia.org/wiki/Git>`_ son ampliamente utilizadas a la hora de mantener un control de cambios en un repositorio de código y podría decirse que hoy es un estandar. Sin embargo, Git realiza comparaciones linea a linea para identificar los cambios en versiones, y por lo tanto no resulta apropiado para realizar versionamiento de conjuntos de datos y las organizaciones suelen descansar en mecanismos especificos dependiendo de la infraestructura disponible. Estos métodos pueden ir desde versionamientos manuales utilizando estructuras de carpetas, hasta técnologias avanzadas como `Delta Time Travel <https://databricks.com/blog/2019/02/04/introducing-delta-time-travel-for-large-scale-data-lakes.html>`_. Independientemente de lo que la organización tenga disponible, es importante poder mantener una práctica de versionamiento de los conjuntos de datos lo cual nos permita que nuestros experimentos sean repetibles. Es más, esto puede ser un requerimiento de :doc:`../../develop/ops/validation/auditing` del cual no podamos escapar.
