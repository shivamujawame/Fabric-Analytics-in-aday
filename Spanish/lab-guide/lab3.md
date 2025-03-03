# Microsoft Fabric Fabric Analyst in a Day - Laboratorio 3

![](../media/lab-03/main3.png)

# Contenido
- Presentación
- Acceso directo a ADLS Gen2
    - Tarea 1: Crear acceso directo
- Transformar datos mediante una consulta visual
    - Tarea 2: Crear una vista Geo con consultas visuales
    - Tarea 3: Crear una vista Reseller con consultas visuales
    - Tarea 4: Crear una vista Sales con consultas visuales
    - Tarea 5: Crear una vista de producto con consultas visuales
- Referencias

# Presentación 

En nuestro escenario, los Datos de Sales provienen del sistema ERP y se
almacenan en ADLS Gen2. Se actualiza a mediodía/12:00 todos los días.
Necesitamos transformar e ingerir estos datos en un almacén de lago de
datos y usarlos en nuestro modelo.

Hay varias formas de ingerir estos datos.

- **Accesos directos:** esto crea un vínculo con los datos, y podemos
    utilizar las vistas de consulta Visual para transformarlos. Usaremos
    accesos directos en este laboratorio.

- **Notebooks:** esto requiere que escribamos código. Es un enfoque
    amigable para los desarrolladores.

- **Flujo de datos Gen2:** probablemente esté familiarizado con Power
    Query o el flujo de datos de primera generación. El flujo de datos
    Gen2, como su nombre indica, es la versión más nueva del flujo de
    datos. Proporciona todas las capacidades de Power Query y el flujo
    de datos de primera generación con la capacidad adicional de
    transformar e ingerir datos en múltiples orígenes de datos.
    Presentaremos esto en los próximos laboratorios.

- **Canalización de datos:** esta es una herramienta de orquestación.
    Se pueden orquestar actividades para extraer, transformar e ingerir
    datos. Usaremos la canalización de datos para ejecutar la actividad
    del flujo de datos Gen2, que, a su vez, hará la extracción,
    transformación e ingestión.

Comenzaremos creando un acceso directo para ingerir datos en un almacén
de lago de datos desde el origen de datos de ADLS Gen2. Una vez
ingeridos, usaremos vistas de consulta visual para transformarlos.

Al final de este laboratorio, habrá aprendido sobre:

- Cómo crear accesos directos en el almacén de lago de datos

- Cómo transformar datos mediante la característica de consulta visual

# Acceso directo a ADLS Gen2

### Tarea 1: Crear acceso directo

Los accesos directos se utilizan para crear un vínculo a la ubicación de
destino. Los accesos directos proporcionan acceso a los datos sin
necesidad de mover físicamente los datos al almacén de lago de datos.
Esto es como crear accesos directos en el escritorio de Windows.

1. Volvamos al **área de trabajo de Fabric** **(1)** que creó en el
    Laboratorio 2, Tarea 2.

2. Si no ha salido de la práctica de laboratorio anterior, estará en la
    pantalla del almacén de lago de datos. Si ha salido, no pasa nada.
    Seleccione **lh_FAIAD** (**2)** para ir al almacén de lago de datos.

3. En el panel del **explorador** de la izquierda, seleccione los
    **puntos suspensivos (3)** al lado de las **Tables**.

4. Seleccione **Nuevo acceso directo (4).**

   ![](../media/lab-03/image6.png)

5. Se abre el cuadro de diálogo **Nuevo acceso directo**. En **Orígenes
    externos**, seleccione **Azure Data Lake Storage Gen2**.

   ![](../media/lab-03/image7.png)

6. Seleccione **Creación de una conexión (1)**.

7. Escriba el siguiente vínculo para la propiedad **URL**: `https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales` **(2)**

8. Seleccione **Firma de acceso compartido (SAS) (3)** en el menú
    desplegable Tipo de autenticación.

9. Copie el token de SAS y péguelo en el campo Token de SAS (4).

    - **Token de SAS:** <inject key="Sas token"></inject>

10. Seleccione **Siguiente (5)** en la esquina inferior derecha de la
    pantalla.

    ![](../media/lab-03/image8.png)

11. Se conectará a ADLS Gen2 con la estructura de directorios que se
    muestra en el panel izquierdo. Expanda **Delta-Parquet-Format-FY25
    (1).**

12. **Seleccione** los siguientes directorios **(2)** y luego haga clic
    en **Siguiente (3):**

    a. Application.Cities

    b. Application.Countries

    c. Application.StateProvinces

    d. DateDim

    e. Sales.BuyingGroups

    f. Sales.Customers

    g. Sales.InvoiceLines

    h. Sales.Invoices

    i. Warehouse.StockGroups

    j. Warehouse.StockItemStockGroups

    k. Warehouse.StockItems

    **Nota:** Sales.Invoices_May es el único directorio que **no** está
    seleccionado.

    ![](../media/lab-03/image9.png)

