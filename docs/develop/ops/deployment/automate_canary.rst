Análisis automático de versiones Canarias
=========================================

La utilización de versiones canarias es útil, pero en general requiere de un proceso manual que verifique que el `canario` se comporta como se espera antes de realizar una implementación completa. En principio, esto podría resultar sencillo, pero no siempre es tan claro como medir la diferencia entre una versión canaria y la versión anterior (or versión base).

En este contexto, la idea de *automatizar el análisis canario* parece ser una buena idea ya que se pueden implementar análisis estádisticos robustos que aseguren la correcta interpretación de una o un conjunto de métricas de manera objetiva. Adicionalmente, permite su utilización en organizaciones que requieren implementar software a alta velocidad.

.. note:: El análisis de versiones canárias no está diseñado para detectar errores o fallas, sino para controlar el riesgo asociado a una nueva funcionalidad o modelo de aprendizaje automático.

Kayenta
-------
Desarrollado conjuntamente por Google y Netflix, Kayenta es la evolución del sistema canario utilizado internamente por Netflix, pero reinventado para ser completamente abierto, extensible y capaz de manejar casos de uso más avanzados. Brinda a los equipos de las organizaciones la confianza para impulsar rápidamente los cambios de producción al reducir los análisis canarios ad-hoc, que requieren mucho tiempo y son propensos a errores.