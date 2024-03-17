=============
Entendimiento
=============

    "The naive simplicity of assuming that understanding meaning is easy, that there is one right definition. The relationship between objects and their essential meanings is far more problematic."

    -- Being and Nothingness essay, Jean-Paul Sartre.


Según una encuesta realizada por Harvard Business Review [1]_, la mayoria de las organizaciones creen ser buenas en la resolución de problemas. Sin embargo, el 85% dice tener dificultad para **identificar qué problema resolver**. Es más, el 87% afirma que esta dificultad y su consecuente "solución al problema incorrecto" les ha signficado grandes costos. Entonces: *¿realmente estamos solucionando el problema correcto? ¿estamos formulando el problema de la forma correcta?*.

Claro está que de nada nos sirve tener un modelo de aprendizaje automático que tiene una precisión del 99% si en realidad sus pedicciones no contribuyen a reducir el problema. Es más, cuando esto sucede nos deberíamos preguntar *¿sigue el problema sin resolverse o estamos creando nuevos problemas?*. Cuando trabajamos con modelos que buscan aprender a partir de la experiencia este punto se vuelve más crítico. Durante el análisis de datos, el analista intenta descubrir el significando de los datos, el cual lo lleva a determinar cual es su *valor de negocio*. Sin embargo, en la mayoria de los casos, los datos tiene **múltiples valoraciones** para el negocio.

Y es que cada vez que persistimos datos también persistimos *ideas* y *significados*, los cuales **deben ser re-interpretados más tarde** por otras personas (o máquinas). Esto sería trivial si existiera un significado único, pero en general los datos capturan la realidad con cierta *distancia digital*. Esta distancia, analogá al concepto de *distancia congnitiva*, representa una tensión interna entre lo que se cree que se almacena y lo que efectivamente se almacena. Más aún, tal distancia no es estática sino que varía en el tiempo ya que la realidad es un *moving target*. El mantenimiento de estos datos (así como también el de los sistemas que los instancian) es una tarea que - además de resultar para nada sencilla - también puede alterar el significado.

El entendimiento del problema es más relevante aún cuando consideramos las multiples diferencias que existen entre diseñar una solución de software y diseñar una solución de aprendizaje automático:

.. csv-table:: Diferencias entre diseñar una solución de software y diseñar una solución de aprendizaje automático
   :header: "Caracteristica", "Software tradicional", "Modelos de aprendizaje automático"
   :widths: 20, 50, 50

   "Objetivo", "Correctitud", "La optimización de una métrica"
   "Calidad", "Depende deterministicamente del código", "Depende de los datos, de la arquitectura del modelo y sus hiperparámetros"

Lecture recomendada: `ML system design: 200 case studies to learn from <https://www.evidentlyai.com/ml-system-design>`_

.. [1] `Reframing them can reveal unexpected solutions. by Thomas Wedell-Wedellsborg <https://hbr.org/2017/01/are-you-solving-the-right-problems>`_

.. toctree::
    :maxdepth: 2
    :caption: En esta sección
    :hidden:
 
    Definición del problema <statement>
    Adquisición de datos <data>
