=========
Monitoreo
=========

Una vez que el modelo está desplegado en producción, es cucial asegurarse que el mismo *performa bien* a lo largo de su vida útil. Sin embargo, *performar bien* puede tener diferentes significados dependiendo el contexto, especialmente para las diferentes personas en el equipo del proyecto.

En general, estas personas buscarán tener respuestas a preguntas como:
 - ¿Responde el modelo en la velocidad que estamos esperando?
 - ¿Qué cantidad de memoria y CPU está utilizando?
 - ¿Qué predicciones está arrojando mi modelo a los usuarios?
 - ¿Cuando se equivoca?

Esto quiere decir que diferentes personas pueden tener diferentes objetivos a la hora de monitorear un modelo de aprendizaje automático, y, por lo tanto, el equipo encargado de realizarlo tiene que tener en cuenta todas estas necesidades. En algunos casos, como es el monitoreo de los recursos de CPU y Memoria, los equipos que administran el despliegue están acostumbrados a monitorearlos y tienen herramientas especificas que le permiten controlarlo. Si bien los requisitos que puede tener, por ejemplo, un modelo de aprendizaje profundo (Deep Learning) son muy distintos a los de un simple regresor logístico, podemos disponibilizar herramientas que escalen el computo a medida que es necesario. Especialmente cuando se trata de despliegues en la nube.

Sin embargo, otro tipo de monitoreos puede ser más dificil de implementar. Por ejemplo, científicos de datos pueden estar interesados en monitorear la performance del modelo a lo largo del tiempo. Un modelo puede ser muy efectivo hace 6 meses atrás, pero comenzar a performar de forma errática luego cuando el patrón de uso de los compradores ha cambiado drasticamente debido a algún suceso (el cambio en el servicio de entrega a domicilio, por ejemplo). ¿Como podemos detectar cuando la performance del modelo se ha degradado? La respuesta a esta pregunta no es tan sencilla de contestar.

.. toctree::
    :maxdepth: 2
    :caption: En esta sección
    :hidden:
 
    Diagnóstico y alertas <logging>
    Evaluación online <onlineEval>
    Desviaciones <drift>