Dieses Modul ermöglicht die Single Sign-On-Autorisierung (SSO) in Ihrer AtroCore-Anwendung mithilfe von Azure Active Directory.

## Benutzerfunktionen

Wenn in der Administration des Systems die Authentifizierung über Azure AD aktiviert ist, erscheint neue Schaltfläche auf der Anmeldeseite.

![Anmeldeseite](../../modules/_assets/azure-active-directory-sso/login-via-azure.png)

Wenn Sie auf die Schaltfläche `Login via Azure AD` klicken, werden Sie zur Microsoft-Anmeldeseite weitergeleitet. Nach der Anmeldung dort werden Sie auf die Atrocore-Anmeldeseite weitergeleitet und werden vollautomatisch mit Ihrem Benutzerkonto authentifiziert. Wenn die Autorisierung fehlschlägt, bleiben Sie auf der Anmeldeseite.

## Neue Anwendung in Azure Active Directory registrieren

Sie müssen die AtroCore-Anwendung in Ihrem Azure Active Directory registrieren. Dafür benötigen Sie sollen ein Administratorkonto. Rufen Sie https://portal.azure.com/ auf. Dort sehen Sie die Liste aller verfügbaren Azure-Dienste. Wählen Sie Azure Active Directory.

![Azure Active Directory](../../modules/_assets/azure-active-directory-sso/azure-active-directory.png)

Klicken Sie im linken Kontextmenü auf `App-Registrierungen`. Sie sehen die Liste der verfügbaren Anwendungen. Um eine neue Anwendung hinzuzufügen, klicken Sie auf die Schaltfläche `Neue Registrierung`.

![Neue Registrierung](../../modules/_assets/azure-active-directory-sso/app-registration-page.png)

Auf der Registrierungsseite müssen Sie den Anwendungsnamen eingeben und den unterstützten Kontotyp auswählen. Empfohlen – Konten nur in diesem Organisationsverzeichnis (nur Standardverzeichnis – Einzelmandant). Sie müssen auch den Umleitungs-URI angeben, an den Azure den Benutzer umleitet, nachdem er erfolgreich authentifiziert wurde. Wählen Sie als App-Typ für die Weiterleitungs-URI `Single-Page-Anwendung (SPA)`.

> Die Umleitungs-URI soll wie folgt eingetragen werden: https://ihre_domain/api/v1/AzureAuth, wobei `your_domain` - der Domänenname sollte der von Ihrer AtroCore-Anwendung sein. Dieses Feld sollte immer ausgefüllt werden!

Nach dem Speichern der neuen Registrierung werden Sie auf die Übersichtsseite weitergeleitet. Hier finden Sie die Application (Client) ID, die für die Konfiguration in Atrore benötigt wird. Also bitte irgendwo speichern.

![Anwendungsübersichtsseite](../../modules/_assets/azure-active-directory-sso/application-page.png)

Gehen Sie zur Seite Zertifikate und Geheimnisse, um die geheime Zeichenfolge für den Client zu erstellen. Klicken Sie auf die Schaltfläche `Neues Client-Geheimnis`.

![Client-Geheimnisseite](../../modules/_assets/azure-active-directory-sso/secrets-page.png)

Geben Sie im modalen Fenster die Beschreibung des Geheimnisses und die Ablaufzeit für Client-Geheimnis ein. Klicken Sie dann auf `Hinzufügen`, um die Änderungen zu speichern.

![Client-Geheimnis-Modal](../../modules/_assets/azure-active-directory-sso/create-secret.png)

Notieren Sie diesen Wert (nicht die ID!), es wird im nächsten Schritt verwendet.

(**Optional**) Jetzt sollen Sie die API-Berechtigungen für Ihre Anwendung festlegen. Gehen Sie auf die entsprechende Seite, Sie sehen eine Liste der aktiven Berechtigungen. Klicken Sie auf `Neue Berechtigung hinzufügen`. Wählen Sie im Block "Microsoft Graph" den Wert `Directory.Read.All` und `Application` als Typ. Klicken Sie anschließend auf `Zustimmung des Administrators erteilen`.

![Api permissions](../../modules/_assets/azure-active-directory-sso/api-permissions.png)

Auf der Authentifizierungsseite können Sie die Umleitungs-URL festlegen, wenn Sie dies vorher noch nicht getan haben. Wählen Sie auch im Block `Implicit grant and hybrid flows` die Option `ID tokens (used for implicit and hybrid flows)` aus.

![Authentifizierung](../../modules/_assets/azure-active-directory-sso/alternative-adding-redirect-url.png)

