======================
Técnicas de despliegue
======================

Hay dos conceptos importantes a tener en cuenta a la hora de poner un modelo de aprendizaje automático a disposición de nuestros usuarios, y son: los **despliegues** y las **versiones** (aunque más conocidas como **releases**). Un despliegue (*o deployment*) es el proceso por el cúal él código/modelo es ubicado o instalado en su ubicación final. Esta ubicación podría ser un servidor web, un dispositivo movil de un usuario, etc. Un release, por el contrario, es el proceso por el cúal el o los usuarios obtienen acceso al nuevo código/modelo/funcionalidad como parte de un objetivo de negocio. 

En algunos casos estos dos procesos se dan al unísono, pero no necesariamente. Un release, por ejemplo, puede involucrar varias instancias de despliegue y, también, un despliegue puede tener multiples releases o releases progresivos. En general, el proceso de despliegue es controlado por un área técnica de operaciones o incluso un proceso automático. El proceso de release, en general es controlado por el equipo responsable del producto.

A contuación veremos varias técnicas para controlar tanto el proceso de despliegue y el proceso de versiones.

Shadow testing
--------------
En algunas organizaciones, los ambientes de entrenamiento de modelos y los ambientes de despliegue del modelo son distintos y estan aislados. Como consecuencia, el reentrenamiento del modelo con nuevos datos podría verse comprometido y no reflejar exactamente el ambiente productico cuando se depliega. Una técnica para mitigar este riesgo consiste en desplegar el nuevo modelo, `modelo B`, junto con el modelo actual `modelo A`. En esta configuración, cada vez que ingresa una nueva solicitud para ejecutar el modelo, tanto el `modelo A` como el `modelo B` se ejecutan, aunque solo las predicciones de `modelo A` son retornadas al sistema. Las prediciones de `modelo B` son registradas vía logging. 

Este tipo de despliegue permite comparar estadisticamente los resultados de los modelos `modelo A` y `modelo B` sin comprometer el ambiente de producción. Si el resultado de este test es satisfactorio, entonces, el `modelo B` toma el lugar del `modelo A`. Esta técnica se conoce como *shadow scoring* y permite implementar transiciones controladas entre diferentes versiones del modelo.

.. note:: Shadow scoring supone que el valor verdadero de la predicción no depende de una acción que es consecuencia de la predicción. Por ejemplo, en el caso de un modelo que recomienda un elemento para comprar en un sitio de compras por internet, solo las predicciones de un modelo podrán ser evaluadas ya que es imposible determinar la performance del `modelo B` sin mostrar la recomendación propiamente dicha para que el usuario haga clic. En estos casos, está técnica es de poca utilidad.

.. _rst_blue_green_deployment:

Blue/Green
----------
Uno de los desafios más grandes a la hora de realizar un despliegue es el "corte" entre la versión antigua y la nueva versión del modelo. En general, uno necesita que este pasaje se realice rápido para evitar tener interrupciones en los servicios que el modelo provee. Sin embargo, no queremos cambiar de modelo hasta estar seguros de que funciona correctamente en el ambiente productivo. El despliegue de tipo Blue/Green trata de atacar esta problemática al proveer 2 ambientes productivos identicos (o tan identicos como sea posible). El nuevo modelo entonces es desplegado en un ambiente identico a producción al que llamamos **green**, mientras que el modelo original continua funcionando en el ambiente **blue**. Las fases finales de validación y control se realizan en este ambiente *green*. Una vez que nos aseguramos que el modelo funciona como esperamos, se realiza un intercambio de ambientes, es decir **green** toma el lugar de **blue** y viceversa. Esto se realiza con una simple configuración de ruteo de red para que todas las solicitudes ahora sean contestadas por el otro ambiente.

Este tipo de despliegue también tiene la ventaja de que permite una rápida *vuelta atrás* o **roll-back** ya que si algo no funciona como esperamos, podemos a volver a hacer el cambio. Por supuerto que, de ser este el caso y necesitar deshacer la operación, se habrán perdido todas las solicitudes que llegaron durante el periodo en donde el ambiente *green* estuvo respondiendo solicitudes. Estos casos pueden ser resueltos implementando algo similar a Shadow Testing que vimos anteriormente.

Una vez que el despliegue finaliza y es aceptado, el ambiente *green* pasa a llamarse *blue*, y el antiguo ambiente *green* queda disponible para desplegar las proximas versiones del modelo en cuestión.

.. _rst_progressive_rollouts:

Progressive Rollouts
--------------------
TODO

.. _rst_canary_releases:

Canary releases
---------------
Versiones canarias, o *canary releases*, es una técnica para reducir el riesgo asociado al introducir una nueva versión del modelo en producción. Se basa en la idea de introducir los cambios a un pequeño subset de usuarios antes de desplegar la nueva versión por completo y habilitarla para todos los usuarios.

Similar a `Blue/Green`_ , la nueva versión del modelo se despliega en un ambiente lo más similar al productivo posible y las pruebas de validación se realizan sobre el mismo. Una vez que estás pruebas se completaron, un pequeño grupo de usuarios es redireccionado para que utilice el nuevo ambientes - *green*. Esta selección puede realizar de forma simple elijiendolos al azar, o de forma más compleja, basada en propiedades del perfil del usuario, usuarios externos vs interos, etc. A medida que se gana más confianza con el nuevo despliegue, más usuarios son dirijidos a la nueva versión del modelo hasta que finalmente el 100% de los usuarios es direccionado al nuevo modelo y su versión anterior permanece inactiva. En este punto, podemos decomisar la infraestructura asociado con el modelo anterior.

Una de las ventajas más visibles de esta técnica es que podemos ir realizando pruebas de estrés y capacidad a medida que nuevos usuarios ingresan a la nueva versión del modelo. Esto lo logramos monitoreando las métricas de utilización de recursos. Adicionalmente, si encontramos un problema, siempre podemos volver hacia atrás con el despliegue.


A/B testing
-----------
Similar a `Blue/Green`_ , la nueva versión del modelo se despliega en un ambiente lo más similar al productivo posible y las pruebas de validación se realizan sobre el mismo. Sin embargo, en A/B testing, las solicitudes de ejecución del modelo se distribuyen entre los dos ambientes y modelos. Es decir, algunas solicitudes son enviadas al `modelo A` y otras solicitudes al `modelo B`. Cada solicitud es procesada o por uno o por el otro, pero nunca por ambos. Los resultados de ambos modelos son registrados via logging para el análisis.

.. warning:: A primera vista, esta técnica puede parecer similar a `Canary releases`_ debido a similaridades técnicas de implementación. Sin embargo, no deben confundirse. Mientras que *Canary releases* es una técnica para detectar problemas al implementar modelos de forma gradual utilizando un *canario*, A/B testing es una técnica para probar una hipótesis utilizando variaciones de un modelo (o multiples modelos). Incluso, dependiendo del tráfico, esperariamos poder concluir con un despluegue de tipo canario en horas, mientras que para una prueba A/B deberiamos de esperar hasta que nuestra prueba alcance significancia estadística.
