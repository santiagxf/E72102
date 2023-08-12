======================
Preparación del modelo
======================

Preparación y Adaptación del modelo hace referencia al proceso por el cual un modelo de aprendizaje automático es preparado y empaquetado para poder ejecutar en un ambiente productivo. La adaptación del modelo puede seguir dos caminos, **uno feliz** y otro **no tan feliz**. El camino feliz sería el caso donde tanto el ambiente de desarrollo como el productivo utilizan la misma tecnología o al menos tecnologías compatibles. Esto sería: mismo framework de Machine Learning, mismo lenguaje de programación, mismo sistema operativo, misma plataforma, etc. En este caso, el trabajo que se debe realizar es relativamente poco.

El camino *no tan feliz*, en el otro extremo, sería el caso donde el modelo debe ser completamente reimplementado, incluso en otro lenguaje y por otro equipo. Esto se puede deber a:
 - Requerimientos de performance debido a la escala (computo distribuido)
 - Requerimientos de performance debido al dispositivo donde se ejecuta (un telefono celular)
 - Requerimientos de uso de tecnologías especificas.

Incluso dentro de la misma organización, muchos equipos tienen diferentes preferencias de frameworks para utilizar, herramientas, entornos de desarrollo, etc. Desde un punto de vista de agilidad, esto puede parecer algo bueno ya que esta flexibilidad permite a los equipos utilizar el conjunto de tecnologías que mejor se adapta a las necesidades e incluso les permite innovar adoptando tecnologías emergentes. Sin embargo, desde el punto de vista de aquellos equipos que se encargan de la disponibilidad, despliegue e implementación de estas tecnologías, este panorama puede volverse una pesadilla. Esto hace que los equipos deban integrar una gran varidad de componentes, volviendo a las soluciones muy frágiles debido a la velocidad en la que cambian. Este último punto es importante remarcarlo ya que refuerza la necesidad de que estas tecnologías sigan estandares de código abierto para aliviar el problema.

Aunque parezca poco común, este es el caso de grandes sitios de e-commerce donde existe un alto tráfico o cuando los modelos son desplegados en dispositivos especificos, como ser teléfonos móbiles. Muchas organizaciones hoy en día trabajan de esta forma donde equipos dedicados portan los modelos a la plataforma de destino.

En el medio de estos dos caminos tenemos todas las combinaciones posibles y dependerá de cada organización y caso de negocio la cantidad de adaptación que hay que aplicar al modelo desarrollado.

.. toctree::
   :maxdepth: 2
   :caption: En esta sección
   :hidden:
   
   Portabilidad <portability>
   El estandar MLflow <code/mlflow_package.ipynb>
   Vinculación de datos en inferencia <augmentation>
   Performance <performance>

