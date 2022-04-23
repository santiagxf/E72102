=======================
Definición del problema
=======================


    "The field of machine learning is concerned with the question of how to construct computer programs that automatically improve with experience."

    -- Machine Learning, Tom Mitchell.

La forma en la que define *Tom Mitchell*  en su libro *Machine Learning* a los sistemas de aprendizaje automático resulta de mucha utilidad al momento de utilizar estas técnicas para resolver un problema de negocio . Esta definición hace incapié en que no solo estamos interesados en resolver un problema utilizando datos, sino que además buscamos que su performance mejore con la experiencia. Esto implica que existe una dinámica de datos, representando la experiencia, que fluye desde el proceso de negocio hasta el modelo y que, a medida que pasa el tiempo, hacen que el modelo mejore en su tarea.

Formulación
-----------

La formulación del problema define cómo utilizaremos los datos (o la experiencia) para resolver un problema de negocio. Podemos definir un problema de aprendizaje automático como:

    A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E.

Aquí tenemos 3 parámetros que en esta fase del proceso debemos clarificar:

- **Tarea (T):** La tarea representa la acción que el modelo de aprendizaje automático debe realizar. Esta tarea debe ser concreta, como por ejemplo *clasificar el sentimiento de un tweet como positivo o negativo para la organización*. Es importante también que la tarea esté completamente especificada. En el ejemplo anterior la frase *como positivo o negativo* es ambigua. Necesitamos identificar que representa para nosotros un tweet positivo y como uno negativo. 
- **Experiencia (E):** La experiencia desde la cual mejoraremos nuestra performance, por ejemplo *un conjunto de tweets donde colaboradores de la organización han identificado (anotado) que describen un sentimiento negativo*.
- **Performance (P):** La métrica que utilizamos para medir nuestra performance. Esta puede ser intrínseca, por ejemplo *la precisión con la que el modelo clasifica un tweet correctamente*, o extrínseca, por ejemplo *la satisfacción general del cliente, suponiendo que al identificar tweets con sentimiento negativo nuestro equipo de marketing es capaz de interactuar con el usuario y solucionar el problema*. En general, al principio utilizamos métricas intrínsecas ya que son reproducibles y repetibles. Las métricas extrínsecas involucran personas, y por lo tanto, complejizan la evaluación. Cuando queremos medir el valor del modelo para el negocio utilizamos métricas extrínsecas.

.. note:: Es importante notar que la experiencia (E) puede existir o no al momento de la definición. Esto nos ayuda a no limitarnos a utilizar estas técnicas sólo con los datos que disponemos. Si la organización tiene un buen motivo para solucionar el problema utilizando aprendizaje automático entonces deberá disponer de alguna forma de :doc:`data`.

Motivación
----------

Es importante tener en claro cual es el valor de negocio que obtenemos al resolver el problema en cuestión. Idealmente este valor debe ser medido y debe haber una conexión entre la métrica de performance que elegimos durante la formulación del problema y el valor del negocio. Cuando utilizamos una métricas extrínsecas, la motivación es casi directa ya que estas métricas buscan medir justamente la contribución que hace el modelo en resolver un problema de negocio. Cuando se utilizan métricas intrínsecas, como ser `acurracy`, `precision` o `recall`, debemos de generar suposiciones que conecten estas métricas con el valor del negocio.

    ¿Porque pensamos que un modelo que clasifica correctamente tweets como sentimiento positivo o negativo hará que la satisfacción del cliente suba? ¿Como se mueven estas dos métricas? Un aumento de 5% en `acurracy` se traduce en un incremento de igual magnitud en satisfacción al cliente?


Suposiciones
------------

Según el teorema de **no free lunch (NFL)**, no existe un algoritmo universal que funcione bien para cualquier conjunto de datos y para cualquier problema. Esto quiere decir que nuestros modelos aprenden en el contexto de suposiciones que hacemos sobre los datos. Si las suposiciones son correctas, entonces nuestros modelos pueden hacer mejor sentido de los datos. Si nuestras suposiciones son incorrectas, en el mejor de los casos tendremos un modelo que genera predicciones con un grado de incertidumbre grande; en el peor de los casos, tendremos un modelo muy confidente generando las predicciones incorrectas.

Entonces las suposiciones son un elemento fundamental de la formulación de nuestro problema, deben ser correctamente documentadas y explicitadas de forma temprana en el proyecto. A menudo es útil identificar problemas similares al que queremos resolver, ya que estos problemas similares podrían ser informativos en saber cuales son las limitaciones o suposiciones que se necesitan enunciar para que la solución sea factible.