13. Se le dirigirá al siguiente cuadro de diálogo, donde podemos editar
    los nombres. Seleccione el **icono Editar (1)** en Acciones para
    **Application.Cities**.

14. Cambie el nombre de **Application.Cities a Cities (2).**

15. Seleccione la marca de verificación al lado del nombre para guardar
    el cambio **(3)**.

    ![](../media/lab-03/image10.png)

16. Del mismo modo, cambie el nombre de los nombres de acceso directo
    como se muestra a continuación:

    a. Application.Countries a **Countries**

    b. Application.StateProvinces a **States**

    c. DateDim a **Date**

    d. Sales.BuyingGroups a **BuyingGroups**

    e. Sales.Customers a **Customers**

    f. Sales.InvoiceLines a **InvoiceLineItems**

    g. Sales.Invoices a **Invoices**

    h. Warehouse.StockGroups a **ProductGroups**

    i. Warehouse.StockItemStockGroups a **ProductItemGroup**

    j. Warehouse.StockItems a **ProductItem**

    > **Nota**: Compruebe dos veces los nombres. Un error tipográfico puede causar errores durante el laboratorio.

17. Seleccione **Crear** para crear el acceso directo.

    ![](../media/lab-03/image11.png)

18. Observe que todos los accesos directos se crean como tablas.
    Seleccione la tabla **BuyingGroups** y observe que podemos ver una
    versión preliminar de los datos en el panel de datos.

    ![](../media/lab-03/image12.png)

El siguiente paso es transformar los datos, para que podamos crear un
modelo semántico. Vamos a crear vistas para transformar los datos.

# Transformar datos mediante una consulta visual

### Tarea 2: Crear una vista Geo con consultas visuales

1. Podemos tener acceso al almacén de lago de datos mediante un punto
    de conexión SQL. Esto permite consultar los datos y crear vistas. En
    la **parte superior derecha** de la pantalla, seleccione
    **Lakehouse (1) -\> Punto de conexión de análisis SQL (2)**.

   ![](../media/lab-03/image13.png)

    Esto le llevará al punto de conexión de análisis de SQL. Observe que el
    panel del Explorador ha cambiado. Ahora puede crear vistas,
    procedimientos almacenados, consultas y mucho más. Vamos a crear una
    consulta visual, ya que proporciona una interfaz similar a Power Query
    con poco código. Guardaremos el resultado como una vista.

    Comenzaremos creando una vista Geo. Necesitamos fusionar los datos de
    las tablas Cities, States y Countries para crear la vista Geo.

2. En el menú principal, haga clic en el menú desplegable junto a
    **Nueva consulta SQL (1)** y, a continuación, seleccione **Nueva
    consulta visual (2)**.

   ![](../media/lab-03/image14.png)

3. Para crear una consulta, tendremos que agregar tablas al panel
    Consulta de objeto visual. Haga clic en los puntos suspensivos junto
    a la tabla **Cities (1)** y seleccione **Insertar en el lienzo
    (2).**

   ![](../media/lab-03/image15.png)

4. Repita los mismos pasos para las tablas **States** y **Countries**.

    A continuación, necesitamos fusionar estas consultas. El editor de
    consultas visual viene con la opción de usar el Editor de Power Query.
    Usemos esto, ya que estamos familiarizados con esto.

5. En el menú del editor de consultas visuales, seleccione el icono
    **Abrir en menú emergente** (hacia la derecha). Se le llevará al
    Editor de Power Query.

   ![](../media/lab-03/image16.png)

6. Con la consulta Cities seleccionada (1), en la cinta del Editor de
    Power Query, seleccione **Inicio (2) - \> Combinar (3) -\> Menú
    desplegable Combinar consultas (4) -\> Combinar consultas como
    nuevas (5)**. Se abrirá el cuadro de diálogo Combinar consultas.

   ![](../media/lab-03/image17.png)

7. En la **Tabla izquierda para combinación**, seleccione **Cities**.

8. En la **Tabla derecha para combinación**, seleccione **States**.

9. Seleccione las columnas **StateProvinceID** de ambas tablas. Vamos a
    unirnos usando esta columna.

10. Seleccione **Interior** como el **Tipo de combinación**.

11. Seleccione **Aceptar**.

    ![](../media/lab-03/image18.png)

    Observe que se ha creado una nueva consulta llamada Merge. Necesitamos
    algunas columnas de States.