![Authentifizierungstoken](../../modules/_assets/azure-active-directory-sso/token-type-select.png)

## Azure Active Directory-Benutzer erstellen

Um einen neuen Benutzer in Active Directory zu erstellen, melden Sie sich auf https://portal.azure.com/ mit Ihrem Administratorkonto an, wählen Sie den Azure Active Directory  und klicken Sie im linken Menü auf den Link `Benutzer`. Dort sehen Sie die Liste der bestehenden Accounts.

![Benutzerlistenseite](../../modules/_assets/azure-active-directory-sso/add-user.png)

Klicken Sie auf die Schaltfläche `Neuer Benutzer`, um einen neuen Benutzer hinzuzufügen.

![Benutzerseite erstellen](../../modules/_assets/azure-active-directory-sso/create-user-page.png)

Wählen Sie `Benutzer erstellen` und füllen Sie alle erforderlichen Felder aus und klicken Sie auf `Erstellen`. Klicken Sie in der Benutzerliste auf den soeben erstellten neuen Benutzer, um seine Detailinformationen anzusehen. Bitte notieren Sie die `Objekt-ID`, die Sie auf der Benutzerkonfigurationsseite in der AtroCore-Anwendung eingeben sollten.

![Benutzerübersichtsseite](../../modules/_assets/azure-active-directory-sso/user-overview-page.png)

## Administratorfunktionen

### Modulkonfiguration

Nachdem Sie die neue Anwendungsregistrierung und die Benutzer in Ihrem Azure Active Directory eingerichtet haben, sollen Sie diese mit Ihrer AtroCore-Anwendung verbinden.

Gehen Sie zur Seite `Administration > System > Authentifizierung` (https://your_domain/#Admin/authentication) und geben Sie die `Application (Object) ID`, die Sie sich zuvor notiert haben, in das Feld `Azure Active Directory Client ID` ein. Füllen Sie auch die Felder `Azure Active Directory Tenant ID` und `Azure Active Directory Client Secret` mit den entsprechenden Werten aus dem Azure-Portal aus.

![AtroCore-Anwendung einrichten](../../modules/_assets/azure-active-directory-sso/atrocore-azure-settings.png)

Stellen Sie sicher, dass Sie die `Site URL` auf der `Administration > System > Settings` Seite (https://your_domain/#Admin/settings) eingerichtet haben.

![Site-URL-Einstellungen](../../modules/_assets/azure-active-directory-sso/site-settings.png)

### Benutzer Konfiguration

Um einen AtroCore-Benutzer mit einem Azure-Benutzer zu binden, gehen Sie zur Benutzerliste (https://your_domain/#User) und wählen Sie den passenden Benutzer-Datensatz aus. Tragen Sie in das Feld `Azure User Object ID` den Wert ein, den Sie aus dem Azure-Feld `Objekt-ID` für den entsprechenden Benutzer notiert haben. 

Wenn Sie Azure Active Directory bereits unter "Administration > System > Authentifizierung" konfiguriert haben und den API-Zugriff auf die Azure AD Benutzerdaten für die AtroPIM-Anwendung erlaubt haben, werden die Felder wie "Vorname", " Nachname" und "Azure User Object ID" automatisch ausgefüllt, sobald Sie die E-Mail eingetragen haben, vorausgesetzt der Benutzer mit der E-Mail existiert.

![AtroCore-Benutzereinstellung](../../modules/_assets/azure-active-directory-sso/atrocore-user-settings.png)

## Kaufbedingungen
Der Preis gilt zzgl. MwSt. Für den oben angegebenen Preis erhalten Sie das Modul einschließlich Updates und Upgrades für den Zeitraum eines Jahres. Nach dieser Zeit können Sie Ihre letzte Version des Moduls weiter verwenden oder das Modul mit einem Rabatt von 50% erneut erwerben, um das Recht zu bekommen, die Updates und Upgrades für ein weiteres Jahr zu erhalten. Im Übrigen gilt unser [ELV](https://atropim.com/de/elv) (Endbenutzerlizenzvertrag). 

## Anpassung
Das Modul kann an Ihre Bedürfnisse angepasst werden – zusätzliche Funktionen können hinzu programmiert werden, vorhandene Funktionen können geändert werden. Bitte kontaktieren Sie uns diesbezüglich. Es gelten unsere [AGB](https://atropim.com/de/agb) (Allgemeine Geschäftsbedingungen).

## Demo
Bitte kontaktieren Sie uns und wir senden Ihnen die Zugangsdaten für die Demoversion.
