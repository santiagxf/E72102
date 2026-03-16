Diseño de arquitecturas de datos para sistemas de IA agente
==================================================================

Introducción
------------

Las arquitecturas de datos empresariales fueron diseñadas históricamente para ayudar a las personas a analizar datos. Los *data warehouses* almacenaban hechos, las capas de transformación preparaban los datos y las herramientas de BI permitían a analistas y ejecutivos explorar reportes y *dashboards*. En este modelo, los humanos eran siempre el intérprete final del significado y quienes tomaban las decisiones.

Los sistemas de IA agente cambian este supuesto. Los agentes autónomos cada vez más leen datos, interpretan el estado del sistema y activan acciones antes de que una persona revise un *dashboard*. Debido a este cambio, las arquitecturas de datos modernas deben soportar no solo la recuperación de datos, sino también la interpretación confiable y la toma de decisiones controlada.

El principio arquitectónico clave es simple: los sistemas deben exponer significado, no solo datos. Los sistemas agentes no pueden depender del contexto humano, de documentación informal o de interpretaciones que existen únicamente en la memoria de las personas. El significado debe formalizarse y estar disponible mediante interfaces legibles por máquinas.

Este artículo presenta los componentes principales y las guías para diseñar un *data stack* empresarial moderno que soporte IA agente.

Separar observaciones de significado
------------

Una regla arquitectónica fundamental es separar los datos observados del significado interpretado.

Los datos observados representan eventos y hechos registrados por los sistemas operacionales: transacciones, clics, pagos, pedidos o eventos de registro. Estos pertenecen a las capas crudas y modeladas de la plataforma de datos.

El significado representa cómo la organización interpreta esos eventos. Métricas como ingresos, churn usuarios activos o tasa de conversión no son solo cálculos; representan acuerdos sobre cómo deben interpretarse los datos.

En los sistemas tradicionales, el significado era reconstruido por los analistas. En los sistemas agentes, el significado debe definirse explícitamente y estar disponible.

Guía:

- Tratar el almacenamiento de datos como la capa de observación.
- Construir una capa separada de interpretación responsable de definir el significado de negocio.

Mantener una capa de observación confiable
------------

La capa de observación sigue siendo esencial. Contiene todos los registros factuales de lo que ocurrió en el negocio.

Los componentes típicos incluyen:

- Sistemas operacionales (aplicaciones, servicios, plataformas SaaS)
- Pipelines de ingestión de datos
- Un *data warehouse* o *lakehouse* centralizado
- Pipelines de transformación y modelado

Frameworks de transformación como ``dbt`` son muy valiosos en esta capa. Proveen control de versiones, pruebas, seguimiento de linaje y modelos reproducibles.

Sin embargo, su función es producir observaciones confiables. Aseguran que las métricas puedan calcularse de forma consistente, pero no definen cómo esas métricas deben interpretarse en contextos de decisión.

Guía:

- Utilizar frameworks de transformación para estabilizar los cálculos.
- No asumir que estos modelos capturan el significado de negocio.

Introducir una capa semántica explícita
------------

Los sistemas agentes requieren una capa que formalice el significado de negocio.

La capa semántica define:

- Definiciones de métricas
- Conceptos de negocio
- Comparaciones válidas
- Reglas de interpretación
- Supuestos y restricciones

Históricamente, las capas semánticas estaban acopladas a herramientas de BI y servían principalmente para *dashboards*. En arquitecturas modernas, la capa semántica debe existir de forma independiente y servir tanto a humanos como a sistemas de software.

Su función es estabilizar la interpretación entre herramientas, equipos y sistemas automatizados.

Guía:

- Tratar la capa semántica como un modelo central de conocimiento de la organización, no solo como una conveniencia para BI.

Exponer significado mediante una API semántica
------------

Para los sistemas agentes, la documentación textual no es suficiente. Los agentes necesitan interfaces determinísticas que eliminen la ambigüedad.

En lugar de generar consultas SQL para reconstruir lógica de negocio, los agentes deberían llamar operaciones semánticas predefinidas.

Ejemplos:

- ``GetRecognizedRevenue(period)``
- ``GetActiveCustomers(segment, time_window)``
- ``GetChurnRate(cohort, month)``
- ``GetCampaignEfficiency(channel)``

Estas operaciones contienen la lógica aprobada por el negocio y las reglas de interpretación.

