=====================
Despliegue del modelo
=====================

En general, un modelo de aprendizaje automático puede ser desplegado en 2 formas distintas, conocidas como *tiempo real* o *real time / online* y *por lotes* o *batch*. 

El modo *batch* hace referencia a modelos que son ejecutados sobre sets de datos enteros, como ser por ejemplo, la base completa de clientes de una organización para categorizar los clientes según perfiles. La caracteristica más importante de este modo de despliegue es que el proceso en general es programado y dispone de una ventana de tiempo grande para completarse.

El modo *real time* hace referencia a modelos que son ejecutados de forma sincrónica, sobre un cantidad de muestras pequeñas y puntuales, por ejemplo cuando un usuario visualiza la página de inicio de un portal de compras y aparecen algunas sugerencias de productos. La característica más importante de este modo de despliegue es que la solicitud de inferencia es bajo demanda, impredecible en el tiempo y en general debe resolverse tan pronto como sea posible.

A pesar de que estos dos modos parecieran ser diametralmente opuestos, en muchos casos, las implementaciones para realizar cada modo de despliegue son idénticas. En otros casos, podría ser completamente diferente.

Adicionalmente, existen diferentes estratégias de despliegue dependiendo de las necesidades del negocio, la magnitud del despliegue y el nivel de control que queremos retener en el proceso.

.. toctree::
    :maxdepth: 2
    :caption: En esta sección
    :hidden:
    
    Contenerización <containerization>
    Estratégias de depliegue <deployment>
    Escalamiento <scaling>