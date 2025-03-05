#  {#section .TOC-Heading}

> Microsoft Fabric
>
> Fabric Analyst in a Day
>
> 实验室 0

Microsoft Fabric Fabric Analyst in a Day

实验室 3

版本：2025 年 2 月

> 实验室 0

# 目录 {#目录 .TOC-Heading}

[简介 [3](#简介)](#简介)

[ADLS Gen2 的快捷方式 [3](#adls-gen2-的快捷方式)](#adls-gen2-的快捷方式)

[任务 1：创建快捷方式 [3](#任务-1创建快捷方式)](#任务-1创建快捷方式)

[使用视觉对象查询转换数据
[9](#使用视觉对象查询转换数据)](#使用视觉对象查询转换数据)

[任务 2：使用视觉对象查询创建 Geo 视图
[9](#任务-2使用视觉对象查询创建-geo-视图)](#任务-2使用视觉对象查询创建-geo-视图)

[任务 3：使用视觉对象查询创建 Reseller 视图
[18](#任务-3使用视觉对象查询创建-reseller-视图)](#任务-3使用视觉对象查询创建-reseller-视图)

[任务 4：使用视觉对象查询创建 Sales 视图
[24](#任务-4使用视觉对象查询创建-sales-视图)](#任务-4使用视觉对象查询创建-sales-视图)

[任务 5：使用视觉对象查询创建 Product 视图
[32](#任务-5使用视觉对象查询创建-product-视图)](#任务-5使用视觉对象查询创建-product-视图)

[参考 [38](#参考)](#参考)

# 

# 

# 

# 

# 

# 

# 

# 

# 简介

在我们的应用场景中，销售数据来自 ERP 系统，存储在 ADLS Gen2 中。每天中午
12
点更新。我们需要将此数据转换并引入到湖屋中，并在我们的模型中使用此数据。

可通过多种方法引入此数据。

-   **快捷方式：**这将创建指向数据的链接，我们可以使用视觉对象查询视图来转换它。我们将在本实验室中使用快捷方式。

-   **笔记本：**这需要我们编写代码。这种方法适合开发人员。

-   **数据流 Gen2：**您可能熟悉 Power Query 或数据流 Gen1。数据流 Gen2
    顾名思义是数据流的新版本。它提供 Power Query/数据流 Gen1
    的所有功能，并添加了将数据转换和引入到多个数据源的功能。我们将在下面几个实验室中进行介绍。

-   **数据管道：**这是一个编排工具。可以编排活动来提取、转换和引入数据。我们将使用数据管道执行数据流
    Gen2 活动，该活动又将执行提取、转换和引入。

我们将首先创建一个快捷方式，以将数据从 ADLS Gen2
数据源引入到湖屋中。引入后，我们将使用视觉对象查询视图来转换它。

在本实验室结束时，您将了解到：

-   如何在您的湖屋中创建快捷方式

-   如何使用视觉对象查询功能转换数据

# ADLS Gen2 的快捷方式

### 任务 1：创建快捷方式

快捷方式用于创建指向目标位置的链接。快捷方式提供对数据的访问权限，而无需将数据实际移动到湖屋中。这就像在
Windows 桌面中创建快捷方式一样。

1.  让我们导航回您在实验室 2 任务 8 中创建的 **Fabric 工作区** **(1)**。

2.  如果您在上一个实验室之后尚未导航离开，您将位于湖屋屏幕中。如果您已导航离开，没有关系。选择
    **lh_FAIAD** (**2)** 以导航到湖屋。

3.  在**资源管理器**面板中，选择**Tables**旁边的**省略号 (3)**。

4.  选择**新建快捷方式 (4)**。

![](images3/media/image6.png){width="6.270833333333333in"
height="6.494391951006124in"}

5.  **新建快捷方式**对话框随即打开。在**外部源**下，选择 **Azure Data
    Lake Storage Gen2**。

![](images3/media/image7.png){width="6.0075765529308836in"
height="3.3830905511811022in"}

6.  选择**新建连接 (1)**。

7.  针对 **URL**
    属性输入以下链接：<https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales>
    **(2)：**

8.  从"身份验证种类"下拉列表中选择**共享访问签名(SAS) (3)**。

9.  复制 SAS 令牌并将其粘贴到 SAS 令牌 (4) 字段中。

-   **SAS 令牌：**

10. 选择屏幕右下角的**下一步 (6)**。

![](images3/media/image8.png){width="6.418722659667542in"
height="3.6118055555555557in"}

11. 您将连接到 ADLS Gen2，目录结构显示在左侧面板中。展开
    **Delta-Parquet-Format-FY25 (1)**。

12. **选择**以下目录 **(2)**，然后单击**下一步 (3)**：

    a.  Application.Cities

    b.  Application.Countries

    c.  Application.StateProvinces

    d.  DateDim

    e.  Sales.BuyingGroups

    f.  Sales.Customers

    g.  Sales.InvoiceLines

    h.  Sales.Invoices

    i.  Warehouse.StockGroups

    j.  Warehouse.StockItemStockGroups

    k.  Warehouse.StockItems

**注意：**Sales.Invoices_May 是唯一**未**选择的目录。

![](images3/media/image9.png){width="6.352689195100613in"
height="3.6006944444444446in"}

13. 系统会将您导航到下一个对话框，我们可以在其中编辑名称。针对
    **Application.Cities**，在"操作"下选择**编辑图标 (1)**。

14. 将 **Application.Cities 重命名为 Cities (2)**。

15. 选中名称旁边的复选标记以保存更改 **(3)**。

![](images3/media/image10.png){width="6.0289873140857395in"
height="2.1527777777777777in"}

16. 同样，按如下所示重命名快捷方式名称：

    a.  将 Application.Countries 重命名为 **Countries**

    b.  将 Application.StateProvinces 重命名为 **States**

    c.  将 DateDim 重命名为 **Date**

    d.  将 Sales.BuyingGroups 重命名为 **BuyingGroups**

    e.  将 Sales.Customers 重命名为 **Customers**

    f.  将 Sales.InvoiceLines 重命名为 **InvoiceLineItems**

    g.  将 Sales.Invoices 重命名为 **Invoices**

    h.  将 Warehouse.StockGroups 重命名为 **ProductGroups**

    i.  将 Warehouse.StockItemStockGroups 重命名为 **ProductItemGroup**

    j.  将 Warehouse.StockItems 重命名为 **ProductItem**

> **注意**：仔细检查名称。拼写错误可能会导致实验室期间出现错误。

17. 选择**创建**以创建快捷方式。

![](images3/media/image11.png){width="6.052400481189851in"
height="3.398838582677165in"}

18. 请注意，所有快捷方式均以表的形式创建。选择 **BuyingGroups**
    表，请注意，我们可以看到数据面板中的数据预览。

![](images3/media/image12.png){width="6.25107283464567in"
height="3.2077077865266843in"}

下一步是转换数据，我们可以创建语义模型。我们将创建视图以转换数据。

# 使用视觉对象查询转换数据

### 任务 2：使用视觉对象查询创建 Geo 视图

1.  我们可以使用 SQL
    终结点访问湖屋。这提供查询数据和创建视图的功能。在屏幕的**右上角**，选择**Lakehouse (1)
    -\> SQL 分析终结点 (2)**。

![](images3/media/image13.png){width="6.5in"
height="1.3070647419072616in"}

系统会将您导航到 SQL
分析终结点。请注意，"资源管理器"面板已更改。现在，您可以创建视图、存储过程、查询等。我们将创建一个可提供低代码界面的视觉对象查询，例如
Power Query。我们将结果另存为视图。

我们将首先创建 Geo 视图。我们需要合并 Cities、States 和 Countries
表的数据来创建 Geo 视图。

2.  从顶部菜单中，单击**新建 SQL 查询 (1)**
    旁边的下拉列表，然后选择**新建视觉对象查询 (2)**。

![](images3/media/image14.png){width="6.447798556430446in"
height="3.797222222222222in"}

3.  若要生成查询，我们需要将表添加到"视觉对象查询"面板。单击 **Cities
    (1)** 表旁边的省略号，然后选择**插入画布 (2)**。

![](images3/media/image15.png){width="6.5in"
height="7.61082895888014in"}

4.  针对 **States** 和 **Countries** 表重复相同步骤。

接下来，我们需要合并这些查询。视觉对象查询编辑器附带使用 Power Query
编辑器的选项。让我们来使用此选项，因为我们对此很熟悉。

5.  从视觉对象查询编辑器的菜单中，选择**在弹出窗口中打开**图标（位于右侧）。系统会将您导航到
    Power Query 编辑器。

![](images3/media/image16.png){width="5.319291338582677in"
height="2.54959208223972in"}

6.  选择 Cities (1) 查询后，从 Power Query
    编辑器功能区中，选择**主页 (2) -\> 合并 (3) -\> 合并查询下拉列表 (4)
    -\> 将查询合并为新查询 (5)**。"合并查询"对话框随即打开。

![](images3/media/image17.png){width="6.5in"
height="1.9226082677165355in"}

7.  在**用于合并的左表**中，选择 **Cities**。

8.  在**用于合并的右表**中，选择 **States**。

9.  从两个表中选择 **StateProvinceID** 列。我们将使用此列进行联接。

10. 选择**内部**作为**联接种类**。

11. 选择**确定**。

![](images3/media/image18.png){width="4.191724628171478in"
height="4.814132764654418in"}

请注意，已创建名为"Merge"的新查询。我们需要"States"中的几列。

12. 在**数据视图**（底部面板）中，单击 **States**
    列（右侧最后一列）旁边的**双箭头**。

13. 面板随即打开。**选择**以下列：

    a.  StateProvinceCode

    b.  StateProvinceName

    c.  CountryID

    d.  SalesTerritory

14. 选择**确定**。

![](images3/media/image19.png){width="6.390979877515311in"
height="2.834819553805774in"}

现在，我们需要合并 Countries 查询。

15. 选择合并 (1) 查询后，选择**主页 (2) -\> 合并 (3) -\>
    合并查询下拉列表 (4) -\> 合并查询 (5)**。

![](images3/media/image20.png){width="6.5in"
height="1.876502624671916in"}

16. "合并 查询"对话框随即打开。在**用于合并的右表**中，选择
    **Countries**。

17. 从两个表中选择 **CountryID** 列。我们将使用此列进行联接。

18. 选择**内部**作为**联接种类**。

19. 选择**确定**。

![A screenshot of a computer Description automatically
generated](images3/media/image21.png){width="3.651943350831146in"
height="4.067567804024497in"}

我们需要"Countries"中的几列。

20. 在**数据视图**（底部面板）中，单击 **Countries**
    列旁边的**双箭头**。

21. 面板随即打开。**选择**以下列：

    a.  CountryName

    b.  FormalName

    c.  IsoAlpha3Code

    d.  IsoNumericCode

    e.  CountryType

    f.  Continent

    g.  Region

    h.  Subregion

22. 选择**确定**。

![A screenshot of a computer Description automatically
generated](images3/media/image22.png){width="6.398951224846894in"
height="1.7161417322834647in"}

我们不需要所有列。确保仅选择所需的列。

23. 选择合并查询后，从功能区中选择**主页 -\> 选择列 -\> 选择列**。

**注意：**如果"选择列"选项不可见，您可以在"管理列"下找到它。

![A screenshot of a computer Description automatically
generated](images3/media/image23.png){width="6.096911636045494in"
height="2.6311078302712163in"}

24. "选择列"对话框随即打开。**取消选中**以下列。

    a.  StateProvinceID

    b.  Location

    c.  LastEditedBy

    d.  ValidFrom

    e.  ValidTo

    f.  CountryID

25. 选择**确定**。

![](images3/media/image24.png){width="2.241547462817148in"
height="3.455450568678915in"}

请注意，该流程与 Power Query
类似，我们将所有步骤记录在右侧"已应用步骤"面板中和视觉对象视图中。让我们重命名
Merge 查询并选择"启用加载"，以便从此查询中加载数据。

26. **右键单击**查询（左侧）面板中的 **Merge**
    查询。选择**重命名**并将查询重命名为 **Geo**。

27. **右键单击**查询（左侧）面板**中**的 **Geo**
    查询。选择**启用加载**以启用此查询。

28. 确保 Cities、States 和 Countries 查询**已禁用**。

29. 选择位于 Power Query 编辑器右下角的**保存**。

![A screenshot of a computer Description automatically
generated](images3/media/image25.png){width="6.5in"
height="2.3989752843394574in"}

系统会将我们导航到视觉对象查询编辑器。现在，让我们将此查询另存为视图。

**注意**：我们使用 Power Query
编辑器执行的所有步骤也可以使用视觉对象查询编辑器执行。

30. 从"视觉对象查询编辑器"菜单中，选择**另存为视图**。

![A screenshot of a computer Description automatically
generated](images3/media/image26.png){width="5.3618777340332455in"
height="2.336246719160105in"}

"另存为视图"对话框随即打开。请注意，SQL 查询可用。如果您想要查看
SQL，可以进行查看。

31. 输入 **Geo** 作为**视图名称**。

32. 选择**确定**以保存视图。

![A screenshot of a computer Description automatically
generated](images3/media/image27.png){width="3.141111111111111in"
height="3.4642268153980753in"}

保存视图后，您将收到警报。

33. 在资源管理器（左侧）面板中，展开**Views**。我们有新创建的 Geo 视图。

![A screenshot of a computer Description automatically
generated](images3/media/image28.png){width="3.6146030183727036in"
height="3.8940824584426945in"}

### 任务 3：使用视觉对象查询创建 Reseller 视图

让我们创建 Reseller
视图，该视图可通过合并"Customers"表与"BuyingGroups"表来创建。这次我们将使用视觉对象查询创建视图。

1.  从顶部菜单中，单击**新建 SQL 查询 (1)**
    旁边的下拉列表，然后选择**新建视觉对象查询 (2)**。

2.  若要生成查询，我们需要将表添加到"视觉对象查询"面板。单击
    **BuyingGroups (1)** 表旁边的省略号，然后选择**插入画布 (2)**。

![A screenshot of a computer Description automatically
generated](images3/media/image29.png){width="6.020833333333333in"
height="4.611875546806649in"}

3.  针对 **Customers** 表重复相同步骤。

4.  选择 **Customers**
    查询。选择后，"Customers"将有一个蓝色边框，**"Table"**后面有一个
    **+**
    符号（这指示我们要在**"Table"**后面添加一个步骤。如果您在**"Table"**后没有看到
    **+** 符号，则可能选择了其他步骤。选择**"Table"**即可开始）。

<!-- -->

5.  从"视觉对象查询"菜单中，选择**组合 -\> 合并查询**。

![A screenshot of a computer Description automatically
generated](images3/media/image30.png){width="4.350240594925634in"
height="1.5810640857392826in"}

"合并"对话框随即打开，其中已选择"Customers"作为顶部表。

6.  在**用于合并的右表**中，选择 **BuyingGroups**。

7.  从两个表中选择 **BuyingGroupID** 列。我们将使用此列进行联接。

8.  选择**内部**作为**联接种类**。

9.  选择**确定**。

![A screenshot of a computer Description automatically
generated](images3/media/image31.png){width="3.5722867454068243in"
height="3.539712379702537in"}

10. 在**数据视图**（底部面板）中，单击 **BuyingGroups**
    列旁边的**双箭头**（右侧最后一列）以从 BuyingGroups 中选择所需的列。

11. 面板随即打开。**选择** **BuyingGroupName** 列。

12. 选择**确定**。

![A screenshot of a computer Description automatically
generated](images3/media/image32.png){width="6.440259186351706in"
height="2.7738156167979002in"}

我们不需要所有列。让我们仅选择所需列。

13. 从"视觉对象查询"菜单中，选择**管理列 -\> 选择列**。

![](images3/media/image33.png){width="5.677199256342957in"
height="1.2526399825021872in"}

14. "选择列"对话框随即打开。**选择**以下列。

    a.  ResellerID

    b.  ResellerName

    c.  PostalCityID

    d.  PhoneNumber

    e.  FaxNumber

    f.  WebsiteURL

    g.  DeliveryAddressLine1

    h.  DeliveryAddressLine2

    i.  DeliveryPostalCode

    j.  PostalAddressLine1

    k.  PostalAddressLine2

    l.  PostalPostalCode

    m.  BuyingGroupName

15. 选择**确定**。

![A screenshot of a computer Description automatically
generated](images3/media/image34.png){width="2.314682852143482in"
height="3.1967825896762903in"}

16. 让我们重命名"BuyingGroupName"列。在 **Data**
    视图中，双击"BuyingGroupName"列标头以使其可编辑。

17. 将此列**重命名**为 **ResellerCompany**。

![A screenshot of a computer Description automatically
generated](images3/media/image35.png){width="6.366902887139108in"
height="1.910071084864392in"}

请注意，"Customer"表已记录所有步骤。现在，让我们保存此视图。

18. 我们需要保存 Customer 查询，因为它包含所有步骤。我们需要启用加载。在
    **Customer** 查询框中选择**省略号**。

19. 确保选中**启用加载**。

![A screenshot of a computer Description automatically
generated](images3/media/image36.png){width="6.300122484689414in"
height="2.0699890638670166in"}

**注意**：如果选中"启用加载"，则 **Customer** 框应具有蓝色边框。

20. 从"视觉对象查询"菜单中，选择**另存为视图**。

![A screenshot of a computer Description automatically
generated](images3/media/image37.png){width="5.816025809273841in"
height="1.2299617235345581in"}

"另存为视图"对话框随即打开。请注意，SQL
查询可用。您可以通过选择它来进行查看。

21. 输入 **Reseller** 作为**视图名称**。

22. 选择**确定**以保存视图。

![A screenshot of a computer Description automatically
generated](images3/media/image38.png){width="3.092136920384952in"
height="3.40712489063867in"}

保存视图后，您将收到警报。

23. 在资源管理器（左侧）面板中，展开**Views**。我们有新创建的 Reseller
    视图。

![](images3/media/image39.png){width="3.15371062992126in"
height="3.4437062554680664in"}

### 任务 4：使用视觉对象查询创建 Sales 视图

让我们创建 Sales
视图，该视图可通过合并"InvoiceLineItems"和"Invoices"表与"Reseller"视图来创建。我们在
Power BI Desktop
中有此查询。我们将从"高级编辑器"复制代码。但在复制代码之前，我们需要使用视觉对象查询创建一个合并表，因为无法在视觉对象查询中创建空白查询。让我们试一下此方法。

1.  从顶部菜单中，单击**新建 SQL
    查询**旁边的下拉列表，然后选择**新建视觉对象查询**。

![A screenshot of a computer Description automatically
generated](images3/media/image14.png){width="6.447798556430446in"
height="3.797222222222222in"}

2.  从**资源管理器 -\>
    表**部分中，我们需要将表添加到"视觉对象查询"面板。单击
    **InvoiceLineItems** 表旁边的省略号，然后选择**插入画布**。

3.  针对 **Invoices** 重复相同步骤。

4.  从**资源管理器 -\>
    视图**部分中，我们需要将表添加到"视觉对象查询"面板。单击
    **Reseller** 表旁边的省略号，然后选择**插入画布**。

5.  从视觉对象查询编辑器中，选择**在弹出窗口中打开**以打开 Power Query
    编辑器。

![A screenshot of a computer Description automatically
generated](images3/media/image40.png){width="6.1538331146106735in"
height="2.5625in"}

6.  选择 **InvoiceLineItems** 查询后，从功能区中选择**主页 (2) -\>
    合并 (3) -\> 合并查询下拉列表 (4) -\> 将查询合并为新查询
    (5)。**"合并查询"对话框随即打开。

![A screenshot of a computer Description automatically
generated](images3/media/image41.png){width="6.197941819772528in"
height="2.076388888888889in"}

7.  在**用于合并的左表**中，选择 **InvoiceLineItems**。

8.  在**用于合并的右表**中，选择 **Invoices**。

9.  从两个表中选择 **InvoiceID** 列。我们将使用此列进行联接。

10. 选择**内部**作为**联接种类**。

11. 选择**确定**。

![](images3/media/image42.png){width="3.134802055993001in"
height="3.6016863517060367in"}

我们将从 Power BI Desktop 中复制代码并使用"高级编辑器"粘贴它。

12. 如果您尚未打开
    **FAIAD.pbix**，请打开它。它位于您的实验室环境的桌面的 **Reports**
    文件夹中。

13. 从功能区中选择**主页 -\> 转换数据**。Power Query
    窗口随即打开。您在之前的实验室中注意到，左侧面板中的查询是按数据源组织的。

![A screenshot of a computer Description automatically
generated](images3/media/image43.png){width="5.966029090113736in"
height="3.5388899825021873in"}

14. 从左侧**查询**面板的 **ADLSData** **(1)** 文件夹下，选择 **Sales
    (2)** 查询**。**

15. 从功能区中选择**主页 -\> 高级编辑器
    (3)**。"高级编辑器"对话框随即打开。

![](images3/media/image44.png){width="3.8086154855643044in"
height="3.7849595363079613in"}

**注意：**如果找不到高级编辑器，可以在**主页 -\> 查询 -\>
高级编辑器**下访问它。

16. **选择行 3 中的代码** (#\"Expanded Invoice\" ...)
    一直到最后一行代码。

17. **右键单击**并选择**复制**。

18. 选择**取消**以关闭"高级编辑器"。

![A screenshot of a computer Description automatically
generated](images3/media/image45.png){width="6.302386264216973in"
height="3.8430719597550307in"}

19. **导航回已打开 Power Query 编辑器的浏览器**。

20. 确保您已选择 **合并** 查询。

21. 从功能区中选择**主页 -\> 高级编辑器**。"高级编辑器"对话框随即打开。

![A screenshot of a computer Description automatically
generated](images3/media/image46.png){width="6.5in"
height="2.074142607174103in"}

22. 在**第 2 行的末尾添加逗号** (Source =
    Table.NestedJoin(InvoiceLineItems, {\"InvoiceID\"}, Invoices,
    {\"InvoiceID\"}, \"Invoices\", JoinKind.Inner)

23. 单击 **Enter** 以开始一个新行。

24. 在键盘上按 **Ctrl+V** 以粘贴从 Power BI Desktop 复制的代码。

> **注意**：如果您在实验室环境中工作，请选择屏幕右上角的**省略号
> (...)**。使用滑块**启用** **VM
> 本机剪贴板**。在对话框中选择"确定"。粘贴查询后，您可以禁用此选项。

![A screenshot of a computer Description automatically
generated](images3/media/image47.png){width="6.5in"
height="0.9585247156605424in"}

![A close up of a text Description automatically
generated](images3/media/image48.png){width="4.317435476815398in"
height="2.4421850393700786in"}

25. 突出显示最后两行代码（在源中），然后将其**删除**。

26. 选择**确定**以保存更改。

![A screen shot of a computer Description automatically
generated](images3/media/image49.png){width="6.5in"
height="2.988280839895013in"}

为了更方便起见，请删除"高级编辑器"中的所有代码，并将以下代码粘贴到"高级编辑器"中。

[let]{.mark}

[  Source = Table.NestedJoin(InvoiceLineItems, {\"InvoiceID\"},
Invoices, {\"InvoiceID\"}, \"Invoices\", JoinKind.Inner),]{.mark}

[    #\"Expanded Invoice\" = Table.ExpandTableColumn(Source,
\"Invoices\", {\"CustomerID\", \"BillToCustomerID\",
\"SalespersonPersonID\", \"InvoiceDate\"}, {\"CustomerID\",
\"BillToCustomerID\", \"SalespersonPersonID\",
\"InvoiceDate\"}),]{.mark}

[    #\"Removed Other Columns\" = Table.SelectColumns(#\"Expanded
Invoice\",{\"InvoiceLineID\", \"InvoiceID\", \"StockItemID\",
\"Quantity\", \"UnitPrice\", \"TaxRate\", \"TaxAmount\", \"LineProfit\",
\"ExtendedPrice\", \"CustomerID\", \"SalespersonPersonID\",
\"InvoiceDate\"}),]{.mark}

[    #\"Renamed Columns\" = Table.RenameColumns(#\"Removed Other
Columns\",{{\"CustomerID\", \"ResellerID\"}}),]{.mark}

[    #\"Merged Queries\" = Table.NestedJoin(#\"Renamed Columns\",
{\"ResellerID\"}, Reseller, {\"ResellerID\"}, \"Customer\",
JoinKind.Inner),]{.mark}

[    #\"Added Custom\" = Table.AddColumn(#\"Merged Queries\", \"Sales
Amount\", each \[ExtendedPrice\] - \[TaxAmount\]),]{.mark}

[    #\"Changed Type\" = Table.TransformColumnTypes(#\"Added
Custom\",{{\"Sales Amount\", type number}}),]{.mark}

[    #\"Removed Columns\" = Table.RemoveColumns(#\"Changed
Type\",{\"Customer\"})]{.mark}

[in]{.mark}

[    #\"Removed Columns\"]{.mark}

27. 系统会将您导航回 Power Query 编辑器。在左侧的"查询"面板中，双击
    **Merge** 查询以对其重命名。

28. **将** Merge 查询重命名为 **Sales**。

29. 右键单击"Sales"查询，然后选择**启用加载**以启用要加载的查询。

![](images3/media/image50.png){width="3.164420384951881in"
height="3.0972222222222223in"}

30. 选择**保存**以保存并关闭 Power Query
    对话框。系统会将您导航到视觉对象查询编辑器。

31. 从"视觉对象查询"菜单中，选择**另存为视图**。"另存为视图"对话框随即打开。请注意，SQL
    查询可用。您可以通过选择它来进行查看。

32. 输入 **Sales** 作为**视图名称 (1)**。

33. 选择**确定 (2)** 以保存视图。

![A screenshot of a computer Description automatically
generated](images3/media/image51.png){width="6.291666666666667in"
height="6.787821522309711in"}

保存视图后，您将收到警报。

34. 在资源管理器（左侧）面板中，展开**Views**。我们有新创建的 Sales
    视图。

![](images3/media/image52.png){width="4.258929352580927in"
height="3.3469160104986875in"}

### 任务 5：使用视觉对象查询创建 Product 视图

让我们创建 Product 视图，该视图可通过合并
**ProductItem**、**ProductItemGroup** 和 **ProductGroups**
表来创建。若要继续，我们需要将代码复制到"高级编辑器"中。

1.  从顶部菜单中，单击**新建 SQL 查询 (1)**
    旁边的下拉列表，然后选择**新建视觉对象查询 (2)**。

![](images3/media/image53.jpeg){width="5.53791447944007in"
height="3.8in"}

2.  从"资源管理器"部分中，我们需要将表添加到"视觉对象查询"面板。单击
    **ProductItem (1)** 表旁边的省略号，然后选**插入画布 (2)**。

![](images3/media/image54.png){width="5.791666666666667in"
height="7.928397856517935in"}

3.  针对 **ProductItemGroup** 和 **ProductGroups** 表重复相同步骤。

4.  在视觉对象查询编辑器中，选择**焦点模式图标**以打开 Power Query
    编辑器。

![](images3/media/image55.png){width="5.779069335083115in"
height="2.7179002624671917in"}

5.  选择 **ProductItem** 查询后，从功能区中，选择**主页 (1) -\> 组合 (2)
    -\> 合并查询下拉列表 (3) -\> 将查询合并为新查询
    (4)**。"合并"对话框随即打开。

![](images3/media/image56.png){width="6.122402668416448in"
height="4.563888888888889in"}

6.  在**用于合并的左表**中，选择 **ProductItem**。

7.  在**用于合并的右表**中，选择 **ProductItemGroup**。

8.  从两个表中选择 **StockItemID** 列。我们将使用此列进行联接。

9.  选择**左外**作为**联接种类**。

10. 选择**确定。**已创建新的"Merge"查询。

![](images3/media/image57.png){width="3.016639326334208in"
height="3.457425634295713in"}

11. 选择 Merge 查询后，从功能区中，选择**主页 -\>
    高级编辑器**。"高级编辑器"对话框随即打开。

![A screenshot of a computer Description automatically
generated](images3/media/image58.png){width="4.906741032370953in"
height="1.7559656605424323in"}

**注意：**如果找不到高级编辑器，可以在**主页 -\> 查询 -\>
高级编辑器**下访问它。

12. 在"高级编辑器"中**选择全部代码**，然后将其**删除**。

13. 将以下代码**粘贴**到"高级编辑器"中。

[let]{.mark}

[Source = Table.NestedJoin(ProductItem, {\"StockItemID\"},
ProductItemGroup, {\"StockItemID\"}, \"ProductItemGroup\",
JoinKind.LeftOuter),]{.mark}

[#\"Expanded ProductItemGroup\" = Table.ExpandTableColumn(Source,
\"ProductItemGroup\", {\"StockGroupID\"}, {\"StockGroupID\"}),]{.mark}

[#\"Merged queries\" = Table.NestedJoin(#\"Expanded ProductItemGroup\",
{\"StockGroupID\"}, ProductGroups, {\"StockGroupID\"},
\"ProductGroups\", JoinKind.LeftOuter),]{.mark}

[#\"Expanded ProductGroups\" = Table.ExpandTableColumn(#\"Merged
queries\", \"ProductGroups\", {\"StockGroupName\"},
{\"StockGroupName\"}),]{.mark}

[#\"Choose columns\" = Table.SelectColumns(#\"Expanded ProductGroups\",
{\"StockItemID\", \"StockItemName\", \"SupplierID\", \"Size\",
\"IsChillerStock\", \"TaxRate\", \"UnitPrice\",
\"RecommendedRetailPrice\", \"TypicalWeightPerUnit\",
\"StockGroupName\"})]{.mark}

[in]{.mark}

[#\"Choose columns\"]{.mark}

14. 选择**确定**以关闭"高级编辑器"。系统会将您导航回 Power Query
    编辑器。

![A computer screen shot Description automatically
generated](images3/media/image59.png){width="6.5in"
height="2.995820209973753in"}

15. 在左侧的"查询"面板中，双击 **Merge** 查询以对其重命名。

16. **将 Merge 查询的名称**更改为 **Product**。

17. 右键单击 Product 查询，然后选择**启用加载**以启用要加载的查询。

18. 选择**保存**以保存并关闭 Power Query
    对话框。系统会将您导航到视觉对象查询。

![A screenshot of a computer Description automatically
generated](images3/media/image60.png){width="6.5in"
height="2.4046839457567803in"}

19. 从"视觉对象查询"菜单中，选择**另存为视图**。"另存为视图"对话框随即打开。请注意，SQL
    查询可用。您可以通过选择它来进行查看。

20. 输入 **Product** 作为**视图名称**。

21. 选择**确定**以保存视图。

![A screenshot of a computer Description automatically
generated](images3/media/image61.png){width="3.009562554680665in"
height="3.337133639545057in"}

保存视图后，您将收到警报。

22. 在资源管理器（左侧）面板中，展开**视图**。我们有新创建的 Product
    视图。

![A screenshot of a computer Description automatically
generated](images3/media/image62.png){width="3.9036253280839897in"
height="3.0836001749781277in"}

我们已转换来自 ADLS Gen2
数据源的数据。在本实验室中，我们了解了如何创建快捷方式，并探索了使用视觉对象查询视图转换数据的各种选项。

在下一个实验室中，我们将了解如何使用数据流 Gen2
以及如何创建另一个湖屋的快捷方式。

# 参考

Fabric Analyst in a Day (FAIAD) 向您介绍了 Microsoft Fabric
中提供的一些主要功能。在服务菜单中，"帮助
(?)"部分包含指向一些优质资源的链接。

![A screenshot of a phone Description automatically
generated](images3/media/image63.png){width="1.9321412948381453in"
height="4.302384076990376in"}

以下更多参考资源可帮助您进行与 Microsoft Fabric 相关的后续步骤。

-   请参阅博客文章以阅读完整的 [Microsoft Fabric GA
    公告](https://aka.ms/Fabric-Hero-Blog-Ignite23)

-   通过[引导式教程](https://aka.ms/Fabric-GuidedTour)探索 Fabric

-   注册 [Microsoft Fabric 免费试用版](https://aka.ms/try-fabric)

-   访问 [Microsoft Fabric 网站](https://aka.ms/microsoft-fabric)

-   通过探索 [Fabric 学习模块](https://aka.ms/learn-fabric)学习新技能

-   探索 [Fabric 技术文档](https://aka.ms/fabric-docs)

-   阅读[有关 Fabric
    入门指南的免费电子书](https://aka.ms/fabric-get-started-ebook)

-   加入 [Fabric
    社区](https://aka.ms/fabric-community)发布问题、分享反馈并向他人学习

阅读更多深度 Fabric 体验公告博客：

-   [Fabric 中的 Data Factory
    体验博客](https://aka.ms/Fabric-Data-Factory-Blog) 

-   [Fabric 中的 Synapse Data Engineering
    体验博客](https://aka.ms/Fabric-DE-Blog) 

-   [Fabric 中的 Synapse Data Science
    体验博客](https://aka.ms/Fabric-DS-Blog) 

-   [Fabric 中的 Synapse Data Warehousing
    体验博客](https://aka.ms/Fabric-DW-Blog) 

-   [Fabric 中的 Synapse Real-Time Analytics
    体验博客](https://aka.ms/Fabric-RTA-Blog)

-   [Power BI 公告博客](https://aka.ms/Fabric-PBI-Blog)

-   [Fabric 中的 Data Activator 博客](https://aka.ms/Fabric-DA-Blog) 

-   [Fabric 中的管理和治理博客](https://aka.ms/Fabric-Admin-Gov-Blog)

-   [Fabric 中的 OneLake 博客](https://aka.ms/Fabric-OneLake-Blog)

-   [Dataverse 和 Microsoft Fabric
    集成博客](https://aka.ms/Dataverse-Fabric-Blog)

> © 2023 Microsoft Corporation.保留所有权利。
>
> 使用此演示/实验即表示您已同意以下条款：
>
> 本演示/实验中的技术/功能由 Microsoft Corporation
> 出于获取反馈和提供学习体验的目的提供。只能将本演示/实验用于评估这些技术特性和功能以及向
> Microsoft
> 提供反馈。不得用于任何其他用途。不得对此演示/实验或其任何部分进行修改、复制、分发、传送、显示、执行、复制、公布、许可、转让、销售或基于以上内容创建衍生作品。
>
> 严禁将本演示/实验（或其任何部分）复制到任何其他服务器或位置以便进一步复制或再分发。
>
> 本演示/实验出于上述目的，在不涉及复杂设置或安装操作的模拟环境中提供特定软件技术/产品特性和功能，包括潜在的新功能和概念。本演示/实验中展示的技术/概念可能不是完整的功能，可能会以不同于最终版本的工作方式工作。我们也可能不会发布此类功能或概念的最终版本。在物理环境中使用此类特性和功能的体验可能也有所不同。
>
> **反馈**。如您针对本演示/实验中所述的技术特性、功能和/或概念向
> Microsoft 提供反馈，则意味着您向 Microsoft
> 无偿提供以任何方式、出于任何目的使用和分享您的反馈并将其商业化的权利。您同样无偿为第三方提供其产品、技术和服务使用或配合使用包含此反馈的
> Microsoft
> 软件或服务的任何特定部分所需的任何专利权。如果根据某项许可的规定，Microsoft
> 由于在其软件或文档中包含了您的反馈需要向第三方授予该软件或文档的许可，请不要提供这样的反馈。这些权利在本协议终止后继续有效。
>
> 对于本演示/实验，Microsoft Corporation
> 不提供任何明示、暗示或法定的保证和条件，包括有关适销性、针对特定目的的适用性、所有权和不侵权的所有保证和条件。对于使用本演示/实验产生的结果或输出内容的准确性，或者出于任何目的包含本演示/实验中的信息的适用性，Microsoft
> 不做任何保证或陈述。
>
> **免责声明**
>
> 本演示/实验仅包含 Microsoft Power BI
> 的部分新功能和增强功能。在产品的后续版本中，部分功能可能有所更改。在本演示/实验中，可了解部分新功能，但并非全部新功能。

