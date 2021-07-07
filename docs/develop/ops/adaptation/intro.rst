=====================
Adaptación del modelo
=====================

Adaptación del modelo hace referencia al proceso por el cual un modelo de aprendizaje automático es preparado y empaquetado para poder ejecutar en un ambiente productivo. La adaptación del modelo puede tener dos historias, **la feliz** y la **no tan feliz**. La historia feliz sería el caso donde tanto el ambiente de desarrollo como el productivo utilizan la misma tecnología o al menos tecnologías compatibles. Esto sería: mismo framework de Machine Learning, mismo lenguaje de programación, mismo sistema operativo, misma plataforma, etc. En este caso, el trabajo que se debe realizar es relativamente poco.

La historia *no tan feliz*, en el otro extremo, sería el caso donde el modelo debe ser completamente reimplementado, incluso en otro lenguaje y por otro equipo. Esto se puede deber a:
 - Requerimientos de performance debido a la escala (computo distribuido)
 - Requerimientos de performance debido al dispositivo donde se ejecuta (un telefono celular)
 - Requerimientos de uso de tecnologías especificas (estandares de la organización)

Aunque parezca poco común, este es el caso de grandes sitios de e-commerce donde existe un alto tráfico o cuando los modelos son desplegados en dispositivos especificos, como ser teléfonos móbiles. Si bien no es el caso más general, muchas organizaciones hoy en día trabajan de esta forma donde equipos dedicados portan los modelos a la plataforma de destino.

En el medio de estas dos historias tenemos todas las combinaciones posibles y dependerá de cada organización y caso de negocio la cantidad de adaptación que hay que aplicar al modelo desarrollado.

.. toctree::
   :maxdepth: 2
   :caption: En esta sección
   :hidden:
   
   Portabilidad <portability>
   Performance <performance>

