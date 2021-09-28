.. _rst_data_adquisition:

====================
Adquisición de datos
====================

Una vez que tenemos el problema de negocio definido, una pregunta que nos podemos hacer es *¿Disponemos de los datos para resolver el problema?* O más aún *¿cuales son los datos que necesitaría para resolver el problema? ¿Qué calidad necesitamos que tengan?*. Estas preguntas no solo alcanzan al diseño del modelo sino que también a su puesta en producción: *¿Disponémos de los recursos para implementar los flujos de datos en producción? ¿Con que frecuencia necesitaré disponer de una nueva versión del conjunto de datos? ¿Cual es el costo total de manetener estos flujos de datos funcionando?*

.. _rst_data_adquire_ingest_generate:

Ingestar, adquirir o generar
----------------------------

El concepto de adquisición de datos puede tomar muchas formas dependiendo del contexto, el objetivo de la organización y la importancia del proyecto. Aquellas organizaciones que se centran en los datos justamente se permiten explotar esta fase al máximo. 

Ingestar
^^^^^^^^
En muchos casos la organización ya dispone de la información necesaria para entrenar el modelo. Sin embargo, es necesario de implementar procesos de ingesta de datos que nos permitan extraer la información desde los origenes de datos en los que se encuentran y depositarlos en algún repositorio donde podamos retenerla. Es importante extraer la información de su repositorio original en aquellos casos donde el repositorio por ejemplo es un sistema transaccional o un sistema OLAP que evoluciona en el tiempo. 

.. warning:: Durante el proceso de experimentación, el conjunto de datos debe mantenerse estático para que podamos obtener resultados repetibles.

Adquirir
^^^^^^^^
En otros casos puede ser que la organización no disponga de toda la información necesaria, y por ejemplo, deba adquirirla. Esta adquisición puede ser o bien a traves de un tercero, como por ejemplo la subscripción a un servicio de imágenes satelitáles, o también a traves de sus propios medios. Por ejemplo, es posible que para entrenar un modelo de detección de defectos en planchas de métal en una industría ciderurgica debamos de generar un conjunto de datos con imagenes tomadas de diferentes defectos para poder clasificarlas. Esta adquisición tendrá un costo para la organización es importante poder cuantificarlo.

Generar
^^^^^^^
Existen problemas donde disponer de un conjunto de datos más rico quizás ofrecería una performance mejor. Por ejemplo, en el caso anterior de un modelo de detección de defectos en planchas de métal, disponer de las mismas fotografías tomadas de diferentes ángulos, en diferentes tamaños, podría hacer que el modelo desarrlle mayor robustes para detectarlas en diferentes configuraciones. Esta técnica se la conoce como *data augmentation* y es un caso especial de la generación sintética de datos.

La generación sintética de datos nos permite generar nuevas instancias de datos a partir de datos pre-existentes, o, porque no, a partir de reglas de generación que definamos.


¿Por qué es importante focalizarse en los datos?
------------------------------------------------

Una estrategia para evolucionar la performance de un modelo de aprendizaje automatico es evolucionar el modelo. Esto quiere decir, probar nuevas arquitecturas, nuevas configuraciones, nuevos conjuntos de parámetros, etc. A esta estrategía, donde básicamente mantenemos los datos estáticos e introducimos modificaciones iterativamente sobre el código, se la conoce como *model-centric*.

En los sitemas basados en aprendizaje automático, aquellos que utilizan la mayor cantidad y calidad de datos son los ganadores. Esta realidad hace que muchos equipos de desarrollo se focalizen en la mejora continua de sus datos, es decir en una estrategia *data-centric*. Aquellas organizaciones que toman esta iniciativa en general la desarrollan junto a una política de adquisición de datos que les permite tener intención sobre la información que almacenan.

En general, los equipos que están involucrados en el desarrollo de modelos de aprendizaje automático están familiarizados o bien con las tareas de administración de datos o con las tareas de modelado, pero por separado. 

Existen multiples diferencias entre diseñar una solución de software y diseñar una solución de aprendizaje automático:

.. csv-table:: Diferencias entre diseñar una solución de software y diseñar una solución de aprendizaje automático
   :header: "Caracteristica", "Software", "Modelos de aprendizaje automático"
   :widths: 20, 50, 50

   "Objetivo", "Correctitud", "La optimización de una métrica"
   "Calidad*", "Depende deterministicamente del código", "Depende de los datos, de la arquitectura del modelo y sus hiperparámetros"



Conjunto de datos vs anotaciones
--------------------------------
En algunos casos, puede resultar útil diferencia entre *conjuntos de datos* y *conjuntos de anotaciones*. Los conjuntos de datos son colecciones de entidades, telemetría o cualquier información que será utilizada para entrenar nuestros modelos de aprendizaje automático. Los *conjuntos de anotaciones*, por el otro lado, son los valores de las etiquetas o incluso otras características que fueron extraidas de los mismos datos. Claramente las anotaciones siempre están asociados con un conjunto de datos, pero esta distinsión nos da una ventaja. En primer lugar, le permite a multiples proyectos y equipos etiquetar los datos de forma distinta. Aun más, dado que las anotaciones son información extra sobre las entidades, esta información puede evolucionar multiples veces sin necesidad de evolucionar el conjunto de datos. 

