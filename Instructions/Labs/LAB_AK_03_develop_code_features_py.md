---
lab:
  title: "Übung: Entwickeln neuer Codefeatures mithilfe von GitHub\_Copilot-Tools (Python)"
  description: 'Erfahren Sie, wie Sie die Entwicklung neuer Codefeatures mithilfe von GitHub Copilot in Visual Studio Code beschleunigen.'
---

# Entwickeln neuer Codefeatures mithilfe von GitHub Copilot

Die Funktion zur Code-Vervollständigung und interaktivem Chat von GitHub Copilot helfen Entwickelnden, Code schneller und mit weniger Fehlern zu schreiben. Sie stellt Vorschläge für Codeausschnitte, Funktionen und sogar ganze Klassen basierend auf dem Kontext des geschriebenen Codes bereit. In dieser Übung verwenden Sie GitHub Copilot, um die Entwicklung neuer Codefunktionen in Visual Studio Code zu beschleunigen.

Diese Übung dauert ca. **30** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, müssen Sie ein eigenes GitHub-Konto und ein eigenes GitHub Copilot-Abonnement bereitstellen. Wenn Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses eigenes Konto <a href="https://go.microsoft.com/fwlink/?linkid=2320148" target="_blank">registrieren</a> und einen GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement in Ihrer Übungsumgebung haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement verwenden, um diese Übung abzuschließen.

## Vor der Installation

Ihre Übungsumgebung muss Folgendes enthalten: Git 2.48 oder höher, Python 3.10 oder höher, Visual Studio Code mit dem Python-Erweiterungsformular Microsoft und Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

Wenn Sie einen lokalen PC als Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Um Hilfe beim Konfigurieren Ihres lokalen PCs als Übungsumgebung zu erhalten, öffnen Sie den folgenden Link in einem Browser: <a href="https://microsoftlearning.github.io/mslearn-github-copilot-dev/Instructions/Labs/LAB_AK_00_configure_lab_environment_py.html" target="_blank">Konfigurieren Sie die Ressourcen Ihrer Übungsumgebung</a>.

- Um Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code zu erhalten, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren Sie GitHub Copilot in Visual Studio Code</a>.

Wenn Sie eine gehostete Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Um Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code zu erhalten, fügen Sie die folgende URL in die Seitennavigationsleiste eines Browsers ein: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren Sie GitHub Copilot in Visual Studio Code</a>.

- Öffnen Sie eine Eingabeaufforderung, und führen Sie die folgenden Befehle aus:

    Um sicherzustellen, dass Visual Studio Code für die Verwendung der richtigen Version von Python konfiguriert ist, stellen Sie sicher, dass die Python-Version 3.10 oder höher installiert ist:

    ```bash
    python --version
    ```

    Um sicherzustellen, dass Git für die Verwendung Ihres Namens und Ihrer E-Mail-Adresse konfiguriert ist, aktualisieren Sie die folgenden Befehle mit Ihren Informationen und führen Sie sie dann aus:

    ```bash

    git config --global user.name "John Doe"

    ```

    ```bash

    git config --global user.email johndoe@example.com

    ```

## Übungsszenario

Sie sind Entwicklerin bzw. Entwickler und arbeiten in der IT-Abteilung Ihrer lokalen Community. Die Back-End-Systeme, die die öffentliche Bibliothek unterstützen, wurden in einem Brand zerstört. Ihr Team muss ein temporäres Projekt entwickeln, damit die Mitarbeitenden der Bibliothek ihre Vorgänge verwalten können, bis das System ersetzt werden kann. Ihr Team hat GitHub Copilot ausgewählt, um den Entwicklungsprozess zu beschleunigen.

Eine erste Version Ihrer Bibliotheksanwendung wurde von Endbenutzenden getestet und es werden mehrere zusätzliche Funktionen angefordert. Ihr Team hat sich damit einverstanden erklärt, an den folgenden Funktionen zu arbeiten:

- Buchverfügbarkeit: Ermöglicht es Bibliothekaren, den Verfügbarkeitsstatus eines Buchs zu bestimmen. Diese Funktion soll eine Nachricht anzeigen, die Aufschluss darüber gibt, ob ein Buch ausgeliehen werden kann. Ist das Buch aktuell an eine andere Person ausgeliehen, soll das Rückgabedatum angezeigt werden.

- Buchausleihe: Ermöglicht es Bibliothekaren, ein Buch an einen Kunden auszuleihen (sofern das Buch verfügbar ist). Diese Funktion soll eine Buchausleihoption für eine Person anzeigen, „Loans.json“ mit der neuen Ausleihe aktualisieren und die aktualisierten Ausleihdetails für die Person anzeigen.

- Buchreservierungen: Ermöglicht es Bibliothekaren, ein Buch für einen Kunden zu reservieren (es sei denn, das Buch ist bereits reserviert). Dieses Feature soll einen neuen Buchreservierungsprozess implementieren. Für dieses Feature müssen unter Umständen eine neue Datei namens „Reservations.json“ sowie neue Klassen und Schnittstellen erstellt werden, die zur Unterstützung des Reservierungsprozesses erforderlich sind.

Alle Teammitglieder arbeiten jeweils an einer der neuen Funktionen und kommen anschließend wieder zusammen. Sie werden an der Funktion arbeiten, um den Verfügbarkeitsstatus eines Buches zu ermitteln. Ihr Kollege arbeitet an dem Feature, das es ermöglicht, ein Buch an einen Kunden auszuleihen. Das letzte Feature (also die Buchreservierung für einen Kunden) wird entwickelt, nachdem die beiden anderen Features fertig sind.

Diese Übung umfasst die folgenden Aufgaben:

1. Richten Sie die Bibliotheksanwendung in Visual Studio Code ein.

1. Verwenden Sie Visual Studio Code zum Erstellen eines GitHub-Repositorys für die Bibliotheksanwendung.

1. Erstellen eines Branch für die Buchverfügbarkeit im Coderepository

1. Entwickeln eines neuen Buchverfügbarkeitsfeatures

    - Verwenden von GitHub Copilot-Vorschlägen, um den Code schneller und präziser zu implementieren
    - Synchronisieren Ihrer Codeaktualisierungen mit dem Branch für die Buchverfügbarkeit Ihres Remoterepositorys

1. Mergen Sie Ihre Updates zur Buchverfügbarkeit in den Mainbranch des Repositorys.

## Einrichten der Bibliotheksanwendung in Visual Studio Code

Sie müssen die vorhandene Anwendung herunterladen, die Codedateien extrahieren und dann das Projekt in Visual Studio Code öffnen.

Gehen Sie folgendermaßen vor, um die Bibliotheksanwendung einzurichten:

1. Öffnen Sie ein Browserfenster in Ihrer Übungsumgebung.

1. Um eine ZIP-Datei mit der Bibliotheksanwendung herunterzuladen, fügen Sie die folgende URL in die Adressleiste Ihres Browsers ein: [GitHub Copilot-Übung – Entwickeln von Codefeatures](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM3Python.zip)

    Die ZIP-Datei heißt **AZ2007LabAppM3Python.zip**.

1. Extrahieren Sie die Dateien aus der Datei **AZ2007LabAppM3Python.zip**.

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner mit Downloads in Ihrer Übungsumgebung.

    1. Klicken Sie mit der rechten Maustaste auf **AZ2007LabAppM3Python.zip** und wählen Sie dann **Alle extrahieren** aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Öffnen Sie den Ordner mit den extrahierten Dateien und kopieren Sie dann den Ordner **AccelerateDevGHCopilot** an einen Speicherort, auf den Sie einfach zugreifen können, z. B. Ihren Windows-Ordner „Desktop“.