12. En la **vista Datos** (panel inferior), haga clic en la **doble
    flecha** al lado de la columna **States** (última columna a la
    derecha).

13. Se abre un panel. **Seleccione** las siguientes columnas:

    a. StateProvinceCode

    b. StateProvinceName

    c. CountryID

    d. SalesTerritory

14. Seleccione **Aceptar**.

    ![](../media/lab-03/image19.png)

    Necesitamos fusionar la consulta Countries ahora.

15. Con la consulta de combinación seleccionada (1), seleccione
    **Inicio (2) -\> Combinar (3) -\> Menú desplegable Combinar
    consultas (4) -\> Combinar consultas (5)**.

    ![](../media/lab-03/image20.png)

16. Se abrirá el cuadro de diálogo Combinar consulta. En la **Tabla
    derecha para combinación**, seleccione **Countries**.

17. Seleccione las columnas **CountryID** de ambas tablas. Vamos a
    unirnos usando esta columna.

18. Seleccione **Interior** como el **Tipo de combinación**.

19. Seleccione **Aceptar**.

    ![](../media/lab-03/image21.png)

    Necesitamos algunas columnas de Countries.

20. En el panel **vista Datos** (panel inferior), haga clic en la
    **doble flecha** al lado de la columna **Countries**.

21. Se abre un panel. **Seleccione** las siguientes columnas:

    a. CountryName

    b. FormalName

    c. IsoAlpha3Code

    d. IsoNumericCode

    e. CountryType

    f. Continent

    g. Region

    h. Subregion

22. Seleccione **Aceptar**.

    ![](../media/lab-03/image22.png)

    No necesitamos todas las columnas. Asegúrese de seleccionar solo las que
    necesitemos.

23. Con la consulta de combinación seleccionada, en la cinta de opciones
    seleccione **Inicio -\> Elegir columnas -\> Elegir columnas**.

    **Nota:** Si la opción Elegir columnas no está visible, puede
    encontrarla en Administrar columnas.

    ![](../media/lab-03/image23.png)

24. Se abrirá el cuadro de diálogo Elegir columnas. **Desmarque** las
    siguientes columnas.

    a. StateProvinceID

    b. Location

    c. LastEditedBy

    d. ValidFrom

    e. ValidTo

    f. CountryID

25. Seleccione **Aceptar**.

    ![](../media/lab-03/image24.png)

    Observe que el proceso es como el de Power Query, tenemos todos los
    pasos registrados tanto en el panel Pasos aplicados de la derecha como
    en la vista visual. Vamos a cambiar el nombre de Combinar consulta a
    Habilitar carga de modo que se carguen los datos desde esta consulta.

26. **Haga clic con el botón derecho** en la consulta **Combinar** en el
    panel Consultas (izquierda). Seleccione **Cambiar nombre** y cambie
    el nombre de la consulta a **Geo**.

27. **Haga clic con el botón derecho** en la consulta **Geo** en el
    panel Consultas (izquierdo). Seleccione **Habilitar carga** para
    habilitar esta consulta.

28. Asegúrese de que las consultas de Cities, States y Countries estén
    **deshabilitadas**.

29. Seleccione **Guardar**, que se encuentra en la parte inferior
    derecha del editor de Power Query.

    ![](../media/lab-03/image25.png)
   
    Se nos dirigirá al editor de consultas visuales. Guardemos ahora esta
    consulta como una vista.

    > **Nota**: Todos los pasos que hemos realizado con el Editor de Power Query también se pueden llevar a cabo con el editor de consultas visuales.

30. En el menú del editor de consultas visuales, seleccione **Guardar
    como copia**.

    ![](../media/lab-03/image26.png)

    Se abre el cuadro de diálogo Guardar como copia. Observe que la consulta
    SQL está disponible. Si quiere revisar la SQL, puede hacerlo.

31. Escriba **Geo** como **Nombre de la vista**.

32. Seleccione **Aceptar** para guardar la vista.

    ![](../media/lab-03/image27.png)

    Recibirá una alerta una vez que se guarde la vista.

33. En el panel Explorador (izquierda), expanda **Views.** Tenemos la
    vista Geo recién creada.

    ![](../media/lab-03/image28.png)

### Tarea 3: Crear una vista Reseller con consultas visuales

Vamos a crear una vista Reseller, que se crea al combinar la tabla
Customers con la tabla BuyingGroups. Esta vez crearemos la vista
mediante la consulta Visual.

1. En el menú principal, haga clic en el menú desplegable junto a
    **Nueva consulta SQL (1)** y, a continuación, seleccione **Nueva
    consulta visual (2)**.

2. Para crear una consulta, tendremos que agregar tablas al panel
    Consulta de objeto visual. Haga clic en los puntos suspensivos junto
    a la tabla **BuyingGroups (1)** y seleccione **Insertar en el lienzo
    (2)**.

   ![](../media/lab-03/image29.png)

