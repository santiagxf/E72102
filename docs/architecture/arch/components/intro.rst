==========================
Organización y componentes
==========================

Las arquitecturas de procesamiento de datos empresariales están diseñadas para manejar la ingesta, el procesamiento y el análisis de datos en aquellos casos donde los mismos son demasiado grandes o complejos para los sistemas de bases de datos tradicionales. Estos sistemas están diseñados para escalar a un gran número de usuarios, y volumen de datos. Sin embargo, los conceptos aplican tanto para organizaciones pequeñas como grandes. Para pequeñas organizaciones, verán que muchos de los componentes que se mencionan aquí están concentrados en el mismo producto o componente de arquitectura. En grandes organizaciones, disponer de componentes específicos puede ayudar a la organización a reducir costos de escalamiento o a alcanzar un objetivo en particular.

No existe una receta única de cómo o qué tan grande/pequeña una arquitectura de datos debe ser, sino que tiene dependerá de los objetivos de negocio, tiempos, presupuestos, y objetivos. El rol del arquitecto de datos es el de diseñar estas arquitecturas.

Organización
------------

Las arquitecturas de datos empresariales generalmente involucran uno o más componentes que son responsables de llevar adelante las siguientes tareas:

* Procesamiento de :ref:`rst_data_batch` y en reposo.
* Procesamiento en :ref:`rst_data_stream`.
* Exploración interactiva de datos.
* Analítica predictiva y aprendizaje automático.

.. figure:: ../_images/arch-highlevel.png
   :alt: Elementos en una arquitectura de datos empresarial
   :align: center

   *Elementos en una arquitectura de datos empresarial*


Componentes
-----------

Desde un punto de vista de arquitectura, las tareas que se mencionaron anteriormente son llevadas a cabo por deferentes componentes técnologios que la organización puede implementar para materializar así una arquitectura de datos coherente.

.. figure:: ../_images/arch-components.png
   :alt: Componentes en una arquitectura de datos empresarial
   :align: center

   *Componentes en una arquitectura de datos empresarial*

La mayoría de las arquitecturas de procesamiento de datos consisten en operaciones de procesamiento de datos que se ejecutan de forma repetida. Estas operaciones están encapsuladas en procesos que transforman los datos, los mueven entre múltiples sistemas de almacenamiento, o envían los resultados directamente a un informe o tablero. Estos procesos deben estar orchestrados en la plataforma para que funcionen de forma coherente y puedan entregar los resultados que el negocio espera. Este es el rol de los componentes de orquestración.

.. toctree::
    :maxdepth: 1
    :caption: En esta sección

    sources
    ingest
    store
    process
    analytics
    consume
