==================================
Vinculación de datos en inferencia
==================================

Es una práctica común que muchos científicos de datos combinen diferentes orígenes de datos para generar un conjunto de datos con una diversa y variada cantidad de predictores. Por ejemplo, si estuviéramos utilizando un conjunto de datos de consumo de energía para una tarea de `forecasting`, sería útil disponer de la información del clima en cada uno de los días. 

Cuando nuestros predictores son consumidos desde lo que se conoce como `feature stores`, es posible que los mismos provean mecanismos para consumir esta información tanto en tiempo de entrenamiento como en tiempo de inferencia. Sin embargo, cuando este no es el caso o no se dispone de este tipo de tecnología, es necesario operacionalizar también mecanismos para obtener los predictores necesarios antes de ejecutar el modelo. 