1. Öffnen Sie den Ordner **AccelerateDevGHCopilot** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Übungsumgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows-Ordner „Desktop“ und wählen Sie **AccelerateDevGHCopilot** und dann **Ordner auswählen** aus.

1. Überprüfen Sie in der EXPLORER-Ansicht von Visual Studio Code die folgende Projektstruktur:

    - AccelerateDevGHCopilot/library   ├── application_core   ├── console   ├── infrastructure   └── tests   └── readme.md

1. Stellen Sie sicher, dass die Anwendung erfolgreich ausgeführt wird.

    Öffnen Sie beispielsweise ein Terminal in Visual Studio Code, navigieren Sie zum Verzeichnis **AccelerateDevGHCopilot/library** und führen Sie den folgenden Befehl aus:

    ```bash
    python -m unittest discover -v tests
    ```

    Es werden einige Warnungen angezeigt, es sollten aber keine Fehler auftreten.

## Erstellen des GitHub-Repositorys für Ihren Code

Wenn Sie das GitHub-Repository für Ihren Code erstellen, können Sie Ihre Arbeit mit anderen teilen und am Projekt zusammenarbeiten.

> **HINWEIS:** Sie verwenden Ihr eigenes GitHub-Konto, um ein privates GitHub-Repository für die Bibliotheksanwendung zu erstellen.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie ein Browserfenster, und navigieren Sie zu Ihrem GitHub-Konto.

    Die GitHub-Anmeldeseite lautet: [https://github.com/login](https://github.com/login).

1. Melden Sie sich bei Ihrem GitHub-Konto an.

1. Öffnen Sie Ihr GitHub-Kontomenü, und wählen Sie dann **Ihre Repositorys** aus.

1. Wechseln Sie zum Visual Studio Code-Fenster.

1. Öffnen Sie in Visual Studio Code die Ansicht „Quellcodeverwaltung“.

1. Wählen Sie **Publish to GitHub** (Auf GitHub veröffentlichen) aus.

1. Name für das Repository **AccelerateDevGHCopilot**.

    > **HINWEIS:** Wenn Sie nicht bei GitHub in Visual Studio Code angemeldet sind, werden Sie aufgefordert, sich anzumelden. Nachdem Sie sich angemeldet haben, autorisieren Sie Visual Studio Code mit den angeforderten Berechtigungen.

1. Wählen Sie **Im privaten GitHub-Repository veröffentlichen** aus.

1. Beachten Sie, dass Visual Studio Code während des Veröffentlichungsprozesses Statusmeldungen anzeigt.

    Nach Abschluss des Veröffentlichungsprozesses wird eine Meldung angezeigt, dass Ihr Code erfolgreich im von Ihnen angegebenen GitHub-Repository veröffentlicht wurde.

1. Wechseln Sie zum Browserfenster mit Ihrem GitHub-Konto.

1. Öffnen Sie das neue AccelerateDevGHCopilot-Repository in Ihrem GitHub-Konto.

    Wenn Ihr AccelerateDevGHCopilot-Repository nicht angezeigt wird, aktualisieren Sie die Seite. Wenn das Repository immer noch nicht angezeigt wird, führen Sie die folgenden Schritte durch:

    1. Wechseln Sie zu Visual Studio Code.
    1. Öffnen Sie Ihre Benachrichtigungen. Beim Veröffentlichen des neuen Repositorys wurde eine Benachrichtigung generiert.
    1. Wählen Sie **Auf GitHub öffnen** aus, um Ihr Repository zu öffnen.

## Erstellen eines neuen Branch im Repository

Bevor Sie mit der Entwicklung des neuen Buchverfügbarkeitsfeatures beginnen, müssen Sie einen neuen Branch im Repository erstellen. Dadurch können Sie an dem neuen Feature arbeiten, ohne dass sich dies auf den Mainbranch des Repositorys auswirkt. Wenn die neue Funktion bereit ist, können Sie sie in den Mainbranch mergen.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Stellen Sie sicher, dass das Projekt „AccelerateDevGHCopilot“ in Visual Studio Code geöffnet ist.

1. Wählen Sie die Ansicht „Quellcodeverwaltung“ aus, und stellen Sie sicher, dass das lokale Repository mit dem Remoterepository synchronisiert wird (Pullen oder Synchronisieren).

1. Wählen Sie links unten im Fenster die Option **main** aus.

1. Um einen neuen Zweig zu erstellen, geben Sie **Buchverfügbarkeit** ein und wählen Sie dann **+ Neuen Zweig erstellen**.

1. Wählen Sie **Branch veröffentlichen** aus, Um den neuen Branch in das Remoterepository zu pushen.

## Verwenden von GitHub Copilot zum Entwickeln einer neuen Funktion zur Buchverfügbarkeit

In diesem Abschnitt der Übung lassen Sie sich bei der Implementierung einer neuen Funktion für die Bibliotheksanwendung von GitHub Copilot unterstützen. Die angeforderte Funktion ermöglicht es einer Bibliothekarin oder einem Bibliothekar, zu überprüfen, ob ein Buch zum Ausleihen verfügbar ist, ein gängiges Szenario, das derzeit nicht von Ihrer aktuellen Bibliotheksanwendung unterstützt wird.

Um die Funktion zur Buchverfügbarkeit zu implementieren, müssen Sie die folgenden Updates ausführen:

- Fügen Sie eine neue Aktion **SEARCH_BOOKS** zur Enumeration **CommonActions** in **library/console/common_actions.py** hinzu.

- Aktualisieren Sie die Methode **WriteInputOptions** in **library/console/console_app.py**.

  - Fügen Sie Unterstützung für die neue Option **CommonActions.SEARCH_BOOKS** hinzu.
  - Zeigen Sie die Option an, um zu überprüfen, ob ein Buch zum Ausleihen verfügbar ist.

- Aktualisieren Sie die Methode **ReadInputOptions** in **library/console/console_app.py**.

  - Fügen Sie Unterstützung für die neue Option **CommonActions.SEARCH_BOOKS** hinzu.

- Aktualisieren Sie die Methode **PatronDetails** in **library/console/console_app.py**.

  - Fügen Sie **CommonActions.SEARCH_BOOKS** zu den **Optionen** hinzu, bevor Sie **ReadInputOptions** aufrufen.
  - Fügen Sie **else if** hinzu, um mit der Aktion **SEARCH_BOOKS** umzugehen.
  - Der Block **else if** sollte eine neue Methode namens **SEARCH_BOOKS** aufrufen.

- Erstellen Sie eine neue Methode **SEARCH_BOOKS** in **library/console/console_app.py**.

  - Die Methode **SEARCH_BOOKS** sollte den Buchtitel lesen, der von Benutzenden angegeben wird.
  - Überprüfen Sie, ob ein Buch zur Ausleihe verfügbar ist, und zeigen Sie eine Meldung mit folgenden Angaben an:

    - „**Buchtitel** ist zur Ausleihe verfügbar“ oder
    - „**Buchtitel** ist derzeit von einer anderen Person ausgeliehen. Das Rückgabedatum ist **loan.DueDate**.“

GitHub Copilot Chat kann Ihnen bei der Implementierung der Code-Updates helfen, die zum Fertigstellen der neuen Funktion erforderlich sind.

- Sie können Inline-Chat-Sitzungen verwenden, um kleinere, diskretere Code-Updates basierend auf Ihren Anforderungen zu implementieren.
- Sie können die Chat-Ansicht verwenden, um an größeren Code-Updates zu arbeiten, die möglicherweise einen Unterhaltungsansatz und iterativeren Ansatz erfordern.

### Implementieren von Updates zur Buchverfügbarkeit mit Copilot-Inline-Chat

Mit **Copilot-Inline-Chat**-Sitzungen können Sie direkt in Ihrem Code-Editor mit GitHub Copilot interagieren. Sie können den Inline-Chat verwenden, um Fragen zu stellen, Codevorschläge anzufordern und Erklärungen für den von GitHub Copilot generierten Code zu erhalten.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie die EXPLORER-Ansicht.

1. Erweitern Sie das Projekt **library/console**.

1. Öffnen Sie die Datei **console/common_actions.py**und **wählen** Sie die Klasse **CommonActions** aus.

    Sie müssen eine neue Aktion **SEARCH_BOOKS** zu **CommonActions** hinzufügen.

1. Öffnen Sie den Inline-Chat: Zeigen Sie auf die Auswahl und klicken Sie mit der rechten Maustaste. Es wird ein Menü geöffnet. Wählen Sie **„Copilot“** aus und anschließend **Editor-Inline-Chat**.

1. Geben Sie den folgenden Prompt ein:

    ```plaintext
    Update selection to include a new `SEARCH_BOOKS` action.
    ```

    GitHub Copilot sollte eine Code-Update vorschlagen, die die neue Aktion **SEARCH_BOOK** zur Klasse **CommonActions** hinzufügt.

1. Überprüfen Sie die vorgeschlagene Aktualisierung, und wählen Sie anschließend **Annehmen** aus.

    Ihr aktualisierter Code sollte dem folgenden Codeschnipsel ähneln:

    ```python

    class CommonActions(Flag):
        REPEAT = 0
        SELECT = auto()
        QUIT = auto()
        SEARCH_PATRONS = auto()
        SEARCH_BOOKS = auto() # added
        RENEW_PATRON_MEMBERSHIP = auto()
        RETURN_LOANED_BOOK = auto()
        EXTEND_LOANED_BOOK = auto()
    ```

    Beachten Sie das Hinzufügen von `SEARCH_BOOKS = auto()` zu `CommonActions`.

1. Öffnen Sie die Datei **library/console/console_app.py**.

1. Suchen die Methode `write_input_options` in der Klasse `ConsoleApp` und und wählen Sie sie dann aus. Zeigen Sie auf die Auswahl und klicken Sie mit der rechten Maustaste. Es wird ein Menü geöffnet. Wählen Sie **„Copilot“** aus und anschließend **Editor-Inline-Chat**.

    Sie müssen Unterstützung für die neue `CommonActions.SEARCH_BOOKS`-Option hinzufügen. Wenn die Option `SEARCH_BOOKS` vorhanden ist, zeigen Sie die Option an, um zu überprüfen, ob ein Buch zur Ausleihe verfügbar ist.

1. Öffnen Sie den Inlinechat, und geben Sie folgenden Prompt ein:

    ```plaintext
    Update selection to include an option for the `CommonActions.SEARCH_BOOKS` action. Use the letter "b" and the message "to check for book availability".
    ```

    GitHub Copilot sollte eine Codeaktualisierung vorschlagen, die einen neuen `if`-Block für die `SEARCH_BOOKS`-Aktion hinzufügt.

1. Überprüfen Sie die vorgeschlagene Aktualisierung, und wählen Sie anschließend **Annehmen** aus.

    Die vorgeschlagene Aktualisierung sollte in etwa wie der folgende Codeschnipsel aussehen:

    ```python
        def write_input_options(self, options):
        print("Input Options:")
        if options & CommonActions.RETURN_LOANED_BOOK:
            print(' - "r" to mark as returned')
        if options & CommonActions.EXTEND_LOANED_BOOK:
            print(' - "e" to extend the book loan')
        if options & CommonActions.RENEW_PATRON_MEMBERSHIP:
            print(' - "m" to extend patron\'s membership')
        if options & CommonActions.SEARCH_PATRONS:
            print(' - "s" for new search')
        if options & CommonActions.SEARCH_BOOKS:
            print(' - "b" to check for book availability')
        if options & CommonActions.QUIT:
            print(' - "q" to quit')
        if options & CommonActions.SELECT:
            print(' - type a number to select a list item.')
    ```

1. Scrollen Sie nach unten, um die Methode `_handle_patron_details_selection` (oder den Abschnitt zur Eingabebehandlung) in der Datei **library/console/console_app.py** zu suchen und auszuwählen.

    Sie müssen erneut Unterstützung für die neue Option `CommonActions.SEARCH_BOOKS` hinzufügen. Schließen Sie einen Fall ein, der die Auswahl der Aktion „`SEARCH_BOOKS`“ durch Benutzende verarbeitet (z. B. wenn „b“ eingegeben wird).

1. Öffnen Sie den Inlinechat, und geben Sie folgenden Prompt ein:

    ```plaintext
    Update selection to include an option for the `CommonActions.SEARCH_BOOKS` action.
    ```

    GitHub Copilot sollte eine Aktualisierung vorschlagen, die einen neuen Block „`elif`“ hinzufügt, der das Auswählen der Aktion „`SEARCH_BOOKS`“ durch die Benutzerin bzw. den Benutzer behandelt.

1. Überprüfen Sie die vorgeschlagene Aktualisierung, und wählen Sie anschließend **Annehmen** aus.

    Die vorgeschlagene Aktualisierung sollte in etwa wie der folgende Codeschnipsel aussehen:

    ```python
    def _handle_patron_details_selection(self, selection, patron, valid_loans):
    # ...existing code...

        elif selection == 'b':
            # Placeholder for book search functionality
            print("Book search functionality is not implemented yet.")
            return ConsoleState.PATRON_DETAILS
        elif selection.isdigit():
            idx = int(selection)
            if 1 <= idx <= len(valid_loans):
                self.selected_loan_details = valid_loans[idx - 1][1]
                return ConsoleState.LOAN_DETAILS
            print("Invalid selection. Please enter a number shown in the list above.")
            return ConsoleState.PATRON_DETAILS
        else:
            print("Invalid input. Please enter a number, 'm', 's', 'b', or 'q'.")
            return ConsoleState.PATRON_DETAILS
    ```

#### Verwenden von Copilot-Inline-Chat zum Freigeben einer Codeauswahl für GitHub Copilot Chat

1. Stellen Sie sicher, dass GitHub Copilot Chat im **Fragemodus**geöffnet ist.

1. Hier sind zwei Aktionen erforderlich:

    - Sie müssen `CommonActions.SEARCH_BOOKS` zu `options` hinzufügen, bevor Sie `_get_patron_details_input` aufrufen.
    - Sie müssen auch einen Block „`if`“ oder „`elif`“ hinzufügen, um die Auswahl `"b"` für die Aktion „`SEARCH_BOOKS`“ zu verarbeiten. Der Block muss eine neue Methode namens `search_books` aufrufen.

    Sie können beide Anforderungen mit demselben Prompt erfüllen.

1. Suchen Sie die Methode `patron_details` in der Datei **library/console/console_app.py** und **wählen** Sie sie aus.

1. Wenn die Methode `patron_details` noch ausgewählt ist, zeigen Sie mit der Maus auf die Auswahl. **Klicken Sie mit der rechten Maustaste** und ein Menü wird geöffnet. Wählen Sie **„Copilot“** und dann **„Auswahl zum Chat hinzufügen“** aus.

1. Geben Sie den folgenden Prompt ein:

    ```plaintext
    @workspace Update selection to add `CommonActions.SEARCH_BOOKS` to `options` before calling `_get_patron_details_input`. Add an `if` or `elif` block to handle the `"b"` selection for the `SEARCH_BOOKS` action. The block should call a new method named `search_books`.
    ```

    GitHub Copilot Chat sollte ein Code-Update vorschlagen, die `CommonActions.SEARCH_BOOKS` zu `options` hinzufügt, bevor `_get_patron_details_input` aufgerufen wird. Wählen Sie für den angegebenen Code das Symbol „Im Editor übernehmen“ aus.

    ![Screenshot von GitHub Copilot im Fragemodus – Symbol „Im Editor übernehmen“.](./Media/m03-github-copilot-chat-view-response-ask-mode.png)

1. Überprüfen Sie die vorgeschlagene Aktualisierung, und wählen Sie anschließend **Annehmen** aus.
    ```python
    def patron_details(self) -> ConsoleState:
        patron = self.selected_patron_details
        print(f"\nName: {patron.name}")
        print(f"Membership Expiration: {patron.membership_end}")
        loans = self._loan_repository.get_loans_by_patron_id(patron.id)
        print("\nBook Loans History:")

        valid_loans = self._print_loans(loans)

        if valid_loans:
            options = (
                CommonActions.RENEW_PATRON_MEMBERSHIP
                | CommonActions.SEARCH_PATRONS
                | CommonActions.QUIT
                | CommonActions.SELECT
                | CommonActions.SEARCH_BOOKS  # Added SEARCH_BOOKS to options
            )
            selection = self._get_patron_details_input(options)
            return self._handle_patron_details_selection(selection, patron, valid_loans)
        else:
            print("No valid loans for this patron.")
            options = (
                CommonActions.SEARCH_PATRONS
                | CommonActions.QUIT
                | CommonActions.SEARCH_BOOKS  # Added SEARCH_BOOKS to options
            )
            selection = self._get_patron_details_input(options)
            return self._handle_no_loans_selection(selection)

    def _handle_patron_details_selection(self, selection, patron, valid_loans):
        if selection == 'q':
            return ConsoleState.QUIT
        elif selection == 's':
            return ConsoleState.PATRON_SEARCH
        elif selection == 'm':
            status = self._patron_service.renew_membership(patron.id)
            print(status)
            self.selected_patron_details = self._patron_repository.get_patron(patron.id)
            return ConsoleState.PATRON_DETAILS
        elif selection == 'b':
            return self.search_books()  # Call the new search_books method
        elif selection.isdigit():
            idx = int(selection)
            if 1 <= idx <= len(valid_loans):
                self.selected_loan_details = valid_loans[idx - 1][1]
                return ConsoleState.LOAN_DETAILS
            print("Invalid selection. Please enter a number shown in the list above.")
            return ConsoleState.PATRON_DETAILS
        else:
            print("Invalid input. Please enter a number, 'm', 's', 'b', or 'q'.")
            return ConsoleState.PATRON_DETAILS

    def _handle_no_loans_selection(self, selection):
        if selection == 'q':
            return ConsoleState.QUIT
        elif selection == 's':
            return ConsoleState.PATRON_SEARCH
        elif selection == 'b':
            return self.search_books()  # Handle SEARCH_BOOKS when no loans
        else:
            print("Invalid input.")
            return ConsoleState.PATRON_DETAILS

    def search_books(self) -> ConsoleState:
        print("Book search functionality is not implemented yet.")
        return ConsoleState.PATRON_DETAILS

    ```
<!-- TODO: Delete or restore? Previous version that resulted in the Agent bug fix
     ```python

    def patron_details(self) -> ConsoleState:
    patron = self.selected_patron_details
    print(f"\nName: {patron.name}")
    print(f"Membership Expiration: {patron.membership_end}")
    loans = self._loan_repository.get_loans_by_patron_id(patron.id)
    print("\nBook Loans History:")

    valid_loans = self._print_loans(loans)

    if valid_loans:
        options = (
            CommonActions.RENEW_PATRON_MEMBERSHIP
            | CommonActions.SEARCH_PATRONS
            | CommonActions.QUIT
            | CommonActions.SELECT
            | CommonActions.SEARCH_BOOKS
        )
        selection = self._get_patron_details_input(options)
        if selection == 'b':
            return self.search_books()
        return self._handle_patron_details_selection(selection, patron, valid_loans)
    else:
        print("No valid loans for this patron.")
        options = (
            CommonActions.SEARCH_PATRONS
            | CommonActions.QUIT
            | CommonActions.SEARCH_BOOKS
        )
        selection = self._get_patron_details_input(options)
        if selection == 'b':
            return self.search_books()
        return self._handle_no_loans_selection(selection)

    def search_books(self) -> ConsoleState:
        print("Book search option selected.")
        return ConsoleState.PATRON_DETAILS
    ``` 

-->

    > **NOTE**: The code suggested by Inline chat may include stub code for the **search_books()** method as in the previous code sample. You can accept that code stub, but you'll implement the **search_books** method in the next section.

### Implementieren einer Methode „SEARCH_BOOKS“ mithilfe des Fragemodus von Copilot Chat

Es gibt noch einen Schritt, um die Updates zur Buchverfügbarkeit zu implementieren. Erstellen Sie die Methode **search_books**. Die Methode **search_books** liest einen von Benutzenden bereitgestellten Buchtitel, überprüft, ob ein Buch für die Ausleihe verfügbar ist und zeigt eine Meldung an, die den Verfügbarkeitsstatus des Buchs angibt. Sie verwenden die Chat-Ansicht, um die Anforderungen auszuwerten und die Methode **search_books** zu implementieren.

Die Chat-Ansicht von GitHub Copilot bietet eine Unterhaltungsumgebung und interaktive Umgebung, die bei Verwendung von Inline-Chats nicht verfügbar ist. Sie können die Chat-Ansicht verwenden, um Fragen zu stellen, Codevorschläge anzufordern und Erklärungen für den von GitHub Copilot generierten Code zu erhalten. Die Chat-Ansicht unterstützt die folgenden drei Modi:

- Fragemodus: Der Fragemodus wird verwendet, um ein besseres Verständnis ihrer Codebasis zu erhalten, Brainstorming von Ideen zu unterstützen und beim Codieren von Aufgaben zu helfen. Die im Fragemodus generierten Codevorschläge können direkt in Ihre Codebasis implementiert oder in die Zwischenablage kopiert werden.
- Bearbeitungsmodus: Der Bearbeitungsmodus wird verwendet, um Änderungen an Ihrem Code vorzunehmen, z. B. Refactoring oder das Hinzufügen neuer Funktionen. Im Bearbeitungsmodus können Sie Änderungen in mehreren Dateien in Ihrem Projekt vornehmen.
- Agent-Modus: Der Agent-Modus wird verwendet, um eine allgemeine Aufgabe zu definieren und eine Agenten-Codebearbeitungssitzung zu starten, um diese Aufgabe auszuführen. Im Agent-Modus plant Copilot autonom die benötigten Arbeiten und bestimmt die relevanten Dateien und Kontexte. Der Agent kann Änderungen an Ihrem Code vornehmen, Tests ausführen und sogar Ihre Anwendung bereitstellen.
<!-- TODO: line below do we use all 3 listed modes? -->
Sie verwenden die Modi **Inline-Chat**, **Frage** und **Bearbeitung**, um die Methode **search_books** zu implementieren.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Nehmen Sie sich kurz Zeit, um sich Gedanken über die Prozessanforderungen für die Methode **search_books** zu machen.

    Was ist der Prozess, den die Methode abschließen muss? Was ist der Rückgabetyp für diese Methode? Benötigt sie Parameter?

    Die Methode **search_books** sollte den folgenden Prozess implementieren:

    1. Auffordern des Benutzers zur Eingabe eines Buchtitels
    1. Lesen des vom Benutzer angegebenen Buchtitels
    1. Überprüfen, ob ein Buch zum Ausleihen verfügbar ist.
    1. Anzeigen einer Nachricht mit einer der folgenden Aussagen:

        - „**{book.title}** ist für die Ausleihe verfügbar"
        - „**{book.title}** ist derzeit von einer anderen Person ausgeliehen. Das Rückgabedatum ist **{loan.due_date}**.“

    Um die Nachrichtenoptionen zu erstellen, muss Ihr Code auf die folgenden JSON-Dateien zugreifen:

    - **Books.json** ist erforderlich, um den übereinstimmenden **Title** und die **Id** zu finden.
    - **BookItems.json** ist erforderlich, um die **BookId** für jede Ausgabe zu finden (wobei **BookId** mit der **Id** in **Books.json** übereinstimmt).
    - **Loans.json** ist erforderlich, um das **ReturnDate** und das **DueDate** zur Übereinstimmung mit der **BookItemId** zu finden (wobei **BookItemId** mit der **Id** in **BookItems.json** übereinstimmt).

> **Hinweis:**  
> Die **BookItemId** in **Loans.json** bezieht sich auf die **Id** in **BookItems.json**.  
> Die **BookId** in **BookItems.json** bezieht sich auf die **Id** in **Books.json**.

1. Stellen Sie sicher, dass Sie die folgende Methode **search_books** in der Datei **console_app.py** erstellt haben:

    ```python

    def search_books(self) -> ConsoleState:
        print("Book search functionality is not implemented yet.")
        return ConsoleState.PATRON_DETAILS

    ```

    > **HINWEIS:** Entfernen Sie unbedingt alle ggf. von GitHub Copilot erstellten Codekommentare. Unnötige und ungenaue Kommentare können die Vorschläge von GitHub Copilot negativ beeinflussen.

1. Öffnen Sie **console_app.py** in VSCode und wählen Sie die Methode **search_books** aus.

1. Öffnen Sie die Chatansicht, und geben Sie dann die folgende Eingabeaufforderung ein:

    ```plaintext
    @workspace Update selection to obtain a book title. Prompt the user to "Enter a book title to search for". Read the user input and ensure the book title isn't null.
    ```

1. Überprüfen Sie das vorgeschlagene Update.

    Die vorgeschlagene Aktualisierung sollte in etwa wie der folgende Codeschnipsel aussehen:

    ```python

    def search_books(self) -> ConsoleState:
        while True:
            book_title = input("Enter a book title to search for: ").strip()
            if not book_title:
                print("No input provided. Please enter a book title.")
            else:
                # Placeholder for future book search logic
                print(f"Searching for book titled: {book_title}")
                break
        return ConsoleState.PATRON_DETAILS

    ```

1. Zeigen Sie mit dem Mauszeiger auf den vorgeschlagenen Code, und wählen Sie dann **Auf „library\console\console_app.py“ anwenden** aus.

    Der vorgeschlagene Code sollte im Code-Editor mit Optionen zum **Beibehalten** oder **Rückgängigmachen** angezeigt werden.

1. Wählen Sie im Code-Editor die Option zum **Beibehalten**aus, um den vorgeschlagenen Code zu akzeptieren.

1. Wählen Sie die Methode **search_books** aus.

1. Fügen Sie die folgenden Dateien per Drag-and-Drop zum Chat-Kontext hinzu:

    - library/console/**console_app.py** (aktuelle Datei ausgewählt)
    - library/console/**main.py**
    - library/infrastructure/Json/**Books.json**
    - library/infrastructure/Json/**Loans.json**
    - library/infrastructure/Json/**BookItems.json**
    - library/infrastructure/**json_data.py**
    - library/infrastructure/**json_loan_repository.py**

1. Geben Sie den folgenden Prompt ein:

    ```plaintext
    @workspace provide a simple text overview plan of how to update the search_books method and ConsoleApps class to find a matching book title in the Books.json file. Use the user supplied book title to find a matching book. If a book is found, use Loans.json to check if the book is available for loan. If the book has been returned, display a message stating "book.title is available for loan". If the book is on loan, display a message stating "book.title is on loan to another patron. The return due date is loan.DueDate". Don't provide code yet. List the general change recommendations for each high level item as a numbered list of paragraphs.
    ```

1. Nehmen Sie sich einen Moment Zeit, um die vorgeschlagenen Aktualisierungen zu überprüfen.

    Die Antwort sollte die folgenden Informationen enthalten:

    ```plaintext

    1. Update the ConsoleApp class to access book data:  
    Add a reference to the book repository or the loaded books data from JsonData within the ConsoleApp class. This will allow the search_books method to access the list of all books and perform searches based on user input.
    
    2. Modify the search_books method to search for a book:  
    Update the search_books method to use the user-supplied book title to search for a matching book in the loaded books data (from Books.json). The search should be case-insensitive and match the title exactly or partially, depending on requirements.
    
    3. Check book availability using loan data:  
    Once a matching book is found, use the book's ID to find all related book items (copies) and then check the Loans.json data to determine if any copies are currently on loan (i.e., have a loan record with a null ReturnDate). If all copies are returned, the book is available for loan.
    
    4. Display book availability status to the user:  
    If at least one copy of the book is available (not currently on loan), display a message such as "book.title is available for loan." If all copies are on loan, display a message such as "book.title is on loan to another patron. The return due date is loan.DueDate," using the due date from the active loan.
    
    5. Handle no match or multiple matches:  
    If no book matches the search, display an appropriate message to the user. Optionally, if multiple books match, prompt the user to refine their search or select from a list.
    
    6. Keep user in the book search loop:  
    After displaying the result, allow the user to search for another book or return to the previous menu, maintaining a smooth user experience.

    ```

    > **HINWEIS**: Möglicherweise haben Sie Code-Updates in der GitHub Copilot-Antwort erhalten. 
    > Die Code-Updates werden im nächsten Schritt behandelt.

    Sie können auch den **Fragemodus** der Chat-Ansicht verwenden, um Code-Updates zu analysieren und dann den **Bearbeitungsmodus**, um die Code-Updates zu implementieren.

1. Überprüfen Sie Beispiel-Prompts (Sie werden später Prompts formulieren).

    ```plaintext

    Update the search_books method and ConsoleApp class so that when a user enters a book title, the app searches 
    Books.json for a matching title (case-insensitive, partial match allowed). If a match is found, check all 
    related BookItem records and their loan status in Loans.json. If any copy is not currently on loan (no active 
    loan or has a ReturnDate), display "book.title is available for loan". If all copies are on loan, display 
    "book.title is on loan to another patron. The return due date is loan.DueDate" (show the soonest due date). 
    Integrate this logic into the user flow and ensure clear user messaging.
    ```

    Sie können den Prompt anpassen, um bestimmte Anforderungen zu erfüllen, indem Sie Copilot bitten, Ihnen über das Copilot-Feedback einen Prompt zu generieren. Ein von Copilot generierter Beispiel-Prompt folgt zur Überprüfung:

    ```plaintext

    Update the ConsoleApp class and its search_books method to implement the following:
    
    1. Add access to the loaded books data (from JsonData or a book repository) in ConsoleApp.
    2. In search_books, use the user-supplied book title to search for a matching book in Books.json (case-insensitive, partial or exact match).
    3. If a book is found, use its ID to find all related book items (copies) and check Loans.json to see if any copies are currently on loan (ReturnDate is null).
    4. If at least one copy is available, display: "book.title is available for loan." If all are on loan, display: "book.title is on loan to another patron. The return due date is loan.DueDate."
    5. If no book matches, inform the user. If multiple books match, prompt for refinement or selection.
    6. After displaying the result, allow the user to search again or return to the previous menu.
        
    Please provide the complete implementation for this book search and availability feature.
    ```

### Implementieren der Methode „search_books“ mithilfe des Bearbeitungsmodus von Copilot Chat

1. Um in der Chat-Ansicht in den Bearbeitungsmodus zu wechseln, wählen Sie **Modus festlegen** und dann **Bearbeiten** aus.

    Wenn Sie aufgefordert werden, eine neue Sitzung zu starten, wählen Sie **Ja** aus.

1. Fügen Sie die folgenden Dateien im **Chat-Bearbeitungsmodus** per Drag-and-Drop zum Chat-Kontext hinzu:

    - library/console/**console_app.py**
    - library/console/**main.py**
    - library/infrastructure/**json_data.py**
    - library/infrastructure/Json/**Books.json**
    - library/infrastructure/Json/**Loans.json**
    - library/infrastructure/Json/**BookItems.json**

1. Wählen Sie die Methode **search_books** aus **console_app.py** aus.

1. Geben Sie den folgenden Prompt ein:

    ```plaintext

    @workspace Update the ConsoleApp class so it can access the loaded books data from JsonData or a book repository, and update main.py to instantiate ConsoleApp with the loaded JsonData instance by passing json_data=json_data. In the search_books method, prompt the user for a book title and search for a matching book in Books.json using a case-insensitive, partial or exact match. If a book is found, use its ID to find all related book items (copies) and check Loans.json to determine if any copies are currently on loan (ReturnDate is null). If at least one copy is available, display a message stating the book is available for loan; if all are on loan, display a message with the book title and the due date of the loan. If no book matches, inform the user, and if multiple books match, prompt for refinement or selection. After displaying the result, allow the user to search again or return to the previous menu.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die vorgeschlagenen Updates in der Datei „console_app.py“ zu überprüfen.

    Sie können **Zurück** und **Weiter** verwenden, um durch die vorgeschlagenen Code-Updates zu navigieren, oder Sie können manuell durch die Datei scrollen.

    **console_app.py**

    Code-Updates, die die **json_data**-Abhängigkeit zum **console_app**-Konstruktor hinzufügen, finden Sie am oberen Rand der Klasse „ConsoleApp“.

    ```python
    class ConsoleApp:
        def **init**(
            self,
            loan_service: ILoanService,
            patron_service: IPatronService,
            patron_repository: IPatronRepository,
            loan_repository: ILoanRepository,
            json_data=None,  # <-- Add json_data for direct access to books/items
            book_repository=None  # <-- Optionally allow a book repo
        ):
            self._current_state: ConsoleState = ConsoleState.PATRON_SEARCH
            self.matching_patrons = []
            self.selected_patron_details = None
            self.selected_loan_details = None
            self._patron_repository = patron_repository
            self._loan_repository = loan_repository
            self._loan_service = loan_service
            self._patron_service = patron_service
            self._json_data = json_data   # <-- store json_data
            self._book_repository = book_repository
    ```

    Der Code schließt die Methode `search_books` zum Implementieren von Funktionen im Stub-Code ab, um zu überprüfen, ob **json_data** verwendet werden soll, um ein Buch nach Titel zu finden, dessen BookItem abzurufen, nach einer aktiven Ausleihe zu suchen und die Verfügbarkeit oder den Ausleihstatus anzuzeigen, wie angefordert.

    ```python
        def search_books(self) -> ConsoleState:
        while True:
            book_title = input("Enter a book title to search for: ").strip()
            if not book_title:
                print("No book title provided. Please try again.")
                continue

            # Case-insensitive, partial or exact match
            books = self._json_data.books
            matches = [b for b in books if book_title.lower() in b.title.lower()]

            if not matches:
                print("No matching books found.")
                again = input("Search again? (y/n): ").strip().lower()
                if again == 'y':
                    continue
                else:
                    return ConsoleState.PATRON_DETAILS

            if len(matches) == 1:
                book = matches[0]
            else:
                print("\nMultiple books found:")
                for idx, b in enumerate(matches, 1):
                    print(f"{idx}) {b.title}")
                selection = input("Select a book by number or 'r' to refine search: ").strip().lower()
                if selection == 'r':
                    continue
                if not selection.isdigit() or not (1 <= int(selection) <= len(matches)):
                    print("Invalid selection.")
                    continue
                book = matches[int(selection) - 1]

            # Find all book items (copies) for this book
            book_items = [bi for bi in self._json_data.book_items if bi.book_id == book.id]
            if not book_items:
                print("No copies of this book are in the library.")
                again = input("Search again? (y/n): ").strip().lower()
                if again == 'y':
                    continue
                else:
                    return ConsoleState.PATRON_DETAILS

            # Find all loans for these book items
            loans = self._json_data.loans
            on_loan = []
            available = []
            for item in book_items:
                # Find latest loan for this item (if any)
                item_loans = [l for l in loans if l.book_item_id == item.id]
                if item_loans:
                    # Get the most recent loan (by LoanDate)
                    latest_loan = max(item_loans, key=lambda l: l.loan_date or l.due_date or l.return_date or 0)
                    if latest_loan.return_date is None:
                        on_loan.append(latest_loan)
                    else:
                        available.append(item)
                else:
                    available.append(item)

            if available:
                print(f"Book '{book.title}' is available for loan.")
            else:
                # All copies are on loan, show due dates
                due_dates = [l.due_date for l in on_loan if l.due_date]
                if due_dates:
                    next_due = min(due_dates)
                    print(f"All copies of '{book.title}' are currently on loan. Next due date: {next_due}")
                else:
                    print(f"All copies of '{book.title}' are currently on loan.")

            again = input("Search for another book? (y/n): ").strip().lower()
            if again == 'y':
                continue
            else:
                return ConsoleState.PATRON_DETAILS 
    ```

    **main.py**

    Geänderte Instanziierung von `ConsoleApp`, um es in `json_data` zu übergeben, damit die App auf die JSON-Datendateien zugreifen kann.

    ```python
    # ...existing code...
            app = ConsoleApp(
            loan_service=loan_service,
            patron_service=patron_service,
            patron_repository=patron_repo,
            loan_repository=loan_repo,
            json_data=json_data  # <-- Pass json_data so ConsoleApp can access books/items/loans
        )
    # ...existing code...
    
    ```

1. Wählen Sie in der Chat-Ansicht die Option zum **Beibehalten** aus, um alle Bearbeitungen beizubehalten.

    Überprüfen Sie immer GitHub Copilot-Vorschläge, bevor Sie Updates akzeptieren.

    Wenn Sie sich bei den vorgeschlagenen Updates nicht sicher sind, können Sie Änderungen annehmen und dann GitHub Copilot um eine Erläuterung bitten. Sie können die Bearbeitungen wiederherstellen, wenn Sie sich gegen die Updates entscheiden.

    > **HINWEIS:** Wenn GitHub Copilot die Formatierung des Rückgabedatums mithilfe eines bestimmten Gebietsschemas oder Formats vorschlägt, stellen Sie sicher, dass Sie die Methode „datetime.strftime()“ von Python verwenden, um das Datum nach Bedarf zu formatieren.

1. Stellen Sie sicher, dass Sie Updates sowohl in der Datei „console_app.py“ als auch in der Datei „main.py“ akzeptiert haben.

1. Öffnen Sie die EXPLORER-Ansicht in Visual Studio Code.

1. Führen Sie Ihre Tests aus, oder starten Sie die Anwendung, um sicherzustellen, dass keine Fehler durch die Code-Updates eingeführt wurden.

    Es werden zwar möglicherweise Warnmeldungen angezeigt, es sollten aber keine Fehler auftreten.

    Um die Tests auszuführen, öffnen Sie ein Terminal in Visual Studio Code, navigieren Sie zum Verzeichnis „AccelerateDevGHCopilot/library“ und führen Sie Folgendes aus:

    ```bash
    python -m unittest discover tests
    ```

## Mergen Ihrer Updates zur Buchverfügbarkeit in den Mainbranch des Repositorys

Es ist wichtig, den Code vor dem Mergen in den Hauptzweig des Repositorys zu testen. Durch Tests wird sichergestellt, dass Ihr Code erwartungsgemäß funktioniert und keine neuen Probleme mit sich bringt. In dieser Übung verwenden Sie manuelle Tests, um zu überprüfen, ob die Funktion zur Buchverfügbarkeit wie erwartet funktioniert.

In diesem Abschnitt der Übung werden folgende Aufgaben ausgeführt:

1. Testen Sie die Funktion „Buchverfügbarkeit“.
1. Synchronisieren Sie Ihre Änderungen mit dem Remoterepository.
1. Erstellen eines Pull Requests, um Ihre Änderungen im Mainbranch des Repositorys zu mergen

### Testen der Funktion „Buchverfügbarkeit“

Manuelle Tests können verwendet werden, um zu überprüfen, ob die neue Funktion wie erwartet funktioniert. Es ist wichtig, eine überprüfbare Datenquelle zu verwenden. In diesem Fall verwenden Sie die Dateien **Books.json** und **Loans.json**, um zu überprüfen, ob die neue Funktion den Verfügbarkeitsstatus eines Buches korrekt meldet.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Um die Anwendung auszuführen, öffnen Sie ein Terminal in Visual Studio Code, navigieren Sie zum Verzeichnis `AccelerateDevGHCopilot/library` und führen Sie Folgendes aus:

```bash
python console/main.py
```

1. Wenn Sie zur Eingabe eines Kundennamens aufgefordert werden, geben Sie **One** ein, und drücken Sie anschließend die EINGABETASTE.

    Daraufhin sollte eine Liste mit Kunden angezeigt werden, die der Suchabfrage entsprechen.

1. Geben Sie **2** beim Prompt „Eingabeoptionen“ ein (Auswahl „Patron 1“) ein und drücken Sie dann die Eingabetaste.

    - Durch Eingeben von **2** wird der zweite Kunde in der Liste ausgewählt.
    - Daraufhin sollten der Name und der Mitgliedschaftsstatus des Kunden angezeigt werden, gefolgt von Details zur Buchausleihe.

1. Um „Book One“ auszuwählen, das „Returned: False“ anzeigt, geben Sie Folgendes ein: **1**.

   - Beachten Sie, dass der Status **Returned: False** zurückgibt.
   - Oder suchen Sie eine Person mit einem Buch mit dem Status **„Returned: False“**. Notieren Sie sich den Namen des Buchs.

1. Um das Buch zurückzugeben, wählen Sie Folgendes aus: **r**

    - Beachten Sie, dass der Status auf Folgendes aktualisiert wird: **Returned: TRUE**

1. Schauen Sie sich die Bücher für „Patron One“ erneut an:

    - Um eine Person auszuwählen, wählen Sie Folgendes aus: **s**
    - Wiederholen Sie die Schritte **Suchen nach einem Patron:** für **Patron One**.
    - Um „Book One“ auszuwählen, das „Returned: True“ anzeigt, geben Sie Folgendes ein: **1**

    Beachten Sie, dass der Buchtitel angezeigt wird, es aber keine Verfügbarkeitsinformationen gibt.

1. Überprüfen Sie die Verfügbarkeit des Buchs und leihen Sie sich ein verfügbares Buch aus.

    - Um die Buchverfügbarkeit zu überprüfen, wählen Sie Folgendes aus: **b**
    - Suchen Sie nach einem verfügbaren Buch, geben Sie Folgendes ein: **One**

    Beachten Sie, dass der Buchtitel angezeigt wird sowie eine Meldung zur Verfügbarkeit, dass das Buch zur Ausleihe verfügbar ist. Beachten Sie auch, dass es keine Option zum Ausleihen von „Book One“ gibt.

1. Sie werden gefragt, ob Sie nach einem anderen Buch suchen möchten. Geben Sie **n** ein.

1. Beenden Sie die Anwendung, indem Sie „q“ eingeben, um den Vorgang zu beenden.

**Es gibt ein Problem mit der Anwendung**. Die Buchverfügbarkeit wird gemeldet, aber es gibt keine Option zum Ausleihen eines Buchs.

### Beheben des Fehlers beim Ausleihen von Büchern mit dem Agent-Modus

Copilot ist ein KI-Tool und wie Menschen kann es Fehler machen, daher müssen Sie die Ergebnisse überprüfen. Um diesen Fehler zu beheben, verwenden Sie den Agent-Modus.

1. Öffnen Sie Github Copilot Chat, und wählen Sie den **Agent-Modus** aus.
1. So fügen Sie den manuellen Test vom Terminal zum Chat hinzu:

    - Wählen Sie im Chatfenster im Copilot-Chat **Kontext hinzufügen** aus (stellen Sie sicher, dass Sie sich im Agent-Modus befinden)
    - Geben Sie „Tools“ ein und dann „Tools“ und wählen Sie mit der Maus oder mit der Eingabetaste aus.
    - Geben Sie „terminalSelection“ ein, und wählen Sie „**terminalLastCommand** den letzten Ausführungsbefehl des Terminals“ aus.

1. Fügen Sie Dateien zu Chat-Inhalten hinzu, indem Sie die im Editor in VSCode aufgeführten Dateien öffnen. Wählen Sie dann im Copilot-Chatfenster **Kontext hinzufügen** und dann **Editoren öffnen** aus:

    - **console_app.py** (enthält die Logik der Hauptanwendung und Benutzerinteraktion)
    - **loan_service.py** (Logik für Ausleihen)
    - **json_data.py** (übernimmt das Laden/Speichern von Büchern, Buchartikeln, Kundschaften, Autorinnen und Autoren, Ausleihen)
    - **json_loan_repository.py** (behandelt das Abrufen, Hinzufügen und Aktualisieren von Datensätzen zu Ausleihen)
    - **Books.json** (Beispielbuchdaten)
    - **BookItems.json** (Beispiele für Buchelemente/kopierte Daten)
    - **Patrons.json** (Beispielkundendaten)
    - **Loans.json** (Beispieldaten zu Ausleihen)
    - **Authors.json** (Beispielautorendaten)

1. Überprüfen Sie den Prompt und geben Sie ihn ein, um den Fehler zu beheben (stellen Sie sicher, dass Copilot Chat **Agent** anzeigt):

    ```plaintext
    @workspace My goal is to make it possible for a patron to check out an available book directly from the console app menu. Right now, when I search for a book and it is available, the app only tells me "...is available for loan" but doesn’t let me check it out. Please help me update the code so that when a book is available, the app prompts me to check it out, and if I choose yes, it creates a new loan for the current patron and book. Make sure the checkout works smoothly in the menu flow. For the loan_service add checkout functionality and ensure the console app calls this method. Only use the existing enum and menu option names as defined in the codebase. Only use enum values and menu option names that are already defined in the codebase. Do not invent, rename, or add new enum values or menu options.
    ```

    Beachten Sie, dass der Agent bestimmte Zeilen mehrerer Dateien liest. Er führt Updates durch, überprüft sie und führt weitere Updates durch.

1. Überprüfen Sie die Updates des Agent-Modus in **console-app.py** am Ende der Methode `search_books`, die dem folgenden Code ähneln sollten:

    ```python
    def search_books(self) -> ConsoleState:
    # ...existing code...

           if available:
                print(f"Book '{book.title}' is available for loan.")
                # Prompt to check out
                checkout = input("Would you like to check out this book? (y/n): ").strip().lower()
                if checkout == 'y':
                    if not self.selected_patron_details:
                        print("No patron selected. Please select a patron first.")
                        return ConsoleState.PATRON_SEARCH
                    # Use the first available copy
                    book_item = available[0]
                    # Create a new loan using the loan service
                    status = self._loan_service.create_loan(
                        patron_id=self.selected_patron_details.id,
                        book_item_id=book_item.id
                    )
                    print(status)
                    # Reload loans to reflect the new loan
                    if hasattr(self._json_data, 'load_data'):
                        self._json_data.load_data()
                    print(f"Book '{book.title}' checked out to {self.selected_patron_details.name}.")
                    return ConsoleState.PATRON_DETAILS
        # ...existing code...
    ```

1. Überprüfen Sie die Updates für **loan_service.create_loan**.

```python
    def create_loan(self, patron_id: int, book_item_id: int):
        """Create a new loan for the given patron and book item, and add it to the repository."""
        from ..entities.loan import Loan
        from datetime import datetime, timedelta
        # Check if the book item is already on loan
        all_loans = getattr(self._loan_repository, 'get_all_loans', lambda: [])()
        for loan in all_loans:
            if loan.book_item_id == book_item_id and loan.return_date is None:
                return "This copy is already on loan."
        # Generate a new loan ID
        max_id = max((l.id for l in all_loans if hasattr(l, 'id')), default=0)
        new_id = max_id + 1
        now = datetime.now()
        due = now + timedelta(days=14)
        new_loan = Loan(
            id=new_id,
            book_item_id=book_item_id,
            patron_id=patron_id,
            loan_date=now,
            due_date=due,
            return_date=None
        )
        self._loan_repository.add_loan(new_loan)
        return f"Loan created. Due date: {due.date()}"

```

1. Beachten Sie die Updates von „ConsoleApp.search_books“ und „LoanService.“:

    Die Methoden „search_books“ und „loan_service“ werden nun aktualisiert, sodass die App die Person auffordert, ein Buch auszuleihen sobald es verfügbar ist. Wenn die Person „zustimmt, wird eine neue Ausleihe für die aktuellen Kundschaft und das ausgewählte Buchelement erstellt, und der Menüfluss kehrt zu den Details der Kundschaft zurück. Der Ausleihvorgang ist nun reibungslos in den Menüfluss integriert.

1. Akzeptieren Sie die Änderungen.

1. Testen Sie die vorherigen Testschritte erneut, und **führen Sie einen Ausleihvorgang für Buch aus**, um sicherzustellen, dass die Fehlerbehebung funktioniert. Wenn Probleme weiterhin bestehen, fahren Sie mit der Problembehandlung mit dem Agent- oder Fragemodus fort.

### Synchronisieren Ihrer Änderungen mit dem Remoterepository

1. Wählen Sie die Ansicht „Quellcodeverwaltung“ aus.

1. Stellen Sie sicher, dass die aktualisierten Dateien unter **Änderungen** aufgeführt sind.

    Die unter **Änderungen** aufgeführten Dateien „common_actions.py“ und „console_app.py“ sollten angezeigt werden. Die Datei „main.py“ kann auch aufgeführt werden.

1. Verwenden Sie GitHub Copilot, um eine Nachricht für den **Commit** zu generieren.

    ![Screenshot der Schaltfläche zum Generieren der Commit-Meldung mit Copilot.](./Media/m03-github-copilot-commit-message-python.png)

1. Wählen Sie **Committen** und anschließend **Ja** aus, um Ihre Änderungen zu stagen und zu committen.

1. Um Änderungen am Remoterepository zu synchronisieren, wählen Sie **Änderungen synchronisieren** aus.

### Erstellen eines Pull Requests, um Ihre Änderungen im Mainbranch zu mergen

Sie haben die neue Funktion implementiert, die es Bibliothekarinnen und Bibliothekaren ermöglicht, den Verfügbarkeitsstatus eines Buchs zu ermitteln. Nun müssen Sie Ihre Änderungen im Mainbranch des Repositorys mergen. Sie können einen Pull Request erstellen, um Ihre Änderungen im Mainbranch zu mergen.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie Ihr GitHub-Repository in einem Webbrowser.

    So öffnen Sie Ihr GitHub-Repository aus Visual Studio Code:

    1. Wählen Sie in der unteren linken Ecke von Visual Studio Code **book-availability** aus.
    1. Wählen Sie im Kontextmenü rechts neben dem Branch **book-availability** das Symbol **In GitHub öffnen** aus.

1. Wählen Sie auf der Seite des GitHub-Repositorys die Registerkarte **Vergleichs- und Pull Request** aus.

1. Stellen Sie sicher, dass **Base** **main** angibt, **compare** **book-availability** angibt und **Able to merge** aktiviert ist.

1. Wählen Sie unter **Beschreibung hinzufügen** die Schaltfläche „Copilot-Aktionen“ (das GitHub Copilot-Symbol) und dann die Option zum Generieren einer Zusammenfassung aus.

    > **HINWEIS:** Der GitHub Copilot Free-Plan unterstützt derzeit die Funktion der Zusammenfassung des Pull Request nicht.

    Wenn Sie den GitHub Copilot Free-Plan verwenden, können Sie Ihre eigene Zusammenfassung schreiben oder die nachstehende Zusammenfassung verwenden, um den Pull Request abzuschließen.

    ```plaintext

    This pull request introduces a new feature to the library console application: the ability to search for books and check their availability. It also includes updates to dependency injection and the CommonActions enumeration to support this functionality. Below are the most important changes grouped by theme.

    New Feature: Book Search

    Added a new SEARCH_BOOKS action to the CommonActions enumeration (library\console\common_actions.py).

    Updated PatronDetails method to handle the SEARCH_BOOKS action, including a new SEARCH_BOOKS method that allows users to search for a book by title and check its availability (library\console\console_app.py).

    Modified ReadInputOptions and WriteInputOptions methods to include the new SEARCH_BOOKS option (library/console/console_app.py).

    Dependency Injection Updates

    Added JsonData as a dependency in the ConsoleApp constructor and ensured it is registered in the DI container before ConsoleApp (library/console/console_app.py, library/console/main.py).

    ```

1. Nachdem die Zusammenfassung generiert wurde, wählen Sie **Vorschau** aus.

1. Nehmen Sie sich einen Moment Zeit, um die Zusammenfassung zu überprüfen.

    Die von GitHub Copilot generierte Zusammenfassung des Pull Request sollte dem folgenden Beispiel ähneln:

    ![Screenshot: Pull Request-Zusammenfassung, die mit einem GitHub Copilot Enterprise-Konto generiert wurde](./Media/m03-github-copilot-pull-request-summary.png)

1. Klicken Sie auf **Pull Request erstellen**.

1. Wenn alle Prüfungen ohne Konflikte mit dem Basis-Branch beendet wurden, wählen Sie **Pull Request mergen** und wählen dann **Merge bestätigen** aus.

    Beachten Sie, dass Sie den Branch **book-availability** löschen können, nachdem Sie die Änderungen zusammengeführt haben. Zum Löschen des Branches wählen Sie **Branch löschen** aus.

1. Wechseln Sie zurück zum Visual Studio Code-Fenster.

1. Wechseln Sie zum **Hauptzweig** des Repositorys.

1. Öffnen Sie die Ansicht „Quellcodeverwaltung“ und **ziehen** Sie dann die Änderungen aus dem Remoterepository.

1. Stellen Sie sicher, dass die Buchverfügbarkeitsfunktion im **Mainbranch** verfügbar ist.

## Zusammenfassung

In dieser Übung haben Sie gelernt, wie Sie GitHub Copilot verwenden, um ein neues Codefeature für eine Python-Anwendung zu entwickeln. Sie haben das Feature in einem neuen Branch mit der Inline-Chat- und der Chat-Ansicht von GitHub Copilot entwickelt, Ihren Code getestet und dann Ihre Änderungen in den Mainbranch des Repositorys gemergt. Sie haben außerdem GitHub Copilot verwendet, um eine Commit-Nachricht und eine Zusammenfassung des Pull Requests zu generieren.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich eine Minute Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder GitHub Copilot-Abonnement vorgenommen haben, die Sie nicht beibehalten möchten. Wenn Sie Änderungen vorgenommen haben, können Sie sie jetzt rückgängig machen.
