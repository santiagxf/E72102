.. index:: Operacionalización

==================
Operacionalización
==================

Obtener un modelo funcionando en un ambiente de desarrollo no es garantia alguna de que nuestro modelo funcionará en cuando se encuentre con el mundo real: ya sea con usuarios reales, con procesos de negocio reales, o con consecuencias reales. *Operacionalización* es el proceso por el cual un modelos de aprendizaje automático es empaquetado y disponibilizado para ser consumido. Cuando este modelo es consumido por los procesos de negocio reales de la organización, dirémos que el modelo está **productivo** o en un **ambiente de producción**. 

Los ambientes productivos dentro de una organización puede tomar diferentes formas: desde servidores en centro de computos, plataformas de ciencias de datos específicas, como parte de un software que se distribuye a los clientes de la organización, como parte de una aplicación e incluso como parte de un dispositivo que vendemos (como es el caso de los automobiles Tesla).

Idealmente, esperariamos poder empaquetar nuetro modelo desarrollado con minimos cambios a un ambiente productivo ya que, de esa forma, minimizariamos el riesgo de que nuestro modelo se comporte distinto que como lo hacia en desarrollo. Sin embargo, en la práctica, es mucho mas común de lo que uno espera de que este no sea el caso. Adaptaciones deben de realizarse al modelo para que pueda ser puesto en producción de forma correcta.

.. toctree::
   :maxdepth: 2
   :caption: En esta sección

   Adaptación del modelo <adaptation/intro>
   Validación del modelo <validation/intro>
   Despliegue del modelo <deployment/intro>
   Monitoreo <monitoring/intro>