Este enfoque transforma las métricas de fórmulas a funciones invocables. Los agentes ya no adivinan el significado; lo obtienen mediante interfaces controladas.

Guía:

- Exponer métricas y conceptos de negocio como operaciones tipo API en lugar de permitir que los agentes infieran lógica desde tablas crudas.

Agregar un motor de interpretación
------------

Los sistemas agentes requieren más que métricas. Deben entender si el comportamiento del sistema es normal, anómalo o requiere acción.

Un motor de interpretación evalúa observaciones frente a reglas de negocio y genera señales como:

::

   state = normal
   state = warning
   state = critical
   action_required = true

Ejemplos de reglas:

- Caída de ingresos mayor al 10% semana contra semana
- Churn de clientes por encima de un umbral específico de segmento
- CAC de marketing por encima del límite permitido para una campaña

Estas reglas transforman métricas en señales operativas.

Guía:

- Implementar una capa de evaluación de reglas que convierta métricas en estados del sistema y señales para la toma automática de decisiones.

Tratar a los agentes de IA como usuarios del sistema
------------

Las arquitecturas tradicionales fueron diseñadas alrededor de usuarios humanos como analistas, gerentes de producto o ejecutivos.

Las arquitecturas modernas deben soportar explícitamente a los agentes de IA como usuarios del sistema.

Los agentes deberían interactuar con:

- APIs semánticas
- Sistemas de señales y estados
- Interfaces de acción gobernadas
- Mecanismos de auditoría y explicación

Los agentes raramente deberían consultar directamente tablas del *warehouse*, ya que esto los obliga a inferir significado y aumenta el riesgo de decisiones incorrectas.

Guía:

- Diseñar interfaces de datos para consumo por máquinas, no solo para exploración humana.

Definir límites de acción
------------

Los sistemas agentes deben operar dentro de límites de decisión bien definidos.

Para cada señal o regla de interpretación, el sistema debe definir:

- Qué acciones están permitidas
- Qué acciones requieren aprobación
- Qué acciones son solo recomendaciones

Ejemplos:

- Detener automáticamente una campaña publicitaria
- Enviar una alerta al equipo de marketing
- Ajustar una previsión
- Recomendar, pero no ejecutar, un cambio de precio

Esto convierte la analítica en un sistema operativo controlado en lugar de una automatización descontrolada.

Guía:

- Definir políticas explícitas que conecten señales con acciones permitidas.

Preservar la explicabilidad mediante BI
------------

Incluso en sistemas agentes, los humanos necesitan visibilidad y confianza.

Los *dashboards* y herramientas de BI siguen siendo importantes, pero su rol cambia. En lugar de descubrir problemas, cada vez más explican decisiones que el sistema ya tomó.

Un flujo típico se vuelve:

- Los datos se recolectan
- La capa semántica interpreta métricas
- Las reglas determinan el estado del sistema
- Un agente ejecuta una acción
- Los dashboards explican por qué

Guía:

- Utilizar BI para transparencia y gobernanza, no como la interfaz principal de decisión.

Alinear acuerdos organizacionales
------------

La parte más difícil de construir arquitecturas agentes rara vez es la tecnología. Es alinear las definiciones de negocio.

Diferentes departamentos suelen interpretar las mismas métricas de forma distinta. Cuando las decisiones se automatizan, estas diferencias deben resolverse explícitamente.

Las organizaciones deben acordar:

- Definiciones de métricas
- Ventanas de comparación
- Umbrales aceptables
- Políticas de decisión

Estos acuerdos deben codificarse en las capas semántica y de reglas.

Guía:

- Tratar las definiciones de negocio como contratos formales del sistema, no como conocimiento informal del equipo.

Conclusión
------------

La transición hacia IA agente transforma el propósito de las arquitecturas de datos empresariales.

Los *data stacks* tradicionales estaban optimizados para responder preguntas. Los stacks modernos deben soportar interpretación automática y acción controlada.

Esto requiere tres capas conceptuales:

- Capa de observación: almacena eventos factuales y transformaciones.
- Capa semántica: define significado de negocio y lógica de métricas.
- Capa de interpretación: evalúa el estado del sistema y dispara acciones.

Cuando estas capas están claramente separadas y expuestas mediante interfaces determinísticas, los agentes de IA pueden operar de forma segura y predecible dentro de sistemas empresariales.

En esta arquitectura, los datos siguen siendo la base, pero el significado se convierte en el centro del sistema.
