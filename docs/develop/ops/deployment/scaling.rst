Escalamiento
============

Independientemente de si estamos ejecutando modelos en tiempo real (*real time*) o por lotes (*batch*), es posible que para poder alcanzar los requerimientos de performance y latencia del negocio, tengamos que aumentar el número de instancias que ejecutan el modelo para poder acomodar la demanda. Desplegar multiples modelos o instancias del modelo para inferencia en tiempo real puede ser conceptualmente más sencillo de implementar que desplegar multiples modelos para procesamiento por lotes, pero en ambos casos es alcanzable.


Escalamiento de modelos en tiempo real
--------------------------------------
Escalar un modelo que se ejecuta en tiempo real, en general, resulta bastante sencillo si se lo implementa de la forma correcta (vea :doc:`containerization`). Es posible instanciar muliples instancias de nuestro modelo para luego utilizar un balanceador de carga que distribuya las solicitudes a cada una de estas instancias. De esta forma, el balanceador de carga controla la cantidad de solicitudes que recibe cada una de las instancias. Lo que es más, esta técnica permite tanto el escalamiento hacia arriba como hacia abajo, significando que podemos decomisar algunas instancias en aquellos momentos de menor carga y aumentar la cantidad en aquellos momentos de mayor demanda. Este tipo de comportamiento se conoce como *elástico*.


Escalamiento de modelos de procesamiento por lotes
--------------------------------------------------
La ejecución de modelos en modo *batch* también puede ser paralelizado utilizando varias técnicas. Una forma de realizarlo, es utilizando una plataforma que sea inerentemente distribuida. Este es el caso de `Apache Spark` por ejemplo. `Spark` es un framework de cómputo distribuido que permite la distribución de la carga entre todos los nodos que componen el cluster donde se ejecuta `Spark`. Sin embargo, esto requerirá adaptar nuestro modelo a este tipo de plataformas tal como se menciona en :doc:`../adaptation/portability`.

Otra alternativa es la utilización de técnicas de `partitioning` como `sharding` donde podemos dividir un conjunto de datos grandes en multiples conjuntos de datos más pequeños donde ejecutar nuestro modelo en paralelo. 

:Sharding: También conocido como `horizontal partitioning`, consiste en dividir un conjunto de datos en multiples conjuntos de datos basandose en algún atributo (o varios atributos) que se llaman `keys` o `sharding keys`. Por ejemplo, si tuvieramos un conjunto de datos de clientes, podríamos particionarlo horizontalmente basandonos en la propiedad `CustomerID` y asignar los clientes con IDs en el rango 0-1000 en un shard, 1001-2000 en otro, etc.

Una vez que el modelo se ejecuta en cada una de las *particiones* o *shards*, los sub-conjuntos de datos se combinan nuevamente para volver a formar el conjunto de datos original.