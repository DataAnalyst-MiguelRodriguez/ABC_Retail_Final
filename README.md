ABC Retail | Análisis de datos, rentabilidad y conversión

Proyecto de portafolio de Data Analytics enfocado en transformar datos de ventas, marketing y comportamiento digital en hallazgos útiles para la toma de decisiones.

Este proyecto recorre un flujo de análisis de datos de principio a fin: exploración y limpieza, cálculo de KPIs de negocio, análisis del funnel de conversión, retención por cohortes y evaluación estadística de un experimento A/B sobre la interfaz de checkout.

Objetivo del proyecto

Evaluar el desempeño comercial de ABC Retail y detectar oportunidades de mejora a lo largo del recorrido del usuario. El análisis busca responder preguntas como:

¿El negocio genera ingresos suficientes para cubrir los costos considerados?

¿Qué productos y canales destacan en el desempeño comercial?

¿En qué etapa del funnel se observa la mayor caída de usuarios?

¿Cómo evoluciona la retención de usuarios después del registro?

¿Existe evidencia estadística de que un cambio en el checkout mejora la conversión?

Herramientas y tecnologías

Python: análisis y transformación de datos.

Pandas: limpieza, preparación, agrupación y análisis de datasets.

SQL / PostgreSQL: consultas a tablas de eventos, usuarios y actividad.

Matplotlib: visualización exploratoria.

Prueba z de dos proporciones: comparación de tasas de conversión entre variantes.

Power BI o Tableau: herramientas propuestas para la capa de visualización ejecutiva.

Proceso de análisis

1. Exploración y limpieza de datos

Se revisan los datasets de pedidos, catálogo y gasto de marketing para identificar problemas que pudieran afectar los resultados:

Conversión de campos de fecha al tipo adecuado.

Revisión de valores nulos, duplicados y categorías inconsistentes.

Detección de cantidades y montos negativos.

Estandarización de nombres de países y categorías.

Tratamiento documentado de valores faltantes.

Exportación de archivos limpios para el análisis posterior.

Valor aportado: una base más consistente para calcular indicadores y comparar resultados. Las decisiones de imputación deben interpretarse con cautela, ya que pueden influir en las métricas finales.

2. Rentabilidad y desempeño comercial

Se calculan indicadores para comprender los resultados comerciales:

Ingresos totales (revenue).

Costos de producto estimados a partir de las cantidades y el catálogo.

Inversión en marketing.

Beneficio calculado en el notebook.

Ticket promedio por pedido.

Cantidad promedio de productos por pedido.

Producto con mayor cantidad vendida.

Gasto de marketing por canal.

Resultados reportados por el notebook

Indicador

Resultado

Ingresos totales

$51,989,976.56

Costo total de productos

$2,522,407.61

Inversión en marketing

$2,871,843.53

Profit reportado

$46,595,725.42

Ticket promedio por pedido

$2,079.60

Cantidad promedio por pedido

7.11

Producto con mayor cantidad vendida

Laptop-Gaming-16GB

Nota de interpretación: estos importes son los resultados obtenidos en el notebook, no cifras auditadas. Antes de presentar el profit como rentabilidad definitiva, conviene validar la definición de ingresos, costos, descuentos, devoluciones y demás gastos operativos, así como la consistencia de las cantidades atípicas detectadas durante la limpieza.

3. Funnel de conversión

Con SQL sobre la tabla events, se cuentan usuarios únicos en cada evento del recorrido:

Etapa

Usuarios únicos

first_visit

7,796

select_item

7,582

add_to_cart

7,634

begin_checkout

7,208

add_payment_info

6,250

purchase

6,240

El notebook identifica la mayor caída entre begin_checkout y add_payment_info (aproximadamente 13.29% según el cálculo realizado).

Hallazgo para investigar: el conteo de add_to_cart supera al de select_item, lo que rompe el orden esperado de un funnel simple. Esto puede deberse a la definición de eventos, diferencias de población o metodología de conteo. Conviene validar la secuencia por usuario/sesión antes de extraer conclusiones causales.

