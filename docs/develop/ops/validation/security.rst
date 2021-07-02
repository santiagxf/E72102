=========
Seguridad
=========

Al igual que cualquier pieza de software, los modelos de aprendizaje automático están expuestos a riesgos de seguridad. Sin embargo, también introduce desafíos específicos al tratarse de una tecnología de aprendizaje automático. Es importante tener en mente que la seguridad no es una carácteristica adicional e independiente que puede ofrecer un sistema, sino que es un principio de diseño del mismo.

La seguridad debe ser abordada desde dos perspectivas:
 - **Técnica**, consistente en implementar mecanismos de seguridad que impidan que los atacantes puedan obtener la información que buscan, pudiendose evitar ataques de fuerta bruta, encriptación sobre los datos, etc.
 - **Auditoría y monitoreo**, los cuales juegan un rol crítico en la seguridad de la información. 


Seguridad de los datos
----------------------
TODO

Data Poisoning
^^^^^^^^^^^^^^
Si el atacante obtiene acceso a los datos de entrenamiento, incluso de forma parcial, entonces podría modificar la distribución de los datos para obtener los resultados que está necesitando en el modelo. Si bien esto puede parecer complejo de realizar, podría no ser el caso. Por ejemplo, si estamos realizando análisis sobre los tweets que se envian a una cuenta en particular, un atacante podría manipular este origen de datos facilmente.

Data Stealing
^^^^^^^^^^^^^
Muchos modelos de aprendizaje automático pueden considerarse como *resumenes* de los datos sobre los que fueron entrenados. De esta forma, un atacante que ingresa determinados valores al modelo podría comenzar a obtener instancias verdaderas sobre los que se entrenó el modelo. Por ejemplo, si disponemos de un modelo que predice el salario de una persona y sabemos que el algoritmo que utiliza está basado en KNN, si introducimos el valor exacto en los predictores (codigo postal, sexo, edad, profesión, etc) de alguna persona que sabemos que está registrada en el sistema, entonces podremos obtener su salario.


Seguridad del modelo
--------------------
TODO

Adversarial Attacks
^^^^^^^^^^^^^^^^^^^
Ataques adversarios, aunque más conocido como *adversarial attacks*, es un tipo de problema de seguridad basado en redes adversarias generativas, o *generative adversarial networks (GANs)*. Esta técnica busca presentarle al modelo en cuestión un dato de entrada que ha sido perturbado (modificado) ligeramente de tal forma que si bien a simple vista pareciera una perturbación insignificante - o incluso inperceptible, produce grandes cambios en las predicciones del modelo. La idea central está basada en como funcionan las redes neuronales internamente, ya que buscan generar las perturbaciones mas pequeñas en los datos de entrada de tal forma que al multiplicar estos valores por todos los coeficientes de la red, genere las variaciones más grandes en la salida.