3. Repita los mismos pasos para la tabla **Customers**.

4. **Seleccione la consulta Customers**. Cuando se selecciona,
    Customers tendrá un borde azul y hay un signo \"**+\"** después de
    Tabla (esto indica que estamos agregando un paso después de Tabla.
    Si no ve el signo **\"+\"** después de la tabla, es posible que haya
    seleccionado un paso diferente. Seleccione Tabla y estará listo).

5. En el menú Consulta visual, seleccione **Combinar -\> Combinar
    consultas**.

   ![](../media/lab-03/image30.png)

    Se abre el cuadro de diálogo Combinar con Customers seleccionado como la
    tabla superior.

6. En la **Tabla derecha para combinación**, seleccione
    **BuyingGroups**.

7. Seleccione las columnas **BuyingGroupID** de ambas tablas. Vamos a
    unirnos usando esta columna.

8. Seleccione **Interior** como el **Tipo de combinación**.

9. Seleccione **Aceptar**.

   ![](../media/lab-03/image31.png)

10. En la **Vista de datos** (panel inferior), haga clic en la **doble
    flecha** al lado de la columna **BuyingGroups** (última columna a la
    derecha) para seleccionar las columnas que necesitamos de
    BuyingGroups.

11. Se abre un panel. **Seleccione la columna** **BuyingGroupName**.

12. Seleccione **Aceptar**.

    ![](../media/lab-03/image32.png)

    No necesitamos todas las columnas. Seleccione solo aquellos que
    necesitamos.

13. En el menú Consulta visual, seleccione **Administrar columnas -\>
    Elegir columnas**.

    ![](../media/lab-03/image33.png)

14. Se abrirá el cuadro de diálogo Elegir columnas. **Seleccione** las siguientes columnas.

    a. ResellerID

    b. ResellerName

    c. PostalCityID

    d. PhoneNumber

    e. FaxNumber

    f. WebsiteURL

    g. DeliveryAddressLine1

    h. DeliveryAddressLine2

    i. DeliveryPostalCode

    j. PostalAddressLine1

    k. PostalAddressLine2

    l. PostalPostalCode

    m. BuyingGroupName

15. Seleccione **Aceptar**.

    ![](../media/lab-03/image34.png)

16. Vamos a cambiar el nombre de la columna BuyingGroupName. En la
    **vista Datos, haga doble clic en el encabezado de columna
    BuyingGroupName** para hacer que sea editable.

17. **Cambie el nombre** de la columna a **ResellerCompany**.

    ![](../media/lab-03/image35.png)

    Observe que la tabla Customer tiene todos los pasos documentados. Ahora
    guardemos esta vista.

18. Necesitamos guardar la consulta Customer, ya que tiene todos los
    pasos. Necesitamos habilitar la carga. Seleccione los **puntos
    suspensivos** en el cuadro de consulta **Customer**.

19. Asegúrese de que la opción **Habilitar carga** esté activada.

    ![](../media/lab-03/image36.png)

    **Nota**: La casilla **Customer** debe tener un borde azul si se activa
    la opción Habilitar carga.

20. En el menú de consultas visuales, seleccione **Guardar como copia**.

    ![](../media/lab-03/image37.png)

    Se abre el cuadro de diálogo Guardar como copia. Observe que la consulta
    SQL está disponible. Puede revisarlo, si así lo desea.

21. Escriba **Reseller** como **Nombre de la vista**.

22. Seleccione **Aceptar** para guardar la vista.

    ![](../media/lab-03/image38.png)

    Recibirá una alerta una vez que se guarde la vista.

23. En el panel Explorador (izquierda), expanda **Views.** Tenemos la
    vista Reseller recién creada.

    ![](../media/lab-03/image39.png)

### Tarea 4: Crear una vista Sales con consultas visuales

Vamos a crear la vista Sales, que se crea combinando las tablas
InvoiceLineItems e Invoices con la vista Reseller. Tenemos esta consulta
en Power BI Desktop. Copiaremos el código del Editor avanzado. Pero
antes de copiar el código, necesitamos crear una tabla de fusión
utilizando Visual query ya que crear una consulta en blanco no es
posible en la consulta visual. Vamos a probar este método.

1. En el menú principal, haga clic en el menú desplegable junto a
    **Nueva consulta SQL** y, a continuación, seleccione **Nueva
    consulta visual**.

   ![](../media/lab-03/image40.png)

2. En la sección **Explorador -\> Table**, tenemos que agregar las
    tablas al panel de la consulta visual. Haga clic en los puntos
    suspensivos junto a la tabla **InvoiceLineItems** y seleccione
    **Insertar en lienzo**.

