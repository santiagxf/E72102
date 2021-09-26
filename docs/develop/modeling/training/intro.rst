========================
Entrenamiento del modelo
========================

Centralizado vs federado
------------------------
Cuando los modelos de aprendizaje automático serán desplegados en millones de dispositivos, como ser teléfonos celulares, sensores o incluso autos hoy en día, el entrenamiento de estos modelos puede ser desafiante. Quizás la opción mas sencilla de visualizar es recolectar toda la información de estos dispositivos en una ubicación centralizada para confirmar el conjunto de datos sobre el que se va a trabajar. Luego, un modelo se entrena de forma centralizado y se despliega en cada uno de los dispositivos en cuestión. Por ejemlo, el sistema de autompiloto de Tesla (Tesla Autopilot System), que se ejecuta en mas de 500.000 autos hoy en día funciona de esta forma.

Otra alternativa a esta es, en lugar de utilizar un proceso centralizado de entrenamiento, realizar "pequeños entrenamientos de ajuste" (técnica conocida como fine tunning) en cada uno de los dispositivos en cuestión. Estos ajustes o mejoras que cada uno de los dispositivos encuentra, son luego reportadas a un servidor centralizado que recolecta el feedback de cada uno de los dispositivos y los condenza. Estas actualizaciones pueden luego ser "empujadas" a cada uno de los modelos nuevamente para que todos se beneficien. Esta técnica de entrenamiento se conoce como **Federated Learning** y tiene ademas la ventaja de que los datos de cada uno de los dispositivos no viaja a una ubicación centralizada, lo cual puede tener implicancias desde el punto de vista regulatorio.

Entrenamiento estratificado de modelos
--------------------------------------

Supongamos que una organización quiere predecir la demanda de productos de los clientes para optimizar la cantidad su cadena de suministro. Sin embargo, el comportamiento varía mucho de una ciudad a la otra, o de un estado al otro. Incluso podría ser que varia de cada una de las locaciones. El modelado estratificado consiste en entrenar un modelo por cada ubicación que la organización dispone en lugar de buscar entrenar un modelo que pueda resolver todas las ubicaciones correctamente.