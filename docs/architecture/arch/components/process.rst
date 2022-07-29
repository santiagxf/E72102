============================
Componentes de procesamiento
============================


Procesamiento por lotes (batch)
-------------------------------

Debido a que los conjuntos de datos son tan grandes, a menudo una solución de big data debe procesar archivos de datos mediante largas ejecuciones de procesamieento de datos para filtrar, agregar y preparar los datos para el análisis. Por lo general, estos trabajos implican leer archivos del origen, procesarlos y escribir la salida en archivos nuevos.


Procesamiento en alta velocidad (stream)
----------------------------------------

Después de capturar mensajes en tiempo real, la solución debe procesarlos filtrando, agregando y preparando los datos para el análisis. Los datos de flujo procesados luego se escriben en un receptor de salida. Tecnologias de nubo como Azure Stream Analytics o AWS Firehorse proporcionan un servicio de procesamiento de datos en alta velocidad administrado que permite a las organizaciones disponer de una técnologia de procesamiento de eventos con garantias de performance. También puede usar tecnologías de streaming de código abierto como ser Apache Storm y Apache Spark Streaming en un clústers de procesamiento distribuido.