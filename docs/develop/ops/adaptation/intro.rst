=====================
Adaptación del modelo
=====================

La adaptación del modelo puede tener dos historias, **la feliz** y la **no tan feliz**. La historia feliz sería el caso donde tanto el ambiente de desarrollo como el productivo utilizan la misma tecnología o al menos tecnologías compatibles. Esto sería: mismo framework de Machine Learning, mismo lenguaje de programación, mismo sistema operativo, misma plataforma, etc. En este caso, el trabajo que se debe realizar es relativamente poco.

La historia *no tan feliz* sería donde el modelo debe ser completamente reimplementado desde cero, incluso en otro lenguaje y por otro equipo. Esto puede deberse a que, debido a la escala, el uso de tecnologías especificas, requerimientos de performances especificos, el modelo debe de ser implementando y optimizado para la plataforma de destino. Esto es el caso de grandes sitios de e-commerce donde tienen un alto tráfico o cuando los modelos son desplegados en dispositivos especificos. Si bien no es el caso más general, muchas organizaciones hoy en día trabajan de esta forma.

En el medio de estas dos historias tenemos todas las combinaciones posibles. 

.. toctree::
   :maxdepth: 2
   :caption: En esta sección
   
   Portabilidad <portability>
   Performance <performance>