4. Retención por cohortes

Se utilizan las tablas users y user_activity para agrupar usuarios por semana de registro y calcular su actividad en las semanas posteriores.

El análisis incluye:

Definición de cohortes según la fecha de registro.

Conteo de usuarios iniciales por cohorte.

Usuarios retenidos en las semanas 1, 2 y 3.

Cálculo de porcentajes de retención para comparar cohortes.

Este enfoque permite observar cómo cambia la actividad después del registro e identificar cohortes que merecen un análisis más profundo.

5. Experimento A/B: cambio en la interfaz de checkout

Se analiza el dataset experiment_checkout_ui.csv, con 10,000 registros y la variable de conversión convirtio. Se comparan las variantes control y tratamiento mediante una prueba z para dos proporciones.

Métrica

Control

Tratamiento

Conversiones

779

820

Usuarios del grupo

4,965

5,035

Tasa de conversión

15.69%

16.29%

Diferencia observada: +0.60 puntos porcentuales a favor del tratamiento.

Estadístico z reportado: 0.8133.

Valor p reportado: 0.4161.

Nivel de significancia de referencia: 0.05.

Conclusión: con esta muestra no se detectó una diferencia estadísticamente significativa entre las variantes. El resultado no demuestra que ambas experiencias sean idénticas; indica que no hay evidencia suficiente para afirmar que el cambio mejora la conversión. Antes de tomar una decisión, el notebook recomienda completar validaciones como SRM, balance por dispositivo y país, e intervalo de confianza.

Entregables y estructura

El notebook principal es ABC Retail_Proyecto_Final.ipynb. Durante el proceso se exportan estos archivos limpios:

orders_clean.csv

catalog_clean.csv

marketing_clean.csv

La última sección plantea la creación de un dashboard ejecutivo en Power BI o Tableau con KPIs de ingresos, profit, marketing, ticket promedio y comportamiento de conversión. El dashboard debe enlazarse aquí cuando esté publicado; el notebook incluye además un enlace a una carpeta de entrega en Google Drive.

Cómo revisar el proyecto

Abre ABC Retail_Proyecto_Final.ipynb en Jupyter Notebook, JupyterLab o Google Colab.

Revisa las secciones en orden: calidad de datos, KPIs comerciales, funnel, cohortes y experimento A/B.

Para reproducir la parte SQL, configura una conexión segura a PostgreSQL y confirma que tienes acceso a las tablas requeridas.

Para el dashboard, importa los CSV limpios en Power BI o Tableau y valida las relaciones y medidas antes de publicar.

Librerías principales

El notebook utiliza, entre otras, pandas, matplotlib, sqlalchemy y herramientas estadísticas de statsmodels. Verifica e instala las dependencias necesarias en tu entorno antes de ejecutar todas las celdas.

Competencias demostradas

Análisis exploratorio y preparación de datos.

Data cleaning y tratamiento de valores faltantes.

Análisis de KPIs comerciales y de marketing.

Consultas SQL sobre datos de comportamiento.

Análisis de funnel y retención por cohortes.

Pruebas de hipótesis y lectura de significancia estadística.

Comunicación de resultados y formulación de recomendaciones de negocio.

Próximas mejoras

Validar registros duplicados, cantidades extremas y reglas de cálculo antes de fijar los KPIs definitivos.

Revisar el orden del funnel mediante eventos por usuario y sesión.

Documentar las fórmulas exactas de profit y conversión.

Añadir intervalos de confianza y comprobaciones de calidad del experimento A/B.

Publicar el dashboard final y añadir capturas o enlace directo.

Añadir un archivo requirements.txt y una guía de configuración sin credenciales.

Autor: Miguel Angel Rodriguez Vega
Rol objetivo: Data Analyst
Contacto: https://www.linkedin.com/in/miguel-rodriguez-dataanalyst/ 

Este README describe los análisis y resultados que aparecen en el notebook. Los hallazgos se presentan como resultados exploratorios y deben validarse antes de usarse para decisiones operativas.
