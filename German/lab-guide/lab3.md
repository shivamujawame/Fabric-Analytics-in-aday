#  {#section .TOC-Heading}

> Microsoft Fabric
>
> Fabric Analyst in a Day
>
> Übung 0

Microsoft Fabric Fabric Analyst in a Day

Übung 3

Version: Februar 2025

> Übung 0

# Inhalt  {#inhalt .TOC-Heading}

[Einführung [3](#einführung)](#einführung)

[Verknüpfung zu ADLS Gen2
[3](#verknüpfung-zu-adls-gen2)](#verknüpfung-zu-adls-gen2)

[Aufgabe1: Verknüpfung erstellen
[3](#aufgabe1-verknüpfung-erstellen)](#aufgabe1-verknüpfung-erstellen)

[Daten mithilfe einer Visual-Abfrage transformieren
[8](#daten-mithilfe-einer-visual-abfrage-transformieren)](#daten-mithilfe-einer-visual-abfrage-transformieren)

[Aufgabe 2: Ansicht „Geo" mithilfe einer Visual-Abfrage erstellen
[8](#aufgabe-2-ansicht-geo-mithilfe-einer-visual-abfrage-erstellen)](#aufgabe-2-ansicht-geo-mithilfe-einer-visual-abfrage-erstellen)

[Aufgabe 3: Ansicht „Reseller" mithilfe einer Visual-Abfrage erstellen
[18](#aufgabe-3-ansicht-reseller-mithilfe-einer-visual-abfrage-erstellen)](#aufgabe-3-ansicht-reseller-mithilfe-einer-visual-abfrage-erstellen)

[Aufgabe 4: Ansicht „Sales" mithilfe einer Visual-Abfrage erstellen
[25](#aufgabe-4-ansicht-sales-mithilfe-einer-visual-abfrage-erstellen)](#aufgabe-4-ansicht-sales-mithilfe-einer-visual-abfrage-erstellen)

[Aufgabe 5: Ansicht „Product" mithilfe einer Visual-Abfrage erstellen
[33](#aufgabe-5-ansicht-product-mithilfe-einer-visual-abfrage-erstellen)](#aufgabe-5-ansicht-product-mithilfe-einer-visual-abfrage-erstellen)

[Referenzen [39](#referenzen)](#referenzen)

# 

# 

# 

# 

# 

# 

# 

# 

# 

# 

# Einführung 

In unserem Szenario stammen die Verkaufsdaten aus dem ERP-System und
werden in einer ADLS Gen2 gespeichert. Jeden Tag um 12 Uhr mittags
werden die Daten aktualisiert. Wir müssen diese Daten transformieren, in
Lakehouse erfassen und in unserem Modell verwenden.

Es gibt mehrere Möglichkeiten, diese Daten zu erfassen.

-   **Verknüpfungen:** Hiermit wird eine Verknüpfung zu den Daten
    erstellt, und wir können sie anhand von Ansichten für visuelle
    Abfragen transformieren. Wir werden Verknüpfungen in dieser Übung
    verwenden.

-   **Notebooks:** Dafür müssen wir Code schreiben. Es handelt sich um
    einen entwicklerfreundlichen Ansatz.

-   **Dataflow Gen2:** Sie sind wahrscheinlich mit Power Query oder
    Dataflow Gen1 vertraut. Dataflow Gen2 ist, wie der Name schon sagt,
    die neuere Version von Dataflow. Es bietet alle Funktionen von Power
    Query/Dataflow Gen1 und ermöglicht zusätzlich die Transformation und
    Erfassung von Daten in mehreren Datenquellen. Wir werden dies in den
    nächsten Übungen vorstellen.

-   **Datenpipeline:** Dies ist ein Orchestrierungstool. Aktivitäten
    können orchestriert werden, um Daten zu extrahieren, zu
    transformieren und zu erfassen. Wir werden Data Pipeline verwenden,
    um Dataflow Gen2-Aktivitäten auszuführen, die wiederum Extraktion,
    Transformation und Aufnahme durchführen.

Wir beginnen mit der Erstellung einer Verknüpfung, um Daten aus der ADLS
Gen2-Datenquelle in ein Lakehouse zu erfassen. Nach der Erfassung
transformieren wir sie mit Ansichten für Visual-Abfragen.

Am Ende dieser Übung haben Sie Folgendes gelernt:

-   Wie Sie Verknüpfungen in Ihrem Lakehouse erstellen

-   Wie Sie Daten mithilfe der Visual-Abfrage transformieren

# Verknüpfung zu ADLS Gen2

### Aufgabe1: Verknüpfung erstellen

Verknüpfungen werden verwendet, um eine Verknüpfung zum Zielort zu
erstellen. Mit Verknüpfungen kann auf die Daten zugegriffen werden, ohne
dass die Daten physisch in das Lakehouse gebracht werden müssen. Dies
ist vergleichbar mit der Erstellung von Verknüpfungen auf dem Windows
Desktop.

1.  Navigieren wir zurück zum **Fabric-Arbeitsbereich** **(1)**, den Sie
    in Übung 2, Aufgabe 8, erstellt haben.

2.  Wenn Sie nach der vorherigen Übung nicht zu einem anderen Bereich
    navigiert sind, befinden Sie sich im Lakehouse-Bildschirm. Wenn Sie
    zu einem anderen Bereich navigiert sind, ist das in Ordnung. Wählen
    Sie **lh_FAIAD** (**2)** aus, um zum Lakehouse zu navigieren.

3.  Wählen Sie im Bereich **Explorer** die **Auslassungspunkte (3)**
    neben **Tabellen** aus.

4.  Wählen Sie **Neue Verknüpfung (4)** aus.

![](images3/media/image6.png){width="6.270833333333333in"
height="6.379891732283465in"}

5.  Das Dialogfeld **Neue Verknüpfung** wird geöffnet. Wählen Sie unter
    **Externe Quellen** die Option **Azure Data Lake Storage Gen2** aus.

![](images3/media/image7.png){width="6.0292705599300085in"
height="3.3830905511811022in"}

6.  Wählen Sie **+ Neue Verbindung erstellen (1)** aus.

7.  Geben Sie den folgenden Link für die Eigenschaft **URL** ein:
    <https://stvnextblobstorage.dfs.core.windows.net/fabrikam-sales>
    **(2):**

8.  Wählen Sie **Shared Access Signature (SAS) (3)** aus der
    Dropdown-Liste „Authentifizierungsart" aus.

9.  Kopieren Sie das SAS-Token und fügen Sie sie in das
    Feld„SAS-Token" (4) ein.

-   **SAS-Token:**

10. Wählen Sie unten rechts auf dem Bildschirm **Weiter (5)** aus.

![](images3/media/image8.png){width="6.159788932633421in"
height="3.6118055555555557in"}

11. Sie werden mit ADLS Gen2 verbunden und die Verzeichnisstruktur wird
    im linken Bereich angezeigt. Erweitern Sie
    **Delta-Parquet-Format-FY25 (1)**.

12. **Wählen** Sie die folgenden Verzeichnisse **(2)** aus, und klicken
    Sie dann auf **Weiter (3):**

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

**Hinweis:** „Sales.Invoices_May" ist das einzige Verzeichnis, das
**nicht** ausgewählt ist.

![](images3/media/image9.png){width="6.387843394575678in"
height="3.6006944444444446in"}

13. Sie werden zum nächsten Dialogfeld weitergeleitet, in dem Sie die
    Namen bearbeiten können. Wählen Sie das Symbol **Bearbeiten (1)**
    unter Aktionen für **Application.Cities** aus.

14. Benennen Sie **Application.Cities in Cities (2)** um.

15. Aktivieren Sie das Häkchen neben dem Namen, um die Änderung zu
    speichern **(3)**.

![](images3/media/image10.png){width="6.5in"
height="1.8726060804899387in"}

16. Benennen Sie auch die Namen der Verknüpfungen wie folgt um:

    a.  Application.Countries in **Countries**

    b.  Application.StateProvinces in **States**

    c.  DateDim in **Date**

    d.  Sales.BuyingGroups in **BuyingGroups**

    e.  Sales.Customers in **Customers**

    f.  Sales.InvoiceLines in **InvoiceLineItems**

    g.  Sales.Invoices in **Invoices**

    h.  Warehouse.StockGroups in **ProductGroups**

    i.  Warehouse.StockItemStockGroups in **ProductItemGroup**

    j.  Warehouse.StockItems in **ProductItem**

> **Hinweis**: Überprüfen Sie die Namen. Ein Tippfehler kann während der
> Übung zu Fehlern führen.

17. Wählen Sie **Erstellen** aus, um die Verknüpfung zu erstellen.

![](images3/media/image11.png){width="6.0625in"
height="3.382592957130359in"}

18. Beachten Sie, dass alle Verknüpfungen als Tabellen erstellt werden.
    Wählen Sie die Tabelle **BuyingGroups** aus, und beachten Sie, dass
    im Datenbereich eine Vorschau der Daten angezeigt wird.

![](images3/media/image12.png){width="6.18132217847769in"
height="3.2077077865266843in"}

Das nächste Schritt besteht darin, die Daten zu transformieren, damit
wir ein semantisches Modell erstellen können. Wir erstellen Ansichten,
um die Daten zu transformieren.

# Daten mithilfe einer Visual-Abfrage transformieren

### Aufgabe 2: Ansicht „Geo" mithilfe einer Visual-Abfrage erstellen

1.  Wir können Lakehouse über einen SQL-Endpunkt aufrufen. Dies bietet
    die Möglichkeit, die Daten abzufragen und Ansichten zu erstellen.
    Wählen Sie **oben rechts** auf dem Bildschirm **Lakehouse (1) -\>
    SQL-Analyseendpunkt (2)** aus.

![](images3/media/image13.png){width="6.5in"
height="1.9060870516185477in"}

Sie werden zum SQL-Analyseendpunkt weitergeleitet. Beachten Sie, dass
sich das Explorer-Bereich geändert hat. Sie können jetzt Ansichten,
gespeicherte Prozeduren, Abfragen und mehr erstellen. Wir erstellen eine
Visual-Abfrage, da sie eine Low-Code, Power Query-ähnliche Schnittstelle
bietet. Wir speichern das Ergebnis als Ansicht.

Wir beginnen mit der Erstellung einer Ansicht „Geo". Wir müssen Daten
aus den Tabellen „Cities", „States" und „Countries" zusammenführen, um
die Ansicht „Geo" zu erstellen.

2.  Klicken Sie im oberen Menü auf das Dropdownmenü neben **Neue
    SQL-Abfrage (1)**, und wählen Sie dann **Neue visuelle Abfrage (2)**
    aus.![](images3/media/image14.png){width="6.5in"
    height="3.7154418197725283in"}

3.  Um eine Abfrage zu erstellen, müssen wir Tabellen zum visuellen
    Abfragebereich hinzufügen. Klicken Sie auf die Auslassungspunkte
    neben der Tabelle **Cities (1)** und wählen Sie **In Zeichenbereich
    einfügen (2)** aus.

![](images3/media/image15.png){width="6.5in"
height="6.479905949256343in"}

4.  Wiederholen Sie die gleichen Schritte für die Tabellen **States**
    und **Countries**.

Als Nächstes müssen wir diese Abfragen zusammenführen. Der Editor für
Visual-Abfragen wird mit der Option zum Verwenden des Power
Query-Editors bereitgestellt. Lassen Sie uns diese verwenden, da wir
damit vertraut sind.

5.  Klicken Sie im Menü des Editors für Visual-Abfragen auf das Symbol
    **Im Popup-Fenster öffnen** (rechts). Sie werden zum Power
    Query-Editor weitergeleitet.

![](images3/media/image16.png){width="6.390117016622922in"
height="2.217548118985127in"}

6.  Wählen Sie bei ausgewählter Abfrage „Cities" (1) im Menüband des
    Power Query-Editors **Start (2)-\> Kombinieren (3) -\> Abfragen
    zusammenführen (4) -\> Abfragen als neue Abfrage zusammenführen
    (5)**. Das Dialogfeld „Abfragen zusammenführen" wird geöffnet.

![](images3/media/image17.png){width="6.5in"
height="1.9178532370953632in"}

7.  Wählen Sie in der **linken zusammenzuführenden Tabelle** die Option
    **Cities** aus.

8.  Wählen Sie in der **rechten zusammenzuführenden Tabelle** die Option
    **States** aus.

9.  Wählen Sie **StateProvinceID**-Spalten aus beiden Tabellen aus. Wir
    führen eine Verknüpfung über diese Spalte aus.

10. Wählen Sie **Innerhalb** als **Art des Joins** aus.

11. Wählen Sie **OK** aus.

![](images3/media/image18.png){width="4.197916666666667in"
height="4.796698381452319in"}

Beachten Sie, dass eine neue Abfrage mit dem Namen „Merge" erstellt
wurde. Wir benötigen einige Spalten aus „States".

12. Klicken Sie in der **Datenansicht** (unterer Bereich) auf den
    **Doppelpfeil** neben der Spalte **States** (letzte Spalte rechts).

13. Es wird ein Bereich geöffnet. **Wählen** Sie die folgenden Spalten
    aus:

    a.  StateProvinceCode

    b.  StateProvinceName

    c.  CountryID

    d.  SalesTerritory

14. Wählen Sie **OK** aus.

![](images3/media/image19.png){width="6.150601487314086in"
height="2.917422353455818in"}

Wir müssen jetzt die Abfrage „Countries" zusammenführen.

15. Wählen Sie bei ausgewählter Merge-Abfrage (1) **Start (2) -\>
    Kombinieren (3) -\> Abfragen zusammenführen (4) -\> Abfragen
    zusammenführen (5)** aus.

![](images3/media/image20.png){width="6.5in"
height="1.9494608486439196in"}

16. Das Dialogfeld „Abfragen zusammenführen" wird geöffnet. Wählen Sie
    in der **rechten zusammenzuführenden Tabelle** **Countries** aus.

17. Wählen Sie **CountryID**-Spalten aus beiden Tabellen aus. Wir führen
    eine Verknüpfung über diese Spalte aus.

18. Wählen Sie **Innerhalb** als **Art des Joins** aus.

19. Wählen Sie **OK** aus.

![](images3/media/image21.png){width="3.6619706911636047in"
height="3.980880358705162in"}

Wir benötigen einige Spalten aus „Countries".

20. Klicken Sie in der **Datenansicht** (unterer Bereich) auf den
    **Doppelpfeil** neben der Spalte **Countries**.

21. Es wird ein Bereich geöffnet. **Wählen** Sie die folgenden Spalten
    aus:

    a.  CountryName

    b.  FormalName

    c.  IsoAlpha3Code

    d.  IsoNumericCode

    e.  CountryType

    f.  Kontinent

    g.  Region

    h.  Subregion

22. Klicken Sie auf **OK**.

![](images3/media/image22.png){width="6.155631014873141in"
height="1.7413385826771655in"}

Wir benötigen nicht alle Spalten. Stellen Sie sicher, dass Sie nur die
Spalten auswählen, die wir benötigen.

23. Wählen Sie bei Merge-Abfrage im Menüband **Start -\> Spalten
    auswählen-\> Spalten auswählen** aus.

> **Hinweis:** Wenn die Option „Spalten auswählen" nicht angezeigt wird,
> finden Sie sie unter „Spalten verwalten".

![](images3/media/image23.png){width="6.071326552930883in"
height="2.6311078302712163in"}

24. Das Dialogfeld „Spalten auswählen" wird geöffnet. **Deaktivieren**
    Sie die folgenden Spalten.

    a.  StateProvinceID

    b.  Location

    c.  LastEditedBy

    d.  ValidFrom

    e.  ValidTo

    f.  CountryID

25. Wählen Sie **OK** aus.

![](images3/media/image24.png){width="2.241547462817148in"
height="3.5205479002624673in"}

Beachten Sie, dass der Prozess dem von Power Query ähnelt. Alle Schritte
sind sowohl im Bereich „Angewendete Schritte" rechts als auch in der
visuellen Ansicht aufgezeichnet. Wir benennen „Merge-Abfrage" und „Laden
aktivieren" um, damit die Daten aus dieser Abfrage geladen werden.

26. Klicken Sie im Bereich „Abfragen" (links) **mit der rechten
    Maustaste** auf **„Merge-Abfrage"**. Wählen Sie **Umbenennen** aus,
    und benennen Sie die Abfrage in **Geo** um.

27. Klicken Sie im Bereich „Abfragen" (links) **mit der rechten
    Maustaste** auf **Geo-Abfrage**. Wählen Sie **Laden aktivieren**
    aus, um diese Abfrage zu aktivieren.

28. Stellen Sie sicher, dass die Abfragen „Cities", „States" und
    „Countries" **deaktiviert** sind.

29. Wählen Sie **Speichern** unten rechts im Power Query-Editor aus.

![](images3/media/image25.png){width="6.5in"
height="2.477370953630796in"}

Wir werden zum visuellen Abfrage-Editor weitergeleitet. Jetzt speichern
wir diese Abfrage als Ansicht.

> **Hinweis**: Alle Schritte, die wir mit dem Power Query-Editor
> ausgeführt haben, können auch mit dem Editor für Visual-Abfragen
> ausgeführt werden.

30. Wählen Sie im Menü des Editors für Visual-Abfragen **Als Ansicht
    speichern** aus.

![](images3/media/image26.png){width="6.568577209098863in"
height="2.019780183727034in"}

Das Dialogfeld „Als Ansicht speichern" wird geöffnet. Beachten Sie, dass
die SQL-Abfrage verfügbar ist. Sie können sie überprüfen, wenn Sie die
SQL überprüfen möchten.

31. Geben Sie als **Ansichtsname** **Geo** ein.

32. Wählen Sie **OK** aus, um die Ansicht zu speichern.

![](images3/media/image27.png){width="3.141111111111111in"
height="3.593688757655293in"}

Sie erhalten eine Benachrichtigung, nachdem die Ansicht gespeichert
wurde.

33. Erweitern Sie im Explorer-Bereich (links) **Ansichten**. Wir haben
    die neu erstellte Ansicht „Geo".

![](images3/media/image28.png){width="3.6146030183727036in"
height="3.8093285214348205in"}

### Aufgabe 3: Ansicht „Reseller" mithilfe einer Visual-Abfrage erstellen

Wir erstellen die Ansicht „Reseller", indem wir die Tabelle „Customers"
mit der Tabelle „BuyingGroups" zusammenführen. Dieses Mal erstellen wir
die Ansicht mithilfe einer Visual-Abfrage.

1.  Klicken Sie im oberen Menü auf das Dropdownmenü neben **Neue
    SQL-Abfrage (1)**, und wählen Sie dann **Neue Visual-Abfrage (2)**
    aus.

2.  Um eine Abfrage zu erstellen, müssen wir Tabellen zum visuellen
    Abfragebereich hinzufügen. Klicken Sie auf die Auslassungspunkte
    neben der Tabelle **BuyingGroups (1)** und wählen Sie **In
    Zeichenbereich einfügen (2)** aus.

![](images3/media/image29.png){width="6.020833333333333in"
height="5.885181539807524in"}

3.  Wiederholen Sie die gleichen Schritte für die Tabelle **Customers**.

4.  Wählen Sie die Abfrage „Customers" aus. Wenn die Abfrage „Customers"
    ausgewählt ist, weist sie einen blauen Rand auf und hinter „Tabelle"
    befindet sich ein „**+**"-Zeichen (dies gibt an, dass wir nach
    „Tabelle" einen Schritt hinzufügen). Wenn kein „**+**"-Zeichen
    hinter der Tabelle angezeigt wird, haben Sie möglicherweise einen
    anderen Schritt ausgewählt. Wählen Sie „Tabelle" aus und es kann
    losgehen).

<!-- -->

5.  Wählen Sie im Menü der Visual-Abfrage **Kombinieren -\> Abfragen
    zusammenführen** aus.

![](images3/media/image30.png){width="5.305297462817148in"
height="2.0912259405074365in"}

Das Dialogfeld „Zusammenführen" wird geöffnet, wobei „Customers" als
oberste Tabelle ausgewählt ist.

6.  Wählen Sie in der **rechten Tabelle für zusammenführung** die Option
    **BuyingGroups** aus.

7.  Wählen Sie **BuyingGroupID**-Spalten aus beiden Tabellen aus. Wir
    führen eine Verknüpfung über diese Spalte aus.

8.  Wählen Sie **Innerhalb** als **Art des Joins** aus.

9.  Wählen Sie **OK** aus.

![](images3/media/image31.png){width="3.5694444444444446in"
height="3.553070866141732in"}

10. Klicken Sie in der **Datenansicht** (unterer Bereich) auf den
    **Doppelpfeil** neben der Spalte **BuyingGroups** (letzte Spalte
    rechts), um die Spalten von BuyingGroups auszuwählen.

11. Es wird ein Bereich geöffnet. Wählen Sie die Spalte
    **BuyingGroupName** aus.

12. Klicken Sie auf **OK**.

![](images3/media/image32.png){width="6.440259186351706in"
height="2.672201443569554in"}

Wir benötigen nicht alle Spalten. Wir wählen nur die aus, die wir
benötigen.

13. Wählen Sie im Menü der Visual-Abfrage **Spalten verwalten -\>
    Spalten auswählen** aus.

![](images3/media/image33.png){width="5.51167760279965in"
height="1.2541830708661417in"}

14. Das Dialogfeld „Spalten auswählen" wird geöffnet. **Wählen Sie** die
    folgenden Spalten aus.

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

15. Wählen Sie **OK** aus.

![](images3/media/image34.png){width="2.314682852143482in"
height="3.236517935258093in"}

16. Wir benennen die Spalte „BuyingGroupName" um. **Doppelklicken Sie in
    der Datenansicht auf die Spaltenüberschrift „BuyingGroupName"**,
    damit sie bearbeitet werden kann.

17. **Benennen** Sie die Spalte in **ResellerCompany** um.

![](images3/media/image35.png){width="6.641031277340333in"
height="1.819400699912511in"}

Beachten Sie, dass in der Tabelle „Customers" alle Schritte dokumentiert
sind. Jetzt speichern wir diese Ansicht.

18. Wir müssen die Customer-Abfrage speichern, da sie alle Schritte
    umfasst. Wir müssen das Laden aktivieren. Wählen Sie die
    **Auslassungspunkte** im Feld der Abfrage **Customer** aus.

19. Stellen Sie sicher, dass die Option **Laden aktivieren** aktiviert
    ist.

![](images3/media/image36.png){width="6.1389140419947505in"
height="2.0699890638670166in"}

> **Hinweis**: Das Feld **Customer** sollte einen blauen Rand haben,
> wenn die Option „Laden aktivieren" aktiviert ist.

20. Wählen Sie im Menü der Visual-Abfrage **Als Ansicht speichern** aus.

![](images3/media/image37.png){width="6.908840769903762in"
height="1.1772659667541556in"}

Das Dialogfeld „Als Ansicht speichern" wird geöffnet. Beachten Sie, dass
die SQL-Abfrage verfügbar ist. Sie können sie überprüfen, indem Sie sie
auswählen.

21. Geben Sie als **Ansichtsname** **Reseller** ein.

22. Wählen Sie **OK** aus, um die Ansicht zu speichern.

![](images3/media/image38.png){width="3.078186789151356in"
height="3.591218285214348in"}

Sie erhalten eine Benachrichtigung, nachdem die Ansicht gespeichert
wurde.

23. Erweitern Sie im Explorer-Bereich (links) **Ansichten**. Wir haben
    die neu erstellte Ansicht „Reseller".

![](images3/media/image39.png){width="3.15371062992126in"
height="3.870194663167104in"}

### Aufgabe 4: Ansicht „Sales" mithilfe einer Visual-Abfrage erstellen

Lassen Sie uns die Ansicht „Sales" erstellen, die durch das
Zusammenführen der Tabellen „InvoiceLineItems" und „Invoices" mit der
Ansicht „Reseller" erstellt wird. Wir haben diese Abfrage in Power BI
Desktop. Wir kopieren den Code aus dem Erweiterten Editor. Aber bevor
wir den Code kopieren, müssen wir mit der Visual-Abfrage eine
Zusammenführungstabelle erstellen, da in der Visual-Abfrage keine leere
Abfrage erstellt werden kann. Lassen Sie uns diese Methode ausprobieren.

1.  Klicken Sie im oberen Menü auf das Dropdownmenü neben **Neue
    SQL-Abfrage**, und wählen Sie dann **Neue visuelle Abfrage** aus.

![](images3/media/image14.png){width="6.5in"
height="3.7154418197725283in"}

2.  Aus dem Abschnitt **Explorer -\> Tabelle** müssen wir die Tabellen
    in den Abschnitt für Visual-Abfragen hinzufügen. Klicken Sie auf die
    Auslassungspunkte neben der Tabelle **InvoiceLineItems** und wählen
    Sie **In Zeichenbereich einfügen** aus.

3.  Wiederholen Sie die gleichen Schritte für die Tabelle **Invoices**.

4.  Aus dem Abschnitt **Explorer -\> Ansichten** müssen wir die Tabellen
    in den Abschnitt für Visual-Abfragen hinzufügen. Klicken Sie auf die
    Auslassungspunkte neben der Tabelle **Reseller** und wählen Sie **In
    Zeichenbereich einfügen** aus.

5.  Wählen Sie im Editor für Visual-Abfragen das **Im Popup-Fenster
    öffnen** aus, um den Power Query-Editor zu öffnen.

![](images3/media/image40.png){width="6.5in"
height="2.1683956692913386in"}

6.  Wählen Sie bei ausgewählter Abfrage **InvoiceLineItems** im Menüband
    **Start (2)-\> Kombinieren (3) -\> Abfragen zusammenführen (4) -\>
    Abfragen als neue Abfrage zusammenführen (5).** Das Dialogfeld
    „Abfragen zusammenführen" wird geöffnet.

![](images3/media/image41.png){width="6.5in"
height="1.7182699037620297in"}

7.  Wählen Sie in der **linken zusammenzuführenden Tabelle** die Option
    **InvoiceLineItems** aus.

8.  Wählen Sie in der **rechten zusammenzuführenden Tabelle** die Option
    **Invoices** aus.

9.  Wählen Sie **InvoiceID**-Spalten aus beiden Tabellen aus. Wir führen
    eine Verknüpfung über diese Spalte aus.

10. Wählen Sie **Innerhalb** als **Art des Joins** aus.

11. Wählen Sie **OK** aus.

![](images3/media/image42.png){width="3.134802055993001in"
height="3.6385214348206474in"}

Wir kopieren den Code aus Power BI Desktop, und fügen ihn über
„Erweiterter Editor" ein.

12. Öffnen Sie **FAIAD.pbix** im Ordner **Report** auf dem Desktop Ihrer
    Übungsumgebung, falls dies noch nicht erfolgt ist.

13. Wählen Sie im Menüband **Start \> Daten transformieren** aus. Das
    Power Query-Fenster wird geöffnet. Wie Sie in der vorherigen Übung
    festgestellt haben, sind die Abfragen im linken Bereich nach
    Datenquelle organisiert.

![](images3/media/image43.png){width="6.430285433070866in"
height="3.5388899825021873in"}

14. Wählen Sie im linken Bereich **Abfragen** unter dem Ordner
    **ADLSData** **(1)** die Abfrage **Sales (2)** aus**.**

15. Wählen Sie im Menüband die Registerkarte **Start -\> Erweiterter
    Editor (3)** aus. Das Dialogfenster „Erweiterter Editor" wird
    geöffnet.

![](images3/media/image44.png){width="3.8192333770778655in"
height="3.063990594925634in"}

> **Hinweis:** Wenn Sie den erweiterten Editor nicht finden können,
> können Sie unter **Start-\> Abfrage -\> Erweiterter Editor** darauf
> zugreifen.

16. **Wählen Sie Code aus Zeile 3** (#\"Expanded Invoice\" ...) bis zur
    letzten Codezeile aus.

17. **Klicken Sie mit der rechten Maustaste**, und wählen Sie
    **Kopieren** aus.

18. Wählen Sie **Abbrechen** aus, um „Erweiterter Editor" zu schließen.

![](images3/media/image45.png){width="5.733089457567804in"
height="4.031353893263342in"}

19. **Navigieren Sie zurück zum Browser**, in dem der Power Query-Editor
    geöffnet ist.

20. Stellen Sie sicher, dass Sie die Abfrage **Merge** ausgewählt haben.

21. Wählen Sie im Menüband die Registerkarte **Start -\> Erweiterter
    Editor** aus. Das Dialogfenster „Erweiterter Editor" wird geöffnet.

![](images3/media/image46.png){width="6.330345581802275in"
height="1.7288757655293088in"}

22. Fügen Sie am **Ende von Zeile 2 ein Komma** hinzu (Source =
    Table.NestedJoin(InvoiceLineItems, {\"InvoiceID\"}, Invoices,
    {\"InvoiceID\"}, \"Invoices\", JoinKind.Inner).

23. Klicken Sie auf die **Eingabetaste**, um eine neue Zeile zu
    beginnen.

24. Geben Sie auf Ihrer Tastatur **STRG+V** ein, um den Code einzufügen,
    den Sie aus Power BI Desktop kopiert haben.

> **Hinweis**: Wenn Sie in der Übungsumgebung arbeiten, wählen Sie die
> **Auslassungspunkte (...)** oben rechts auf dem Bildschirm aus.
> Verwenden Sie den Schieberegler, um das **VM Native Clipboard** **zu
> aktivieren**. Wählen Sie im Dialogfeld „OK" aus. Nachdem Sie die
> Abfragen eingefügt haben, können Sie diese Option deaktivieren.

![](images3/media/image47.png){width="6.5in"
height="0.8786472003499562in"}

![](images3/media/image48.png){width="4.3001323272090985in"
height="2.8552187226596675in"}

25. Markieren Sie die letzten beiden Codezeilen (in der Quelle), und
    **löschen** Sie sie.

26. Wählen Sie **OK** aus, um die Änderungen zu speichern.

![](images3/media/image49.png){width="6.5in"
height="3.1184044181977253in"}

Wenn es einfacher ist, löschen Sie den gesamten Code im erweiterten
Editor, und fügen Sie den folgenden Code in „Erweiterter Editor" ein.

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

27. Sie werden zum Power Query-Editor weitergeleitet. Im linken Bereich
    „Abfragen" müssen Sie **auf die „Merge"-Abfrage doppelklicken**, um
    sie umzubenennen.

28. **Benennen Sie** Merge-Abfrage in **Sales** um.

29. Klicken Sie mit der rechten Maustaste auf die Abfrage „Sales", und
    wählen Sie **Laden aktivieren** aus, damit die Abfrage geladen
    werden kann.

![](images3/media/image50.png){width="3.1032469378827647in"
height="3.1032469378827647in"}

30. Wählen Sie **Speichern** aus, um das Power Query-Dialogfeld zu
    speichern und zu schließen. Sie werden zum visuellen Abfrage-Editor
    weitergeleitet.

31. Wählen Sie im Menü der Visual-Abfrage **Als Ansicht speichern** aus.
    Das Dialogfeld „Als Ansicht speichern" wird geöffnet. Beachten Sie,
    dass die SQL-Abfrage verfügbar ist. Sie können sie bei Bedarf
    überprüfen.

32. Geben Sie als **Ansichtsname (1)** **Sales** ein.

33. Wählen Sie **OK (2)** aus, um die Ansicht zu speichern.

![](images3/media/image51.png){width="6.241526684164479in"
height="6.947916666666667in"}

Sie erhalten eine Benachrichtigung, nachdem die Ansicht gespeichert
wurde.

34. Erweitern Sie im Explorer-Bereich (links) **Ansichten**. Wir haben
    die neu erstellte Ansicht „Sales".

![](images3/media/image52.png){width="4.258929352580927in"
height="2.757451881014873in"}

### Aufgabe 5: Ansicht „Product" mithilfe einer Visual-Abfrage erstellen

Wir erstellen die Ansicht „Product", die durch das Zusammenführen der
Tabellen **ProductItem**, **ProductItemGroup** und **ProductGroups**
erstellt wird. Um voranzukommen, kopieren wir den Code in „Erweiterter
Editor".

1.  Klicken Sie im oberen Menü auf das Dropdownmenü neben **Neue
    SQL-Abfrage (1)**, und wählen Sie dann **Neue visuelle Abfrage (2)**
    aus.

![](images3/media/image53.jpeg){width="6.182702318460192in"
height="3.8in"}

2.  Aus dem Abschnitt Explorer müssen wir die Tabellen in den Abschnitt
    für Visual-Abfragen hinzufügen. Klicken Sie auf die
    Auslassungspunkte neben der Tabelle **ProductItem (1)** und wählen
    Sie **In Zeichenbereich einfügen (2)** aus.

![](images3/media/image54.png){width="5.791666666666667in"
height="7.355974409448819in"}

3.  Wiederholen Sie die gleichen Schritte für die Tabellen
    **ProductItemGroup** und **ProductGroups**.

4.  Wählen Sie im Editor für Visual-Abfragen das **Symbol für den
    Fokusmodus** aus, um den Power Query-Editor zu öffnen.

![](images3/media/image55.png){width="6.5in"
height="2.1364687226596675in"}

5.  Wählen Sie bei ausgewählter Abfrage **ProductItem** im Menüband
    **Start (1)-\> Kombinieren (2) -\> Abfragen zusammenführen (3) -\>
    Abfragen als neue Abfrage zusammenführen (4).** Das Dialogfeld zum
    Zusammenführen wird geöffnet.

![](images3/media/image56.png){width="6.5in"
height="3.5646741032370954in"}

6.  Wählen Sie in der **linken zusammenzuführenden Tabelle** die Option
    **ProductItem** aus.

7.  Wählen Sie in der **rechten zusammenzuführenden Tabelle** die Option
    **ProductItemGroup** aus.

8.  Wählen Sie **StockItemID**-Spalten aus beiden Tabellen aus. Wir
    führen eine Verknüpfung über diese Spalte aus.

9.  Wählen Sie als **Art des Joins** die Option **linker äußerer Join**
    aus.

10. Wählen Sie **OK** aus. Es wird eine neue Merge-Abfrage erstellt.

![](images3/media/image57.png){width="3.0027515310586175in"
height="3.4722222222222223in"}

11. Wählen Sie bei ausgewählter Merge-Abfrage im Menüband **Start -\>
    Erweiterter Editor** aus. Das Dialogfenster „Erweiterter Editor"
    wird geöffnet.

![](images3/media/image58.png){width="6.105435258092738in"
height="1.727952755905512in"}

> **Hinweis:** Wenn Sie den erweiterten Editor nicht finden können,
> können Sie unter **Start-\> Abfrage -\> Erweiterter Editor** darauf
> zugreifen.

12. **Wählen Sie den gesamten Code** in „Erweiterter Editor" aus, und
    **löschen** Sie ihn.

13. **Fügen** Sie den folgenden Code in „Erweiterter Editor" ein.

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

14. Wählen Sie **OK** aus, um „Erweiterter Editor" zu schließen. Sie
    werden zum Power Query-Editor weitergeleitet.

![](images3/media/image59.png){width="6.5in"
height="3.056968503937008in"}

15. Im Bereich „Abfragen" auf der linken Seite müssen Sie **auf die
    „Merge"-Abfrage doppelklicken**, um sie umzubenennen.

16. **Ändern Sie den Namen** der Merge-Abfrage zu **Product**.

17. Klicken Sie mit der rechten Maustaste auf die Abfrage „Product", und
    wählen Sie **Laden aktivieren** aus, damit die Abfrage geladen
    werden kann.

18. Wählen Sie **Speichern** aus, um das Power Query-Dialogfeld zu
    speichern und zu schließen. Die werden zur visuellen Abfrage
    weitergeleitet.

![](images3/media/image60.png){width="6.5in"
height="2.4794181977252845in"}

19. Wählen Sie im Menü der Visual-Abfrage **Als Ansicht speichern** aus.
    Das Dialogfeld „Als Ansicht speichern" wird geöffnet. Beachten Sie,
    dass die SQL-Abfrage verfügbar ist. Sie können sie bei Bedarf
    überprüfen.

20. Geben Sie als **Ansichtsname** **Product** ein.

21. Wählen Sie **OK** aus, um die Ansicht zu speichern.

![](images3/media/image61.png){width="2.9999737532808397in"
height="3.5155949256342955in"}

Sie erhalten eine Benachrichtigung, nachdem die Ansicht gespeichert
wurde.

22. Erweitern Sie im Explorer-Bereich (links) **Ansichten**. Wir haben
    die neu erstellte Ansicht „Product".

![](images3/media/image62.png){width="3.82626968503937in"
height="3.0836001749781277in"}

Wir haben die Daten aus der ADLS Gen2-Datenquelle transformiert. In
dieser Übung haben wir gelernt, wie man Verknüpfungen erstellt und
verschiedene Optionen zur Verwendung von Ansichten für Visual-Abfragen
zum Transformieren von Daten erkundet.

In der nächsten Übung erfahren wir, wie man Dataflow Gen2 verwendet und
eine Verknüpfung zu einem anderen Lakehouse erstellt.

# Referenzen

Bei Fabric Analyst in a Day (FAIAD) lernen Sie einige der wichtigsten
Funktionen von Microsoft Fabric kennen. Im Menü des Dienstes finden Sie
in der Hilfe (?) Links zu praktischen Informationen.

![](images3/media/image63.png){width="1.8726399825021873in"
height="4.536075021872266in"}

Nachfolgend finden Sie weitere Angebote zur weiteren Arbeit mit
Microsoft Fabric.

-   Die vollständige [Ankündigung der allgemeinen Verfügbarkeit von
    Microsoft Fabric](https://aka.ms/Fabric-Hero-Blog-Ignite23) finden
    Sie im Blogbeitrag.

-   Fabric bei einer [interaktiven
    Vorstellung](https://aka.ms/Fabric-GuidedTour) kennenlernen

-   Zur [kostenlosen Testversion von Microsoft
    Fabric](https://aka.ms/try-fabric) anmelden

-   [Website von Microsoft Fabric](https://aka.ms/microsoft-fabric)
    besuchen

-   Mit Modulen von [Fabric Learning](https://aka.ms/learn-fabric) neue
    Qualifikationen erwerben

-   [Technische Dokumentation zu Fabric](https://aka.ms/fabric-docs)
    lesen

-   [Kostenloses E-Book zum Einstieg in
    Fabric](https://aka.ms/fabric-get-started-ebook) lesen

-   Mitglied der [Fabric-Community](https://aka.ms/fabric-community)
    werden, um Fragen zu stellen, Feedback zu geben und sich mit anderen
    auszutauschen

Lesen Sie die detaillierteren Blogs zur Ankündigung der Fabric-Umgebung:

-   [Blog zum Data Factory-Funktionsbereich in
    Fabric](https://aka.ms/Fabric-Data-Factory-Blog) 

-   [Blog zum Data Engineering-Funktionsbereich von Synapse in
    Fabric](https://aka.ms/Fabric-DE-Blog) 

-   [Blog zum Data Science-Funktionsbereich von Synapse in
    Fabric](https://aka.ms/Fabric-DS-Blog) 

-   [Blog zum Data Warehousing-Funktionsbereich von Synapse in
    Fabric](https://aka.ms/Fabric-DW-Blog) 

-   [Blog zum Real-Time Analytics-Funktionsbereich von Synapse in
    Fabric](https://aka.ms/Fabric-RTA-Blog)

-   [Blog mit Ankündigungen zu Power BI](https://aka.ms/Fabric-PBI-Blog)

-   [Blog zum Data Activator-Funktionsbereich in
    Fabric](https://aka.ms/Fabric-DA-Blog) 

-   [Blog zu Verwaltung und Governance in
    Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

-   [Blog zu OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

-   [Blog zur Dataverse- und Microsoft
    Fabric-Integration](https://aka.ms/Dataverse-Fabric-Blog)

> © 2023 Microsoft Corporation. Alle Rechte vorbehalten.
>
> Durch die Verwendung der vorliegenden Demo/Übung stimmen Sie den
> folgenden Bedingungen zu:
>
> Die in dieser Demo/Übung beschriebene Technologie/Funktionalität wird
> von der Microsoft Corporation bereitgestellt, um Feedback von Ihnen zu
> erhalten und Ihnen Wissen zu vermitteln. Sie dürfen die Demo/Übung nur
> verwenden, um derartige Technologiefeatures und Funktionen zu bewerten
> und Microsoft Feedback zu geben. Es ist Ihnen nicht erlaubt, sie für
> andere Zwecke zu verwenden. Es ist Ihnen nicht gestattet, diese
> Demo/Übung oder einen Teil derselben zu ändern, zu kopieren, zu
> verbreiten, zu übertragen, anzuzeigen, auszuführen, zu
> vervielfältigen, zu veröffentlichen, zu lizenzieren, zu transferieren
> oder zu verkaufen oder aus ihr abgeleitete Werke zu erstellen.
>
> DAS KOPIEREN ODER VERVIELFÄLTIGEN DER DEMO/ÜBUNG (ODER EINES TEILS
> DERSELBEN) AUF EINEN/EINEM ANDEREN SERVER ODER SPEICHERORT FÜR DIE
> WEITERE VERVIELFÄLTIGUNG ODER VERBREITUNG IST AUSDRÜCKLICH UNTERSAGT.
>
> DIESE DEMO/ÜBUNG STELLT BESTIMMTE
> SOFTWARE-TECHNOLOGIE-/PRODUKTFEATURES UND FUNKTIONEN, EINSCHLIESSLICH
> POTENZIELLER NEUER FEATURES UND KONZEPTE, IN EINER SIMULIERTEN
> UMGEBUNG OHNE KOMPLEXE EINRICHTUNG ODER INSTALLATION FÜR DEN OBEN
> BESCHRIEBENEN ZWECK BEREIT. DIE TECHNOLOGIE/KONZEPTE IN DIESER
> DEMO/ÜBUNG ZEIGEN MÖGLICHERWEISE NICHT DAS VOLLSTÄNDIGE
> FUNKTIONSSPEKTRUM UND FUNKTIONIEREN MÖGLICHERWEISE NICHT WIE DIE
> ENDGÜLTIGE VERSION. UNTER UMSTÄNDEN VERÖFFENTLICHEN WIR AUCH KEINE
> ENDGÜLTIGE VERSION DERARTIGER FEATURES ODER KONZEPTE. IHRE ERFAHRUNG
> BEI DER VERWENDUNG DERARTIGER FEATURES UND FUNKTIONEN IN EINER
> PHYSISCHEN UMGEBUNG KANN FERNER ABWEICHEND SEIN.
>
> **FEEDBACK**. Wenn Sie Feedback zu den Technologiefeatures, Funktionen
> und/oder Konzepten geben, die in dieser Demo/Übung beschrieben werden,
> gewähren Sie Microsoft das Recht, Ihr Feedback in jeglicher Weise und
> für jeglichen Zweck kostenlos zu verwenden, zu veröffentlichen und
> gewerblich zu nutzen. Außerdem treten Sie Dritten kostenlos sämtliche
> Patentrechte ab, die erforderlich sind, damit deren Produkte,
> Technologien und Dienste bestimmte Teile einer Software oder eines
> Dienstes von Microsoft, welche/welcher das Feedback enthält, verwenden
> oder eine Verbindung zu dieser/diesem herstellen können. Sie geben
> kein Feedback, das einem Lizenzvertrag unterliegt, aufgrund dessen
> Microsoft Drittparteien eine Lizenz für seine Software oder
> Dokumentation gewähren muss, weil wir Ihr Feedback in diese aufnehmen.
> Diese Rechte bestehen nach Ablauf dieser Vereinbarung fort.
>
> DIE MICROSOFT CORPORATION LEHNT HIERMIT JEGLICHE GEWÄHRLEISTUNGEN UND
> GARANTIEN IN BEZUG AUF DIE DEMO/ÜBUNG AB, EINSCHLIESSLICH ALLER
> AUSDRÜCKLICHEN, KONKLUDENTEN ODER GESETZLICHEN GEWÄHRLEISTUNGEN UND
> GARANTIEN DER HANDELSÜBLICHKEIT, DER EIGNUNG FÜR EINEN BESTIMMTEN
> ZWECK, DES RECHTSANSPRUCHS UND DER NICHTVERLETZUNG VON RECHTEN
> DRITTER. MICROSOFT MACHT KEINERLEI ZUSICHERUNGEN BZW. ERHEBT KEINERLEI
> ANSPRÜCHE IM HINBLICK AUF DIE RICHTIGKEIT DER ERGEBNISSE UND DES AUS
> DER VERWENDUNG DER DEMO/ÜBUNG RESULTIERENDEN ARBEITSERGEBNISSES BZW.
> BEZÜGLICH DER EIGNUNG DER IN DER DEMO/ÜBUNG ENTHALTENEN INFORMATIONEN
> FÜR EINEN BESTIMMTEN ZWECK.
>
> **HAFTUNGSAUSSCHLUSS**
>
> Diese Demo/Übung enthält nur einen Teil der neuen Features und
> Verbesserungen in Microsoft Power BI. Einige Features können sich
> unter Umständen in zukünftigen Versionen des Produkts ändern. In
> dieser Demo/Übung erhalten Sie Informationen über einige, aber nicht
> über alle neuen Features.