3. Repita los mismos pasos para la tabla **Invoices**.

4. En la sección **Explorador -\> Vistas**, tenemos que agregar las
    tablas al panel de la consulta visual. Haga clic en los puntos
    suspensivos junto a la tabla **Reseller** y seleccione **Insertar en
    lienzo**.

5. En el editor de consultas visuales, seleccione **Abrir en ventana
    emergente** para abrir el Editor de Power Query.

   ![](../media/lab-03/image41.png)

6. Con la consulta **InvoiceLineItems** seleccionada, en la cinta de
    opciones, seleccione **Inicio (2) - \> Combinar (3) -\> Menú
    desplegable Combinar consultas (4) -\> Combinar consultas como
    nuevas (5).** Se abrirá el cuadro de diálogo Combinar consultas.

   ![](../media/lab-03/image42.png)

7. En **Tabla izquierda para combinación**, seleccione
    **InvoiceLineItems**.

8. En la **Tabla derecha para combinación**, seleccione **Invoices**.

9. Seleccione las columnas **InvoiceID** de ambas tablas. Vamos a
    unirnos usando esta columna.

10. Seleccione **Interior** como el **Tipo de combinación**.

11. Seleccione **Aceptar**.

    ![](../media/lab-03/image43.png)

    Vamos a copiar el código de Power BI Desktop y pegarlo con el Editor
    avanzado.

12. Si aún no lo ha abierto, abra **FAIAD.pbix**, que se encuentra en la
    carpeta **Reports** en el escritorio de su entorno de laboratorio.

13. En la cinta de opciones, seleccione **Inicio -\> Transformar
    datos**. Se abre la ventana de Power Query. Como habrá notado en la
    práctica de laboratorio anterior, las consultas en el panel
    izquierdo están organizadas por orígenes de datos.

    ![](../media/lab-03/image44.png)

14. En el panel izquierdo **Consultas**, en la carpeta **ADLSData**
    **(1)**, seleccione la consulta **Sales (2).**

15. En la cinta de opciones, seleccione **Inicio -\> Editor avanzado
    (3)**. Se abre el cuadro de diálogo del Editor avanzado.

    ![](../media/lab-03/image45.png)

    > **Nota:** Si no encuentra el Editor avanzado, puede acceder a él en **Inicio -\> Consulta -\> Editor avanzado**.

