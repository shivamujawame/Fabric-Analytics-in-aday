# **Microsoft Fabric Fabric Analyst in a Day - Laboratorio 1**

![](../media/lab-01/main1.png)

# Contenido 
- Estructura del documento	
- Escenario/planteamiento del problema	
- Información general del informe de Power BI Desktop	
   - Tarea 1: Configurar Power BI Desktop en un entorno de laboratorio	
   - Tarea 2: Analizar el informe de Power BI Desktop	
   - Tarea 3: Revisar consultas de Power Query	
- Referencias	

# Estructura del documento
El laboratorio incluye pasos que el usuario debe seguir junto con capturas de pantalla asociadas que sirven de ayuda visual. En cada captura de pantalla, las secciones se resaltan con cuadros de color naranja para indicar en qué áreas debe centrarse el usuario.

 - **Nota:** Algunas de las capturas de pantalla pueden estar desactualizadas debido a las actualizaciones continuas del producto.

# Escenario/planteamiento del problema

Fabrikam, Inc. es un distribuidor mayorista de artículos novedosos. Como mayorista, los clientes de Fabrikam son en su mayoría empresas que revenden a particulares. Fabrikam vende a clientes minoristas en todo Estados Unidos, incluidas tiendas especializadas, supermercados, tiendas de informática y tiendas de atracciones turísticas. Fabrikam también vende a otros mayoristas a través de una red de agentes que promocionan los productos en nombre de Fabrikam. Si bien todos los clientes de Fabrikam tienen su sede actualmente en los Estados Unidos, la compañía tiene la intención de impulsar la expansión a otros países y regiones.

Es analista de datos en el equipo de ventas. Usted recopila, limpia e interpreta conjuntos de datos para resolver problemas comerciales. También reúne visualizaciones como cuadros y gráficos, escribe informes y los presenta a los encargados de tomar decisiones de la organización.

Para extraer información valiosa de los datos, se extraen datos de varios sistemas, se limpian y se combinan. Extrae datos de los siguientes orígenes:

- Datos de ventas: estos datos provienen del sistema ERP y los datos se almacenan en una base de datos ADLS Gen2. Se actualiza a mediodía/12:00 todos los días.
- Datos de proveedores: estos datos provienen de diferentes proveedores y se almacenan en una base de datos de Snowflake. Se actualiza a medianoche/00:00 todos los días.
- Datos del cliente: estos datos provienen de Customer Insights y se almacenan en Dataverse. Los datos siempre están actualizados.
- Datos de los empleados: estos datos provienen del sistema de recursos humanos; se almacenan como un archivo de exportación en una carpeta de SharePoint. Se actualiza a todas las mañanas a las 9:00. 

![](../media/lab-01/main1.png)

Actualmente está creando un conjunto de datos en Power BI Premium que extrae los datos de los sistemas de origen anteriores para satisfacer sus necesidades de informes y ofrecer a los usuarios finales la capacidad de autoservicio. Use Power Query para actualizar su modelo. 
