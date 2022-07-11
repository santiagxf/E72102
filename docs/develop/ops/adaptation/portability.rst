============
Portabilidad
============

Una vez que un modelo específico ha sido seleccionado para producción, deberemos de persistirlo en almacenamiento duradero para su posterior implementación. El formato en el cual persistiremos el modelo debe ser considerado de forma temprana en el ciclo de desarrollo del modelo ya que puede tener gran impacto en el modelo propiamente dicho e incluso en las herramientas que utilizaremos. Por ejemplo, los modelos desarrollados con el popular Scikit-learn en Python requeriran técnicas de conversión para poder ejecutarlo en un entorno Java.

.. warning:: Es importante verificar que los modelos de aprendizaje automático podrán ser portados a la plataforma de destino de forma temprana en el desarrollo. De no hacerlo, corremos el riesgo de iniciar un proyecto de desarrollo que luego fallará en su etapada de validación. Como veremos en :ref:`rst_model_validation` mas adelante, el proceso de validación se realiza en un ambiente similar al de producción ya que será ese el modelo que finalmente será puesto productivo y no el que trabajamos en desarrollo. 

Formatos de almancenamiento de modelos
--------------------------------------

La siguiente trabla muestra los formatos más comunes que se utilizan dependiendo del la plataforma y framework de machine learning utilizado:

.. csv-table:: Formatos
   :header: "Formato", "Uso", "Descripcion"
   :widths: 5, 15, 50

   ".pb", "TensorFlow – R y Python", "Protocol Buffer: es un formato diseñado por Google que es independiente del lenguaje y de la plataforma."
   ".pt", "Torch – R y Python", "Más que un formato, es una referencia a modelos que están implementados con Torch. El formato interno puede ser Pickle o un diccionario con los parámetros del modelo. Este ultimo requiere que la arquitectura del modelo sea reconstruida en el destino."
   ".h5", "TensorFlow (1.8+) y Keras", "Permite almacenar grandes cantidades de datos numéricos y manipularlos fácilmente."
   ".pkl", "Scikit-Learn", "Pickle: Es un formato de serialización de objetos binaria. Debido a esto, el formato es sensible al software y runtime que lo genera y lo lee."
   ".rds", "R", "Es un formato especifico de R que permite serializar objetos en R que luego son comprimidos con gzip. Este formato es sensible al software y runtime que lo genera y lee."
   "MLeap", "Spark", "Usualmente estos archivos están empaquetados en zip conteniendo todos los pasos del pipeline de Machine Learning."
   ".mlmodel", "iOS", "Formato especifico para la plataforma de Apple iOS."
   ".onnx", "Múltiples frameworks", "Es un formato que permite abstraerse de la plataforma donde se entrenó el modelo. Soportado por PyTorch, TensorFlow, ScikitLearn, Spark, entre otros."
   ".pmml", "Múltiples frameworks", "Es un formato interoperable basado en XML que permite representar multiples tipos de modelos. Si bien su ultima versión (4.3) data de 2016, `multiples organizaciones lo soportan <http://dmg.org/pmml/products.html>`_ "
   "MLmodel", "MLflow", "Se trata de un formato especifico utilizado por la popular librería MLflow (el cual soporta una gran variedad de frmeworks de aprendizaje automático). Este formato es auto-contenido y permite no solo almacenar el modelo sino que también todos los componentes necesarios para su ejecución."


Conversión a formatos interoperables
------------------------------------
La conversión a formatos interoperables, como ONNX o PMML, pemite persistir los modelos en formatos que pueden ser ejecutados en diversos ambientes y plataformas independientemente de la tecnología con la que se entrenó el modelo. En algunos casos, puede ser que el framework de aprendizaje automático que estamos usando soporte persistir el modelo en estos formatos, en otros casos, deberemos hacer dicha partabilidad manualmente a través de las librerias de soporte que provea el formato.

Ejemplo de conversión al formato ONNX
*************************************
Por ejemplo, si quisieramos convertir un modelo entrenado con Keras a ONNX, podriamos utilizar la librería `onnxtools` de la siguiente forma. Primero definiremos un simple modelo::

   from keras.layers import Input, Dense, Add
   from keras.models import Model

   batch_size = 64
   input_dim = 3
   output_dim = 2

   inputs = Input(shape=(input_dim,))
   outputs = Dense(output_dim)(inputs)
   model = Model(inputs=inputs, outputs=outputs)

Luego podemos convertir el modelo a ONNX y persistirlo::

   import onnxmltools

   onnx_model = onnxmltools.convert_keras(model)
   onnxmltools.utils.save_model(onnx_model, 'ejemplo.onnx')


Persistir otros componentes
---------------------------

El modelo propiamente dicho es un componente central de nuestra implementación de aprendizaje automático, pero no debemos de perder de vista otros componentes que hacen posible que el modelo funcione correctamente. Por ejemplo, si durante la fase de :doc:`../../prep/engineering` se aplicaron transformaciones o normalizaciones de predictores, probablemente debamos de persistirlas para asegurarnos que las mismas se aplican de forma correcta durante inferencia.

.. note:: La forma en la que estas transformaciones se persiste dependerá del lenguaje de programación y de la librería que estemos utilizando.