16. **Seleccione el código de la Línea 3** (#\"Expanded Invoice\" ...) hasta la última línea de código.

17. **Haga clic con el botón derecho** y seleccione **Copy**.

18. Seleccione **Cancelar** para cerrar el Editor avanzado.

    ![](../media/lab-03/image46.png)

19. **Regrese a la ventana/pestaña del navegador** donde tiene abierto
    el Editor de Power Query.

20. Asegúrese de que se ha seleccionado la consulta **Combinar**.

21. En la cinta de opciones, seleccione **Inicio -\> Editor avanzado**.
    Se abre el cuadro de diálogo del Editor avanzado.

    ![](../media/lab-03/image47.png)

22. Al final de la **línea 2 agregue una coma** (Source =
    Table.NestedJoin(InvoiceLineItems, {\"InvoiceID\",
    Invoices,}\"InvoiceID\" {}, \"Invoices\", JoinKind.Inner)

23. Haga clic en **Entrar** para empezar una nueva línea.

24. Introduzca **Ctrl+V** en el teclado para pegar el código que Power BI Desktop ha copiado.

    > **Nota**: Si está trabajando en el entorno de laboratorio, seleccione los **puntos suspensivos (...)** en la parte superior derecha de la pantalla. Utilice el control deslizante para **habilitar** **Portapapeles nativo de VM**. Seleccione De acuerdo en el cuadro de diálogo. Una vez que haya terminado de pegar las consultas, puede desactivar esta opción.

    ![](../media/lab-03/image48.png)

    ![](../media/lab-03/image49.png)

25. Resalte las dos últimas líneas de código (en Origen) y
    **elimínelas**.

26. Seleccione **Aceptar** para guardar las modificaciones.

    ![](../media/lab-03/image50.png)

    Si resulta más fácil, elimine todo el código del Editor avanzado y pegue
    el siguiente código en el Editor avanzado.

    ```
    let
      Source = Table.NestedJoin(InvoiceLineItems, {"InvoiceID"}, Invoices, {"InvoiceID"}, "Invoices", JoinKind.Inner),
        #"Expanded Invoice" = Table.ExpandTableColumn(Source, "Invoices", {"CustomerID", "BillToCustomerID", "SalespersonPersonID", "InvoiceDate"}, {"CustomerID", "BillToCustomerID", "SalespersonPersonID", "InvoiceDate"}),
        #"Removed Other Columns" = Table.SelectColumns(#"Expanded Invoice",{"InvoiceLineID", "InvoiceID", "StockItemID", "Quantity", "UnitPrice", "TaxRate", "TaxAmount", "LineProfit", "ExtendedPrice", "CustomerID", "SalespersonPersonID", "InvoiceDate"}),
        #"Renamed Columns" = Table.RenameColumns(#"Removed Other Columns",{{"CustomerID", "ResellerID"}}),
        #"Merged Queries" = Table.NestedJoin(#"Renamed Columns", {"ResellerID"}, Reseller, {"ResellerID"}, "Customer", JoinKind.Inner),
        #"Added Custom" = Table.AddColumn(#"Merged Queries", "Sales Amount", each [ExtendedPrice] - [TaxAmount]),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Sales Amount", type number}}),
        #"Removed Columns" = Table.RemoveColumns(#"Changed Type",{"Customer"})
    in
        #"Removed Columns"
    ```

27. Se le llevará de vuelta al Editor de Power Query. En el panel de
    consultas izquierdo, **haga doble clic en Combinar** consulta para
    cambiar su nombre.

28. **Cambie el nombre** de la consulta de combinación a **Sales**.

29. Haga clic con el botón derecho en la consulta de Sales y seleccione
    **Habilitar carga** para permitir que se cargue la consulta.

    ![](../media/lab-03/image51.png)

30. Seleccione **Guardar** para guardar y cerrar el cuadro de diálogo de
    Power Query. Se le dirigirá al editor de consultas visuales.

31. En el menú de consultas visuales, seleccione **Guardar como copia**.
    Se abre el cuadro de diálogo Guardar como copia. Observe que la
    consulta SQL está disponible. Puede revisarlo, si así lo desea.

32. Escriba **Sales** como **Nombre de vista (1)**.

33. Seleccione **Aceptar (2)** para guardar la vista.

    ![](../media/lab-03/image52.png)

    Recibirá una alerta una vez que se guarde la vista.

34. En el panel Explorador (izquierda), expanda **Views.** Tenemos la
    vista Sales recién creada.

    ![](../media/lab-03/image53.png)

### Tarea 5: Crear una vista de producto con consultas visuales

Vamos a crear la vista Producto, que se crea mediante la combinación de
las tablas **ProductItem**, **ProductItemGroup** y **ProductGroups**.
Para avanzar en las cosas, copiaremos el código en el Editor avanzado.

1. En el menú principal, haga clic en el menú desplegable junto a
    **Nueva consulta SQL (1)** y, a continuación, seleccione **Nueva
    consulta visual (2)**.

   ![](../media/lab-03/image14.png)

2. En la sección Explorador, tenemos que agregar las tablas al panel de
    la consulta visual. Haga clic en los puntos suspensivos junto a la
    tabla **ProductItem (1)** y seleccione **Insertar en el lienzo
    (2)**.

   ![](../media/lab-03/image54.png)

3. Repita los mismos pasos para las tablas **ProductItemGroup** y
    **ProductGroups**.

4. En el editor de consultas visuales, seleccione el **icono de modo de
    enfoque** para abrir el Editor de Power Query.

   ![](../media/lab-03/image55.png)

5. Con la consulta **ProductItem** seleccionada, en la cinta de
    opciones, seleccione **Inicio (1) - \> Combinar (2) -\> Menú
    desplegable Combinar consultas (3) -\> Combinar consultas como
    nuevas (4).** Se abrirá el cuadro de diálogo Combinar.

   ![](../media/lab-03/image56.png)

6. En la **Tabla izquierda para combinación**, seleccione
    **ProductItem**.

7. En la **Tabla derecha para combinación**, seleccione
    **ProductItemGroup**.

8. Seleccione las columnas **StockItemID** de ambas tablas. Vamos a
    unirnos usando esta columna.

9. Seleccione **Externa izquierda** como **Tipo de combinación**.

10. Seleccione **Aceptar.** Se crea la nueva consulta de combinación.

    ![](../media/lab-03/image57.png)

11. Con la consulta de combinación seleccionada, en la cinta de
    opciones, seleccione **Inicio -\> Editor avanzado**. Se abre el
    cuadro de diálogo del Editor avanzado.

    ![](../media/lab-03/image58.png)

    > **Nota:** Si no encuentra el Editor avanzado, puede acceder a él en **Inicio -\> Consulta -\> Editor avanzado**.

12. **Seleccione todo el código** en el Editor avanzado y **elimínelo**.

13. **Pegue** el código siguiente en el Editor avanzado.

    ```
    let
       Source = Table.NestedJoin(ProductItem, {"StockItemID"}, ProductItemGroup, {"StockItemID"}, "ProductItemGroup", JoinKind.LeftOuter),
       #"Expanded ProductItemGroup" = Table.ExpandTableColumn(Source, "ProductItemGroup", {"StockGroupID"}, {"StockGroupID"}),
       #"Merged queries" = Table.NestedJoin(#"Expanded ProductItemGroup", {"StockGroupID"}, ProductGroups, {"StockGroupID"}, "ProductGroups", JoinKind.LeftOuter),
       #"Expanded ProductGroups" = Table.ExpandTableColumn(#"Merged queries", "ProductGroups", {"StockGroupName"}, {"StockGroupName"}),
       #"Choose columns" = Table.SelectColumns(#"Expanded ProductGroups", {"StockItemID", "StockItemName", "SupplierID", "Size", "IsChillerStock", "TaxRate", "UnitPrice", "RecommendedRetailPrice", "TypicalWeightPerUnit", "StockGroupName"})
    in
       #"Choose columns"
    ```

14. Seleccione **Aceptar** para cerrar el Editor avanzado. Se le llevará
    de vuelta al Editor de Power Query.

    ![](../media/lab-03/image59.png)

15. En el panel Consultas izquierdo, **haga doble clic en Combinar**
    consulta para cambiar su nombre.

16. **Cambie el nombre** de la consulta de combinación a **Product**.

17. Haga clic con el botón derecho en la consulta de Product y
    seleccione **Habilitar carga** para permitir que se cargue la
    consulta.

18. Seleccione **Guardar** para guardar y cerrar el cuadro de diálogo de
    Power Query. Esto le llevará a la consulta visual.

    ![](../media/lab-03/image60.png)

19. En el menú de consultas visuales, seleccione **Guardar como copia**.
    Se abre el cuadro de diálogo Guardar como copia. Observe que la
    consulta SQL está disponible. Puede revisarlo, si así lo desea.

20. Escriba **Product** como **Nombre de la vista**.

21. Seleccione **Aceptar** para guardar la vista.

    ![](../media/lab-03/image61.png)

    Recibirá una alerta una vez que se guarde la vista.

22. En el panel Explorador (izquierda), expanda **Views.** Tenemos la
    vista Product recién creada.

    ![](../media/lab-03/image62.png)

Hemos transformado los datos del origen de datos ADLS Gen2. En este
laboratorio, hemos aprendido a crear accesos directos y hemos explorado
diversas opciones para usar vistas de consulta visual para transformar
datos.

En la siguiente práctica de laboratorio, aprenderemos a usar el flujo de
datos Gen2 y a crear un acceso directo a otro almacén de lago de datos.

# Referencias

Fabric Analyst in a Day (FAIAD) le presenta algunas funciones clave disponibles en Microsoft Fabric. En el menú del servicio, la sección Ayuda (?) tiene vínculos a algunos recursos excelentes.

![](../media/lab-01/image28.png)

Estos son algunos recursos más que podrán ayudarle a seguir avanzando
con Microsoft Fabric.

- Vea la publicación del blog para leer el [anuncio de disponibilidad general de Microsoft Fabric](https://aka.ms/Fabric-Hero-Blog-Ignite23) completo.

- Explore Fabric a través de la [Visita guiada](https://aka.ms/Fabric-GuidedTour)

- Regístrese en la [prueba gratuita de Microsoft Fabric](https://aka.ms/try-fabric)

- Visite el [sitio web de Microsoft Fabric](https://aka.ms/microsoft-fabric)

- Adquiera nuevas capacidades mediante la exploración de los [módulos de aprendizaje de Fabric](https://aka.ms/learn-fabric)

- Explore la [documentación técnica de Fabric](https://aka.ms/fabric-docs)

- Lea el [libro electrónico gratuito sobre cómo empezar a usar Fabric](https://aka.ms/fabric-get-started-ebook)

- Únase a la [comunidad de Fabric](https://aka.ms/fabric-community) para publicar sus preguntas, compartir sus comentarios y aprender de otros.

Obtenga más información en los blogs de anuncios de la experiencia
Fabric:

- [Experiencia de Data Factory en el blog de Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Experiencia de Synapse Data Engineering en el blog de Fabric](https://aka.ms/Fabric-DE-Blog)

- [Experiencia de Synapse Data Science en el blog de Fabric](https://aka.ms/Fabric-DS-Blog)

- [Experiencia de Synapse Data Warehousing en el blog de Fabric](https://aka.ms/Fabric-DW-Blog)

- [Experiencia de Synapse Real-Time Analytics en el blog de Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog de anuncios de Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Experiencia de Data Activator en el blog de Fabric](https://aka.ms/Fabric-DA-Blog)

- [Administración y gobernanza en el blog de Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake en el blog de Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog de integración de Dataverse y Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2025 Microsoft Corporation. Todos los derechos reservados.

Al participar en esta demostración o laboratorio práctico, acepta las siguientes condiciones:

Microsoft Corporation pone a su disposición la tecnología o funcionalidad descrita en esta demostración/laboratorio práctico con el fin de obtener comentarios por su parte y de facilitarle una experiencia de aprendizaje. Esta demostración/laboratorio práctico solo se puede usar para evaluar las características de tal tecnología o funcionalidad y para proporcionar comentarios a Microsoft. No se puede usar para ningún otro propósito. Ninguna parte de esta demostración/laboratorio práctico se puede modificar, copiar, distribuir, transmitir, mostrar, realizar, reproducir, publicar, licenciar, transferir ni vender, ni tampoco crear trabajos derivados de ella.

LA COPIA O REPRODUCCIÓN DE ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO (O PARTE DE ELLA) EN CUALQUIER OTRO SERVIDOR O UBICACIÓN PARA SU REPRODUCCIÓN O DISTRIBUCIÓN POSTERIOR QUEDA EXPRESAMENTE PROHIBIDA.

ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO PROPORCIONA CIERTAS FUNCIONES Y CARACTERÍSTICAS DE PRODUCTOS O TECNOLOGÍAS DE SOFTWARE (INCLUIDOS POSIBLES NUEVOS CONCEPTOS Y CARACTERÍSTICAS) EN UN ENTORNO SIMULADO SIN INSTALACIÓN O CONFIGURACIÓN COMPLEJA PARA EL PROPÓSITO ARRIBA DESCRITO. LA TECNOLOGÍA/CONCEPTOS DESCRITOS EN ESTA DEMOSTRACIÓN/LABORATORIO PRÁCTICO NO REPRESENTAN LA FUNCIONALIDAD COMPLETA DE LAS CARACTERÍSTICAS Y, EN ESTE SENTIDO, ES POSIBLE QUE NO FUNCIONEN DEL MODO EN QUE LO HARÁN EN UNA VERSIÓN FINAL. ASIMISMO, PUEDE QUE NO SE PUBLIQUE UNA VERSIÓN FINAL DE TALES CARACTERÍSTICAS O CONCEPTOS. DE IGUAL MODO, SU EXPERIENCIA CON EL USO DE ESTAS CARACTERÍSTICAS Y FUNCIONALIDADES EN UN ENTORNO FÍSICO PUEDE SER DIFERENTE.

**COMENTARIOS**. Si envía comentarios a Microsoft sobre las características, funcionalidades o conceptos de tecnología descritos en esta demostración/laboratorio práctico, acepta otorgar a Microsoft, sin cargo alguno, el derecho a usar, compartir y comercializar sus comentarios de cualquier modo y para cualquier fin. También concederá a terceros, sin cargo alguno, los derechos de patente necesarios para que sus productos, tecnologías y servicios usen o interactúen con cualquier parte específica de un software o servicio de Microsoft que incluya los comentarios. No enviará comentarios que estén sujetos a una licencia que obligue a Microsoft a conceder su software o documentación bajo licencia a terceras partes porque incluyamos sus comentarios en ellos. Estos derechos seguirán vigentes después del vencimiento de este acuerdo.

MICROSOFT CORPORATION RENUNCIA POR LA PRESENTE A TODAS LAS GARANTÍAS Y CONDICIONES RELATIVAS A LA DEMOSTRACIÓN/LABORATORIO PRÁCTICO, INCLUIDA CUALQUIER GARANTÍA Y CONDICIÓN DE COMERCIABILIDAD (YA SEA EXPRESA, IMPLÍCITA O ESTATUTARIA), DE IDONEIDAD PARA UN FIN DETERMINADO, DE TITULARIDAD Y DE AUSENCIA DE INFRACCIÓN. MICROSOFT NO DECLARA NI GARANTIZA LA EXACTITUD DE LOS RESULTADOS, EL RESULTADO DERIVADO DE LA REALIZACIÓN DE LA DEMOSTRACIÓN/LABORATORIO PRÁCTICO NI LA IDONEIDAD DE LA INFORMACIÓN CONTENIDA EN ELLA CON NINGÚN PROPÓSITO.

**DECLINACIÓN DE RESPONSABILIDADES**

Esta demostración/laboratorio práctico contiene solo una parte de las nuevas características y mejoras realizadas en Microsoft Power BI. Puede que algunas de las características cambien en versiones futuras del producto. En esta demostración/laboratorio práctico, conocerá algunas de estas nuevas características, pero no todas.

