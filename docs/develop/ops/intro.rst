.. index:: Operacionalización

==================
Operacionalización
==================

El poder desplegar soluciones de software rápidamente en producción es visto por las organizaciones como un factor clave para alcanzar sus objetivos de negocio. Sin embargo, esto es solo cierto si tal despliegue puede asegurar riesgos mínimos. Y es que esto último no es menor si consideramos que obtener un modelo funcionando en un ambiente de desarrollo no es garantia alguna de que nuestro modelo funcionará cuando se encuentre con el mundo real: ya sea con usuarios reales, con procesos de negocio reales, o con consecuencias reales. *Operacionalización* es el proceso por el cual un modelos de aprendizaje automático es empaquetado y disponibilizado para ser consumido. Cuando este modelo es consumido por los procesos de negocio reales de la organización, dirémos que el modelo está **productivo** o en un **ambiente de producción** y que se ha **liberado**. 

Los ambientes productivos dentro de una organización pueden tomar diferentes formas: desde servidores en centro de cómputos, plataformas de ciencias de datos específicas, como parte de un software que se distribuye a los clientes de la organización, como parte de una aplicación o incluso como parte de un dispositivo que vendemos (por ejemplo, el caso de los automobiles Tesla).

.. figure:: _images/ops_environments.png
   :alt: Segregación de ambientes
   :align: center

   *Separación de ambientes dentro del proceso de desarrollo de modelos de aprendizaje automático.*

Idealmente, esperariamos poder empaquetar nuetro modelo desarrollado con mínimos cambios a un ambiente productivo, ya que de esa forma, minimizariamos el riesgo de que nuestro modelo se comporte distinto a como lo hacía en desarrollo. Sin embargo, pocas veces en la práctica es este el caso. Existen diversas razones por las cuales debemos realizar adaptaciones y modificaciones al modelo para que pueda ser desplegado en producción de una forma escalable, sólida, segura y confiable. Este proceso se conoce como :doc:`adaptation/intro`.

Cuando nuestro modelo fue adaptado para alcanzar su ubicación final, una serie de procesos de :doc:`validation/intro` se aplican para asegurarse que el mismo cumple con los requisitos de calidad, auditabilidad y reproducibilidad: características que el negocio probablemente demande. También será necesario poder comunicar efectivamente los resultados que se esperan de nuetro modelo mediante un proceso de :doc:`interpret/intro`. Finalmente, deberemos empaquetar e instalar nuestro modelo en su ubicación final a traves del proceso de :doc:`deployment/intro` donde evaluaremos diferentes alternativas para minimizar el riesgo asociado al cambio. Por último, los equipos operativos de la organización deben poder monitorear que nuestro modelo se comporta de las forma que se esperaba y tal como fué diseñado, a través de su :doc:`monitoring/intro`.

.. toctree::
   :maxdepth: 2
   :caption: En esta sección
   :hidden:

   Preparación del modelo <adaptation/intro>
   Validación del modelo <validation/intro>
   Interpretación <interpret/intro>
   Despliegue del modelo <deployment/intro>
   Monitoreo <monitoring/intro>