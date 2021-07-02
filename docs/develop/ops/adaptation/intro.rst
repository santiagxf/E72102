=====================
Adaptación del modelo
=====================

La adaptación del modelo puede tener dos historias, **la feliz** y la **no tan feliz**. La historia feliz sería el caso donde tanto el ambiente de desarrollo como el productivo utilizan la misma tecnología o al menos tecnologías compatibles. Esto sería: mismo framework de Machine Learning, mismo lenguaje de programación, mismo sistema operativo, misma plataforma, etc. En este caso, el trabajo que se debe realizar es relativamente poco.

La historia *no tan feliz* sería donde el modelo debe ser completamente reimplementado desde cero, incluso en otro lenguaje y por otro equipo. Esto puede deberse a:
 - Requerimientos de performance debido a la escala (computo distribuido)
 - Requerimientos de performance debido al dispositivo donde se ejecuta (un telefono celular)
 - Requerimientos de uso de tecnologías especificas (estandares de la organización)

Aunque parezca poco común, esto es el caso de grandes sitios de e-commerce donde tienen un alto tráfico o cuando los modelos son desplegados en dispositivos especificos. Si bien no es el caso más general, muchas organizaciones hoy en día trabajan de esta forma donde equipos dedicados portan los modelos a la plataforma de destino.

En el medio de estas dos historias tenemos todas las combinaciones posibles y dependerá de cada organización y caso de negocio la cantidad de adaptación que hay que aplicar al modelo desarrollado.

.. toctree::
   :maxdepth: 2
   :caption: En esta sección
   
   Portabilidad <portability>
   Performance <performance>

