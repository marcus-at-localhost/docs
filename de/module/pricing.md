# Pricing

Das Modul "Pricing" bietet erweiterte Preisfunktionen, sodass unterschiedliche Preise für verschiedene Kundengruppen und Kanäle angezeigt werden können. Dank der automatischen Preisumrechnung lassen sich auch skalierbare Preise in verschiedenen Währungen erstellen, abhängig von der Anzahl der Artikel und Preise. Die Preisumrechnung kann in Relation zu einem festen Wechselkurs oder durch manuelle Preiseingabe für jeden einzelnen Artikel erfolgen.

## Installation

Um das Modul "Pricing" zu installieren, geht man zunächst auf auf `Administration > Modulmanager`. Suchen Sie dieses Modul in der Liste `Shop` und klicken Sie auf `Installieren`:

![Pricing install](_assets/pricing-install.jpg)

Wählen Sie im angezeigten Installations-Pop-up-Fenster die gewünschte Version aus und klicken Sie auf den Button `Installieren`. Der Modulhintergrund wird grün und in den Bereich `Installiert` des Modulmanagers verschoben. Klicken Sie auf `Update starten`, um die Installation zu bestätigen.

> Bitte beachten Sie, dass nach dem Systemupdate alle Nutzer abgemeldet werden.

Um das Modul „Pricing“ zu aktualisieren / zu entfernen, nutzen Sie die entsprechenden Optionen aus dem Menü für einzelne Datensatzaktionen in `Administration > Modulmanager`.

## Funktionen für den Administrator

