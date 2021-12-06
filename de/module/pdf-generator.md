# PDF Generator

Mit dem Modul "PDF-Produktblätter" können Sie benutzerfreundlich PDF-Dateien mit Produktinformationen erstellen, die für bestimmte Kanäle und / oder Gebietsschemas erstellt wurden.

Das Modul ermöglicht, PDF-Dateien mit folgenden Informationen zu generieren:
- alle Produktinformationen;
- [kanalspezifische](#product-sheet-settings) Produktinformationen;
- [länderspezifische](#product-sheet-settings) Produktinformationen.


## Administratorfunktionen

Im Allgemeinen hat das Modul "PDF-Produktblätter" keine Einstellungen. Um jedoch PDF-Dateien für die länderspezifischen Produktdaten generieren zu können, müssen die mehrsprachigen Parameter konfiguriert werden. Gehen Sie dazu zu "Administration> Multi-Languages" und wählen Sie die gewünschte (n) Sprache (n) aus der Dropdown-Liste aus Liste, die angezeigt wird, wenn Sie auf das Feld "Eingabesprachenliste" klicken:

![Multi-Lang-Setup](../../modules/_assets/pdf-generator/multi-lang-setup.jpg)

Klicken Sie auf die Schaltfläche "Speichern", um die Konfiguration zu übernehmen, oder auf "Abbrechen", um den Vorgang abzubrechen.

## Benutzerfunktionen

Nach der Modulinstallation wird die Option "Produktblatt" sowohl im Menü [Aktionen für einzelne Datensätze](https://atropim.com/help/products#single-record-actions) auf der Seite Produktdatensatzliste / Plattenansicht 

![Listenansicht](../../modules/_assets/pdf-generator/list-view.jpg)

und auf der Produktseite [Detailansicht](https://atropim.com/help/views-and-panels#detail-view) angezeigt:

![Detailansicht](../../modules/_assets/pdf-generator/detail-view.jpg)

Klicken Sie auf diese Option, um das Popup-Fenster des Produktblattgenerators zu öffnen:

![Generator-Popup](../../modules/_assets/pdf-generator/generator-popup.jpg)

### Produktblatteinstellungen

Geben Sie im Popup-Fenster des Produktblattgenerators die folgenden Parameter an:

- **Produktblattvorlage** - Die Liste der Vorlagen zum Generieren der PDF-Dateien. Die Option "Standardproduktblattvorlage" ist standardmäßig vorhanden. Um die Liste der Vorlagen zu erweitern, wenden Sie sich bitte an uns oder an Ihren Entwickler.
- **Kanal** - Die Liste der Kanäle, die mit dem angegebenen Produktdatensatz verknüpft sind. Die Option "Nur globaler Bereich" ist standardmäßig definiert, d. H. Alle Produktattributwerte mit dem Bereich "Global" werden in der PDF-Datei generiert. Um kanalspezifische Attributwerte (einschließlich Mehrkanalattribute) zu generieren, wählen Sie den gewünschten Kanalnamen in der Liste aus:

![Channel](../../modules/_assets/pdf-generator/channel.jpg)

Bitte beachten Sie, dass die Dropdown-Liste "Kanal" nur eine Option enthält, wenn keine Kanäle mit dem Produktdatensatz verknüpft sind - "Nur globaler Bereich".

- **Gebietsschema** - Die Liste der Gebietsschemas gemäß den vom [Administrator] konfigurierten Optionen (# Administratorfunktionen). Für jedes Gebietsschema sollte eine separate PDF-Datei generiert werden.

### Produktblattgenerierung

Klicken Sie auf die Schaltfläche "Produktblatt generieren", um den Vorgang zu starten. Infolgedessen wird die gemäß den definierten Parametern generierte PDF-Datei in einer neuen Registerkarte geöffnet:

![Generiertes PDF](../../modules/_assets/pdf-generator/generated-pdf.jpg)

Hier werden alle Daten aus den Feldern "ÜBERSICHT" und "PRODUKTATTRIBUTE" des angegebenen Produktdatensatzes angezeigt.

Bitte beachten Sie, dass in der generierten PDF-Datei "Keine" für die nicht ausgefüllten Datenfelder und Attribute angezeigt wird.

Wenn im Bereich "BILDER" des jeweiligen Produkts oder mit dem im Produktblattgenerator definierten Kanalbereich keine Datensätze vorhanden sind, wird in der generierten PDF-Datei keine Bildvorschau angezeigt:

![Kein Bild](../../modules/_assets/pdf-generator/no-image.jpg)

Die generierten Produktblätter können später als Anhänge zu Berichten, Tabellen, gedruckten Katalogen mit Produktinformationen usw. verwendet werden.

### Generieren von Massenproduktblättern

AtroPIM unterstützt auch die Möglichkeit, Produktblätter für bis zu 200 Produkte gleichzeitig über die Massenaktion "PDF generieren" in den Produktdatensätzen [Listenansicht](https://atropim.com/help/products#listing) zu generieren:

![Massengenerierung](../../modules/_assets/pdf-generator/mass-generation.jpg)

Das Popup des Produktblattgenerators wird angezeigt:

![Massengenerator-Popup](../../modules/_assets/pdf-generator/mass-generator-popup.jpg)

Da nur globale Produktwerte für das Produktarray generiert werden, gibt es in diesem Popup keinen "Channel" -Parameter.

Klicken Sie auf die Schaltfläche "Produktblatt generieren", um den Vorgang zu starten. Das Popup [Warteschlangenmanager](https://atropim.com/help/user-interface#queue-manager) wird geöffnet und zeigt den Betriebsstatus und den Fortschritt an:

![Warteschlangenmanager](../../modules/_assets/pdf-generator/queue-manager.jpg)

Klicken Sie im Warteschlangenmanager-Popup auf die Schaltfläche "Herunterladen", um den Vorgang abzuschließen und die generierte PDF-Datei auf einer separaten Registerkarte anzuzeigen.

Wenn Sie PDF-Dateien für Produktdatensätze in einem [**Katalog**](https://atropim.com/help/catalogs) generieren müssen, filtern Sie die Produkte nach dem gewünschten Katalog und verwenden Sie die Massenaktion "PDF generieren":

![Katalogfilter](../../modules/_assets/pdf-generator/catalog-filter.jpg)

### Produktblätter Historie

Um die Liste der generierten Produktblätter anzuzeigen, klicken Sie im Popup des Produktblattgenerators auf die Schaltfläche "Verlauf", die über die Massenaktion "PDF generieren" auf der Seite "Produktlistenansicht" ausgeführt wird:

![Produktblattverlauf](../../modules/_assets/pdf-generator/product-sheets-history.jpg)

Auf der Listenansicht "Anhänge" werden die Datensätze nach ihrer Erstellungszeit sortiert. Sie können in einem separaten Popup über die Option "Ansicht" im Menü "Einzelaufzeichnungsaktionen" angezeigt werden:

![Verlaufsansicht](../../modules/_assets/pdf-generator/history-view.jpg)

Um einen Produktblatt-Verlaufsdatensatz zu entfernen, verwenden Sie die Option "Entfernen" und bestätigen Sie Ihre Entscheidung im angezeigten Popup.