.. note:: Esta distinción no siempre suele realizarse, y dependerá de la implementación que la organización haya realizado de la plataforma de analítica avanzada.

Versionamiento
--------------
Herramientas como Git son ampliamente utilizadas a la hora de mantener un control de cambios en un repositorio de código. Sin embargo, git realiza comparaciones linea a linea, y por lo tanto no resulta apropiado para realizar versionamiento de conjuntos de datos.

Anonimización y emascaramiento
------------------------------
El *enmascaramiento*, también conocido como *ofuscamiento*, *anonimización* o *pseudonimización*, hace referencia al proceso por el cual aquella información clasificada como confidencial es ocultada a quien la consume mediante su remplazo por otros valores de datos o incluso caracteres especiales. Cuando trabajamos con datos que incluyen información sensible o regulada por la industria, los procesos de adquisición de datos deberán tener en cuenta la protección de esta información no solo para los diferentes roles que están involucrados en el ciclo de desarrollo del modelo sino que también durante el tránsito de la información (*data in motion*) y durante su almacenamiento (*data at rest*).

.. figure:: _images/3_states_of_data.jpg
   :alt: Estados de los datos
   :align: center

   Origen: Wikipedia

Quizás una de las tareas más complejas asociadas con la anonimización es el descubrimiento de la información sensible antes de que los usuarios tengan acceso a la misma. Existen herramientas en el mercado capaces de descubrir esta información dentro de los repositorios de la organización y disponibilizar mecanismos de enmascaramiento para protegerla.

Tipos de enmascaramientos
^^^^^^^^^^^^^^^^^^^^^^^^^

Existen diferentes tipos de enmascaramiento:

:Estático (SDM - Static Data Masking): En esta configuración, la información sensible se encuenra en el repositorio de datos original pero luego es enmascarada en una copia ubicada en un ambientes de destino que la organización puede compartir con los actores que lo requieren.
:Dinámica (DDM - Dynamic Data Masking): En esta configuración, no hay necesidad de duplicar el repositorio de datos ya que la información sensible permanece en el repositorio original pero es *dinámicamente* enmascarada al momento de ser consumida por los actores que lo requieren.

.. note:: El enmascaramiento de información es una forma de proteger información sensible, aunque podría no ser suficiente para evitar que un usuario mal intencionado tenga acceso a los valores reales de las instancias de datos. Por ejemplo, un usuario podría utilizar lógica para deducir los valores de los campos que han sido enmascarados, sobre todo cuando estos usuarios tienen conocimiento de alguna de las instancias de datos. La propiedad que asegura que un conjunto de datos no revelará información sensible ante un usuario se conoce como `private differenciable` y comprende un ámbito más grande que el del enmascaramiento de información.

Técnicas de enmascaramiento
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Dependiendo de los requerimientos de la organización y el tipo de análisis de datos que se va a realizar a posteriori, existen multiples técnicas para el enmascaramiento de datos. En lo que nos respecta al alcance de este curso, nos interesa indentificar que técnicas de enmascaramiento funcionarán de mejor manera con nuestros modelos de aprendizaje automático.

Podemos diferenciar técnicas *deterministas*, es decir, técnicas que producen el mismo resultado para la misma pieza de información, y técnicas *no deterministas* donde existe una naturaleza estocástica. La propiedad que mayormente nos interesará es la de obtener un conjnuto de datos que mantenga la misma distribución de los datos originales y esto lo podemos alcanzar con técnicas tanto determinstas como no deterministas, dependiendo de como se implemente cada una.

Adicionalmente, las técnicas pueden ser reversibles o irreversibles significando si es posible o no volver a obtener el dato original desde una pieza de información que fué enmascarada. En general, preferiremos métodos que sean irreversibles ya que nos aseguran que no sera posible volver a generar el dato original.

* Sustitución: Como el nombre lo sugiere, esta técnica consiste en remplazar la información original con datos que son o bien aleatórios o provenientes de una lista predefinida. La sustitución del dato puede ser total o parcial, siendo esta ultima muy utilizada por ejemplo en los sitios que almacenan tarjetas de crédito.
* Mezcla: Similar a sustitución, esta técnica consiste en remplazar la información original con el valor de otra instancia (registro) de datos. La ventaja de esta técnica es que el dato con el que se remplaza el valor es genuino ya que pertenece al conjunto de datos, aunque como consecuencia puede generar instancias de datos que no son realistas.
* Estádistica: Esta técnica consiste en remplazar la información original por un nuevo tipo de dato pero que preserva la misma distribución estádistica que los datos originales. La ventaja de este tipo de enmascaramiento es que preserva la mayoria de las propiedades en las que podemos estar interesados cuando utilizamos nuestros bancos de datos para entrenar modelos de aprendizaje automáticos.
* Encriptación: La encriptación no es estrictamente una técnica de enmascaramiento sino que de cifrado de datos, aunque es posible implementar 