Das Modul "Pricing" erweitert die Funktionalität des [AtroPIM](https://atropim.com/help/what-is-atropim)-Systems, sodass eine weitere Beschreibung des Moduls im Kontext von AtroPIM erfolgt.

Nach der Installation des Moduls wird im [Navigationsmenü](https://atropim.com/help/user-interface#navigation-menu) ein neues Element `Preisprofile` hinzugefügt, und das Feld `Preis` auf der [Produktdetailseite](https://atropim.com/help/products) wird durch das Panel `PRODUKTPREISE` ersetzt.

## Konfiguration der Währung

Um die Währungen für die Preisberechnung für die Produktverteilung zu konfigurieren, gehen Sie zur `Administration > Währung`:

![Currency settings](_assets/currency-settings.jpg)

Die `EUR`-Währung ist standardmäßig eingestellt, Sie können die Liste jedoch um beliebig viele Währungen erweitern. Dafür klicken Sie auf das Feld `Währungsliste` und wählen Sie die gewünschten Optionen aus der angezeigten Dropdown-Liste aus:

![Currency list](_assets/currency-list.jpg)

Hier können Sie auch die Standardwährung (für die Erstellung neuer Datensätze) und das Währungsformat via entsprechender Dropdown-Listen auswählen. Geben Sie im Feld `Dezimalstellen der Währung` die Anzahl der Dezimalstellen an, die in Währungsfeldern und Berechnungen zu verwenden sind, oder lassen Sie das Feld leer, damit alle ausgefüllten Dezimalstellen angezeigt werden.

Im Panel `Wechselkurse` sollten Sie auch die Wechselkurse für die in der Währungsliste verfügbaren Währungen angeben. Wählen Sie hierzu die Basiswährung aus und geben Sie deren Kurswert entsprechend anderen Währungen ein:

![Currency rates](_assets/currency-rates.jpg)

Klicken Sie auf den Button `Speichern`, um Ihre Währungskonfiguration zu übernehmen, oder auf `Abbrechen`, um den Vorgang abzubrechen.

### Zugangsrechte

Standardmäßig ist die Preisfunktion für alle Nutzer aktiviert. Bei Bedarf kann sie jedoch für bestimmte Nutzerrollen auf der Seite `Administration> Rollen> Rollenname` deaktiviert werden:

![Access rights](_assets/pricing-role-cfg.jpg)

Bitte beachten Sie, dass die Zugangsrechte für `Kanäle` und `Produkte` ebenfalls aktiviert werden sollten.

## Funktionen für den Nutzer

Nachdem der Administrator das Modul "Pricing" installiert und konfiguriert hat, kann der Nutzer mit Preisprofilen gemäß seinen Rollenrechten arbeiten.

## Preisprofil

Ein Preisprofil ist eine konfigurierbare Preisvariante, mit der man verschiedene Preise für unterschiedliche Kundengruppen in Zahlen und Währungen definieren kann. Beispiele für Preisprofile sind: reguläre Preise, Großhandelspreise, VIP-Kundenpreise, Saisonrabatte usw.

### Erstellung

Um einen neuen Preisprofildatensatz zu erstellen, klicken Sie im Navigationsmenü auf `Preisprofile`, um zur [Listenansicht](https://atropim.com/help/views-and-panels#list-view) der Profile zu gelangen, und klicken Sie dann auf den Button `Preisprofil erstellen`. Das gemeinsame Erstellungsfenster wird geöffnet:

![Profile creation](_assets/profile-create.jpg)

Geben Sie hier den gewünschten Namen für den zu erstellenden Preisprofildatensatz ein und definieren Sie die Währungen, die hier zu nutzen sind (gemäß den Währungen, die im Schritt zur [Konfiguration der Währung](#konfiguration-der-währung) definiert wurden).

> Bitte beachten Sie, dass die Standardwährung nicht entfernt werden kann.

Aktivieren Sie das Preisprofil und geben Sie bei Bedarf dessen Beschreibung ein.

Bitte beachten Sie, dass nur aktivierte Profile zu den verfügbaren Produkten hinzugefügt werden.

Klicken Sie auf den Button `Speichern`, um die Erstellung des Preisprofils abzuschließen und zu dessen [Konfiguration](#konfiguration) fortzuschreiten, oder klicken Sie auf `Abbrechen`, um den Vorgang abzubrechen.

### Konfiguration

Die Seite mit der [Detailansicht](https://atropim.com/help/views-and-panels#detail-view) des Preisprofils wird geöffnet, wenn das Preisprofil gespeichert wird:

![Price profile details](_assets/price-profile-details.jpg)

Hier im Panel `Kanäle` werden die Beziehungen zwischen den [Kanälen](https://atropim.com/help/channels), über welche die Produktverteilung erfolgt, und den Preisprofilen erstellt und verwaltet; das ist durch die Auswahl vorhandener Preisprofile oder Erstellung neuer Kanäle möglich:

 ![Channels panel](_assets/channels-panel.jpg)

Weitere Informationen zu diesen Optionen finden Sie im entsprechenden [Artikel](https://atropim.com/help/products#channels) im AtroPIM-Benutzerhandbuch.

Alternativ können Sie die Preisprofile mit Kanälen im Panel `PREISPROFILE` auf der gewünschten Kanaldetailseite verknüpfen:

![Price profiles panel](_assets/price-profiles-panel.jpg)

## Einstellung des Produktpreises

Sobald das aktive Preisprofil erstellt wurde, wird es zu allen Produkten hinzugefügt und im Panel `PRODUKTPREISE` angezeigt:

![Price profiles panel](_assets/product-prices-panel.jpg)

Hier können Sie die Produktpreise für alle Währungen bestimmen, die für das angegebene Preisprofil vorkonfiguriert sind. Wählen Sie dazu im Aktionsmenü des gewünschten Preisprofils die Option `Bearbeiten`:

![Price editing option](_assets/price-edit-option.jpg)

Im angezeigten Bearbeitung-Popup ist der Produktpreis in der Standardwährung einzugeben. Der Preis für andere Währungen wird automatisch anhand der festgelegten Wechselkurswerte berechnet:

![Price value](_assets/price-value.jpg)

Allerdings können Sie den automatisch berechneten Preis ändern; dazu ist die Checkbox `Bearbeiten` für die gewünschte Währung zu setzen und ein anderer Wert einzugeben:

![Price edited](_assets/price-edited.jpg)

> Bitte beachten Sie, dass der automatisch berechnete Wert wiederhergestellt wird, wenn Sie die Checkbox `Bearbeiten` deaktivieren. Wenn Sie die Checkbox `Bearbeiten` erneut setzen, wird der zuvor eingegebene Wert nicht wiederhergestellt.

Wenn Sie den Produktpreis skalieren müssen, d.h. nach der Anzahl der verkauften Artikel differenzieren, klicken Sie auf `Hinzufügen`, und geben Sie die gewünschten Preiswerte in hinzugefügte Felder ein:

![Price added](_assets/price-added.jpg)

Klicken Sie auf `Entfernen`, um bei Bedarf die ganze Reihe von Preiswerten für alle Währungen zu löschen.

Um die Änderungen zu übernehmen, klicken Sie auf den Button `Speichern`. Die definierten Produktpreiswerte werden im Panel `PRODUKTPREISE` angezeigt:

![Filled price profiles panel](_assets/product-prices-panel-filled.jpg)

Bitte beachten Sie, dass nur die ersten drei Preise im dem Panel angezeigt werden. Um  alle Preise anzusehen, öffnen Sie ein separates Popup über die Option `Ansehen` im Aktionsmenü des angegebenen Preisprofils:

![View product price](_assets/product-price-view.jpg)

Um einen Produktdatensatz zu [duplizieren](https://atropim.com/help/products#duplicating), in dem die Preiswerte konfiguriert sind, muss man im angezeigten Bestätigungs-Popup auswählen, ob die Preise ebenfalls dupliziert werden sollen:

![Duplicate product prices](_assets/product-duplicate-prices.jpg)

## Kanäle und Produktpreise

Die Anzeige des Panels `PRODUKTPREISE` hängt von den Währungseinstellungen der mit dem Produktdatensatz verknüpften Kanäle ab. Die Preisdetails für nur aktive Kanäle werden gemäß den Preisprofilen angezeigt, sortiert nach Währungen:

![Channels and prices](_assets/channels-prices.jpg)

## Erweiterte Funktionen des Moduls

Das Modul "Pricing" zusammen mit dem Modul ["Product Variants"](https://atropim.com/store/product-variants) kann darüber hinaus effizient genutzt werden, um die Preise für konfigurierbare Produkte und deren Varianten zu differenzieren. Besuchen Sie unseren [Shop](https://atropim.com/de/shop), um mehr über das Modul "Product Variants" und andere verfügbare Add-Ons zu erfahren.

## Kaufbedingungen

Der Preis gilt zzgl. MwSt. Für den oben angegebenen Preis erhalten Sie das Modul einschließlich Updates und Upgrades für den Zeitraum eines Jahres. Nach dieser Zeit können Sie Ihre letzte Version des Moduls weiter verwenden oder das Modul mit einem Rabatt von 50% erneut erwerben, um das Recht zu bekommen, die Updates und Upgrades für ein weiteres Jahr zu erhalten. Im Übrigen gilt unser [ELV](https://atropim.com/de/elv) (Endbenutzerlizenzvertrag). 

## Anpassung
Das Modul kann an Ihre Bedürfnisse angepasst werden – zusätzliche Funktionen können hinzu programmiert werden, vorhandene Funktionen können geändert werden. Bitte kontaktieren Sie uns diesbezüglich. Es gelten unsere [AGB](https://atropim.com/de/agb) (Allgemeine Geschäftsbedingungen).

## Demo
Bitte kontaktieren Sie uns und wir senden Ihnen die Zugangsdaten für die Demoversion.

