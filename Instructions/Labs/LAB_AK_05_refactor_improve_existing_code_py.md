---
lab:
  title: Übung – Umgestalten von vorhandenem Code mithilfe von GitHub Copilot (Python)
  description: 'Erfahren Sie, wie Sie vorhandene Codeabschnitte mithilfe von GitHub Copilot in Visual Studio Code umgestalten und verbessern.'
---

# Umgestalten von vorhandenem Code mithilfe von GitHub Copilot

Mit GitHub Copilot können Sie Ihre gesamte Codebasis auswerten und Aktualisierungen vorschlagen, die Ihnen bei der Umgestaltung und Verbesserung Ihres Codes helfen. In dieser Übung verwenden Sie GitHub Copilot, um bestimmte Abschnitte einer Python-Anwendung umzugestalten, während Sie Verbesserungen an Codequalität, Zuverlässigkeit, Leistung und Sicherheit vornehmen.

Diese Übung dauert ca. **30** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, benötigen Sie ein eigenes GitHub-Konto und ein GitHub Copilot-Abonnement. Falls Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses Einzelkonto <a href="https://go.microsoft.com/fwlink/?linkid=2320148" target="_blank">registrieren</a> und den GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement in Ihrer Labumgebung haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement für diese Übung verwenden.

## Vor der Installation

Ihre Übungsumgebung muss die folgenden Voraussetzungen erfüllen: Git 2.48 oder höher, Python 3.10 oder höher, Visual Studio Code mit dem Python-Erweiterungsformular Microsoft und Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

Wenn Sie einen lokalen PC als Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Wenn Sie Hilfe beim Konfigurieren Ihres lokalen PCs als Labumgebung benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://microsoftlearning.github.io/mslearn-github-copilot-dev/Instructions/Labs/LAB_AK_00_configure_lab_environment_py.html" target="_blank">Konfigurieren Ihrer Labumgebungsressourcen</a>.

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

Wenn Sie eine gehostete Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, fügen Sie die folgende URL in die Navigationsleiste eines Browsers ein: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

- Öffnen Sie die Eingabeaufforderung, und führen Sie die folgenden Befehle aus:

    Um sicherzustellen, dass Visual Studio Code für die Verwendung der richtigen Version von Python konfiguriert ist, stellen Sie sicher, dass die Python-Version 3.10 oder höher installiert ist:

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

Sie sind Entwicklerin bzw. Entwickler und arbeiten in der IT-Abteilung Ihrer lokalen Community. Die Back-End-Systeme, die die öffentliche Bibliothek unterstützen, wurden bei einem Brand zerstört. Ihr Team muss ein temporäres Projekt entwickeln, damit die Mitarbeitenden der Bibliothek ihre Vorgänge verwalten können, bis das System ersetzt werden kann. Ihr Team hat GitHub Copilot ausgewählt, um den Entwicklungsprozess zu beschleunigen.

Sie haben eine erste Version der Bibliotheksanwendung zur Überprüfung abgegeben. Das Überprüfungsteam hat Möglichkeiten zur Verbesserung der Codequalität, Leistung, Lesbarkeit, Wartung und Sicherheit identifiziert.

Diese Übung umfasst die folgenden Aufgaben:

1. Einrichten der Bibliotheksanwendung in Visual Studio Code
1. Analysieren Sie Code in der Chatansicht und gestalten Sie ihn in den Modi „Fragen“ und „Bearbeiten“ um.
1. Gestalten Sie Code mithilfe von Inlinechat und der Chatansicht in den Modi „Bearbeiten“ und „Agent“ um.

## Einrichten der Bibliotheksanwendung in Visual Studio Code

Sie müssen die vorhandene Anwendung herunterladen, die Codedateien extrahieren und dann das Projekt in Visual Studio Code öffnen.

Gehen Sie folgendermaßen vor, um die Bibliotheksanwendung einzurichten:

1. Öffnen Sie ein Browserfenster in Ihrer Labumgebung.

1. Um eine ZIP-Datei mit der Bibliotheksanwendung herunterzuladen, fügen Sie die folgende URL in die Adressleiste Ihres Browsers ein: [GitHub Copilot-Übung – Umgestalten von vorhandenem Code](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM5Python.zip)

    Die ZIP-Datei heißt **AZ2007LabAppM5Python.zip**.

1. Extrahieren Sie die Dateien aus der Datei **AZ2007LabAppM5Python.zip**.

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner mit Downloads in Ihrer Labumgebung.

    1. Klicken Sie mit der rechten Maustaste auf **AZ2007LabAppM5Python.zip**, und wählen Sie dann **Alle extrahieren** aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Öffnen Sie den Ordner mit den extrahierten Dateien und kopieren Sie dann den Ordner **AccelerateDevGHCopilot** an einen Speicherort, auf den Sie einfach zugreifen können, z. B. Ihren Windows-Desktop-Ordner.

1. Öffnen Sie den Ordner **AccelerateDevGHCopilot** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Labumgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows-Desktop-Ordner, und wählen Sie **AccelerateDevGHCopilot** und dann **Ordner auswählen** aus.

1. Überprüfen Sie in der EXPLORER-Ansicht von Visual Studio Code die folgende Projektstruktur:

    - AccelerateDevGHCopilot/library   ├── application_core   ├── console   ├── infrastructure   └── tests   └── readme.md

1. Stellen Sie sicher, dass der ursprüngliche Code in den Tests im nächsten Abschnitt erfolgreich ausgeführt wird. Führen Sie optional die Anwendung aus, wenn Sie mit den vorherigen Labs aus dem Ordner **\library** im Terminal unter Verwendung von **`python console\main.py`** vertraut sind.

### pytest aktivieren

Im Vergleich zu Unittest bietet pytest einige Vorteile wie präzise Syntax, Features wie Fixtures und Parametrisierung sowie eine bessere Fehlerberichterstattung. pytest erleichtert das Schreiben und Warten von Tests und führt zudem Unittest-Testfälle aus.

1. Bei Bedarf wird pytest aus der Installation der <a href="https://marketplace.visualstudio.com/items?itemName=ms-python.python" target="_blank">Microsoft Python-Erweiterung von Visual Studio</a> aktiviert.

1. Wählen Sie das Flasksymbol  ![Screenshot des Test-Flasksymbols.](./Media/m04-pytest-flask-py.png) in der Symbolleiste aus, sobald Tests ermittelt wurden. Wenn das Symbol nicht vorhanden ist, lesen Sie die vorherigen Anweisungen.

1. Wählen Sie „Python-Tests konfigurieren“ oder falls zuvor konfiguriert:

1. Wenn die Tests nicht konfiguriert wurden oder das richtige Projekt getestet wird, fahren Sie mit dem nächsten Schritt fort. Wenn Sie das Testprojekt ändern müssen, fahren Sie mit folgenden Aktionen fort:
    - `Ctrl+Shift+P` zum Öffnen der Befehlspalette.
    - Geben Sie **„Python: Tests konfigurieren“** ein.
    - Wählen Sie „pytest“ aus.
    - Wählen Sie das Verzeichnis für Ihren Python-Code aus.
    - Wählen Sie das Wiedergabesymbol aus, um Tests auszuführen.

1. Wählen Sie „pytest“ aus den Optionen aus.

1. Wählen Sie den Ordner (`library\`) aus, der Ihren Testcode enthält.

1. Wählen Sie das Wiedergabesymbol aus, um Tests auszuführen.
    ![Screenshot mit den pytest-Ergebnissen](./Media/m04-pytest-configure-results-py.png)

1. Führen Sie optional den ptytest-Befehl vom `library`-Pfad im Terminal aus:

    ```plaintext
    pytest -v
    ```

## Analysieren von Code in der Chat-Ansicht und Umgestaltung in den Modi „Fragen“ und „Bearbeiten“

Reflexion ist ein leistungsfähiges Feature, mit dem Sie Objekte während der Runtime untersuchen und bearbeiten können. Reflexion kann jedoch langsam sein, und es gibt dabei potenzielle Sicherheitsrisiken, die berücksichtigt werden sollten.

Sie müssen folgende Schritte durchführen:

1. Analysieren Sie Ihren Arbeitsbereich und untersuchen Sie, wie Sie Ihre zugewiesene Aufgabe angehen sollten.
1. Gestalten Sie die Verwendung von Python Enum in eine enum_helper-Klasse um, um statische Wörterbücher anstelle von Reflexion und Pythons zu verwenden, die in Enum integriert sind.

### Analysieren der Enumerationsverwendung mit der Chatansicht im Fragemodus

Die Chatansicht von GitHub Copilot verfügt über drei Modi: **Fragen**, **Bearbeiten** und **Agent**. Jeder Modus wurde für verschiedene Arten von Interaktionen mit GitHub Copilot entwickelt.

- **Fragen**: Verwenden Sie diesen Modus, um GitHub Copilot Fragen zu Ihrer Codebasis zu stellen. Sie können GitHub Copilot auffordern, Code zu erklären, Änderungen vorzuschlagen oder Informationen zur Codebasis bereitzustellen.
- **Bearbeiten**: Verwenden Sie diesen Modus, um ausgewählte Codedateien zu bearbeiten. Sie können GitHub Copilot verwenden, um Code umzugestalten, Kommentare hinzuzufügen oder andere Änderungen an Ihrem Code vorzunehmen.
- **Agent**: Verwenden Sie diesen Modus, um GitHub Copilot als Agent auszuführen. Sie können GitHub Copilot verwenden, um Befehle auszuführen, Code auszuführen oder andere Aufgaben in Ihrem Arbeitsbereich auszuführen.

In diesem Abschnitt der Übung verwenden Sie die Chatansicht im Modus **Fragen**, um Ihre Programmieraufgabe zu analysieren.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Erweitern Sie in der EXPLORER-Ansicht den Ordner **Bibliothek**.

1. Öffnen Sie die Chatansicht von GitHub Copilot.

    Die Chatansicht bietet eine verwaltete Chatoberfläche zur Interaktion mit GitHub Copilot.

    Sie können die Chatansicht über die Schaltfläche **Chat umschalten** ein- und ausblenden. Diese befindet sich oben im Visual-Studio-Code-Fenster, rechts neben dem Suchtextfeld.

    ![Screenshot der Copilot-Schaltfläche „Chat umschalten“](./Media/m01-github-copilot-toggle-chat.png)

    Sie können auch die Tastenkombination **Strg+Alt+I** verwenden, um die Chatansicht umzuschalten.

1. Beachten Sie, dass die Chatansicht standardmäßig im Modus **Fragen** geöffnet wird.

    Der aktuelle Chatmodus wird in der unteren rechten Ecke der Chatansicht angezeigt. Chatantworten werden in der Chatansicht angezeigt, wenn Sie im Modus **Fragen** arbeiten.

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext
    @workspace Provide an explanation of how the current Python code can be improved with code refactoring to:
    - avoid reflection
    - avoid repeated `if/elif`
    - make the code more explicit and efficient.
    Then provide suggestion for refactoring this Python project to implement the improvement suggestions.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die Antwort zu überprüfen, z. B. diese, mit entfernten Codeempfehlungen:

    >**HINWEIS** Es ist normal, dass die Antworten sehr unterschiedlich ausfallen, aber es sollten ähnliche Themen auftauchen.

    -----

    >### Erläuterung zur Codeverbesserung
    >
    > Zur Verbesserung des aktuellen Codes gibt es folgende Umgestaltungsstrategien:
    >
    > 1. **Reflexion vermeiden**:  
    >    Reflexion kann langsam und fehleranfällig sein. Verwenden Sie stattdessen explizite Methodenaufrufe, Schnittstellen oder Wörterbücher, um Funktionen Aktionen zuzuordnen. Dadurch wird der Code wartungsfreundlicher und leistungsfähiger.
    >
    > 2. **Wiederholte `if/elif`-Ketten vermeiden**:  
    >    Lange `if/elif`-Ketten sind schwer zu lesen und zu warten. Ersetzen Sie sie durch ein Wörterbuch (in Python) oder einen Switchausdruck (in C# 8+), oder verwenden Sie Polymorphismus (objektorientiertes Design), um das Verhalten zu delegieren.
    >
    > 3. **Code expliziter und effizienter gestalten**:  
    >    Expliziter Code ist einfacher zu verstehen und zu debuggen. Verwenden Sie klare Variablennamen, vermeiden Sie magische Zeichenfolgen/Zahlen und Strukturlogik, damit ihre Absicht klar erkennbar ist. Die Effizienz kann häufig verbessert werden, indem unnötige Prüfungen oder Lookups reduziert werden.
    >
    >#### Umgestaltungsempfehlungen
    >
    > Angenommen Sie hätten folgenden Code (Python-Beispiel):
    >
    > ```python
    > # ...existing code...
    > def handle_action(action, data):
    >     if action == "create":
    >         return create_item(data)
    >     elif action == "update":
    >         return update_item(data)
    >     elif action == "delete":
    >         return delete_item(data)
    >     else:
    >         raise ValueError("Unknown action")
    > # ...existing code...
    > ```
    >
    > **Umgestaltete Version (verhindert Reflexion und if/elif, expliziter)**
    >
    > ```python
    > # ...existing code...
    > def handle_action(action, data):
    >     action_map = {
    >         "create": create_item,
    >         "update": update_item,
    >         "delete": delete_item,
    >     }
    >     try:
    >         return action_map[action](data)
    >     except KeyError:
    >         raise ValueError(f"Unknown action: {action}")
    > # ...existing code...
    > ```
    >
    > **Vorteile:**
    >
    > - Es wird keine Reflexion verwendet.
    > - `if/elif` nicht wiederholt.
    > - Die Zuordnung ist explizit und einfach zu erweitern.
    > - Effizienter durch direkte Funktionssuche.
    >
    >### Zusammenfassung
    >
    > - Verwenden Sie Wörterbücher oder Schalterausdrücke anstelle von Reflexion oder langen `if/elif`-Ketten.
    > - Machen Sie Zuordnungen explizit für Wartbarkeit und Effizienz.
    > - Verwenden Sie für unbekannte Fälle klare Vorgaben zur Fehlerbehandlung.
    >
    > Durch diese Änderungen ist Ihre Codebasis einfacher zu verwalten, effizienter und weniger fehleranfällig.

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext
    @workspace which Python files in this workspace use reflection or long `if/elif` chains?
    ```

    Die Antwort sollte **console/console_app.py**  (`getattr`) beinhalten und dass **console/console_app.py** auch lange `if/elif`-Ketten für die Befehls- und Eingabebehandlung verwendet.

1. Fügen Sie die Datei **console/console_app.py** zum Chatkontext hinzu:

    Sie können die Dateien aus der Explorer-Ansicht von Visual Studio Code per Drag-and-Drop in die Chatansicht ziehen. Sie können auch die Schaltfläche **Kontext hinzufügen** in der Chatansicht verwenden, um Dateien und andere Ressourcen hinzuzufügen.

    > **HINWEIS:** Durch das Hinzufügen von Dateien zum Chatkontext wird sichergestellt, dass GitHub Copilot diese Dateien beim Generieren einer Antwort berücksichtigt. Die Relevanz und die Genauigkeit der Antworten erhöhen sich, wenn GitHub Copilot den Kontext Ihrer Prompts versteht.

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext

    @workspace I need to refactor the `library\console\console_app.py` Python file to: Use dictionaries or switch expressions instead of reflection or long `if/elif` chains; Make mappings explicit for maintainability and efficiency; Use clear error handling for unknown cases; Provide refactored code to apply.

    ```

    Beim Schreiben von Prompts sind Klarheit und Kontext wichtig. Mithilfe von Chatteilnehmern, Schrägstrich-Befehlen und Chatvariablen können Sie den Kontext so definieren, dass GitHub Copilot ihn versteht.

    Bei einem Prompt, der GitHub Copilot auffordert, ein Problem zu lösen, beginnen Sie mit dem Problem, das Sie lösen möchten. Verwenden Sie prägnante Sätze, um Details zu beschreiben, Einschränkungen festzulegen und Ressourcen zu identifizieren. Stellen Sie abschließend sicher, dass Sie GitHub Copilot mitteilen, was in die Antwort eingeschlossen werden soll.

    In diesem Fall beginnt Ihr Prompt mit einer Beschreibung Ihres Problems/Ziels. Sie teilen GitHub Copilot mit, dass Sie die Datei `library\console\console_app.py` wie folgt umgestalten müssen:

    - Verwenden Sie Wörterbücher oder Schalterausdrücke anstelle von Reflexion oder langen `if/elif`-Ketten.
    - Machen Sie Zuordnungen explizit für Wartbarkeit und Effizienz.
    - Verwenden Sie für unbekannte Fälle klare Vorgaben zur Fehlerbehandlung.

    Um den Prompt zu verbessern, geben Sie die Anweisung zum Bereitstellen von umgestaltetem Code an, der angewendet werden soll.

1. Nehmen Sie sich kurz Zeit, um die von GitHub Copilot generierte Antwort zu überprüfen. Sie wenden die Bearbeitungen in diesem Schritt **nicht** an.

    > ### Erläuterung zur Codeverbesserung
    >
    > Zur Verbesserung des aktuellen Codes gibt es folgende Umgestaltungsstrategien:
    >
    > 1. **Reflexion vermeiden**:  
    >    Reflexion kann langsam und fehleranfällig sein. Verwenden Sie stattdessen explizite Methodenaufrufe, Schnittstellen oder Wörterbücher, um Funktionen Aktionen zuzuordnen. Dadurch wird der Code wartungsfreundlicher und leistungsfähiger.
    >
    > 2. **Wiederholte `if/elseif`-Ketten vermeiden**:  
    >    Lange `if/elseif`-Ketten sind schwer zu lesen und zu warten. Ersetzen Sie sie durch ein Wörterbuch (in Python) oder einen Switchausdruck (in C# 8+), oder verwenden Sie Polymorphismus (objektorientiertes Design), um das Verhalten zu delegieren.
    >
    > 3. **Code expliziter und effizienter gestalten**:  
    >    Expliziter Code ist einfacher zu verstehen und zu debuggen. Verwenden Sie klare Variablennamen, vermeiden Sie magische Zeichenfolgen/Zahlen und Strukturlogik, damit ihre Absicht klar erkennbar ist. Die Effizienz kann häufig verbessert werden, indem unnötige Prüfungen oder Lookups reduziert werden.
    >
    >
    > ### Umgestaltungsempfehlungen
    >
    > Angenommen Sie hätten folgenden Code (Python-Beispiel):
    >
    > ```python
    > # ...existing code...
    >    def _handle_patron_details_selection(self, selection, patron, valid_loans):
    >        if selection == 'q':
    >            return ConsoleState.QUIT
    >        elif selection == 's':
    >            return ConsoleState.PATRON_SEARCH
    >        elif selection == 'm':
    >            status = self._patron_service.renew_membership(patron.id)
    >            print(status)
    >            self.selected_patron_details = self._patron_repository.get_patron(patron.id)
    >            return ConsoleState.PATRON_DETAILS
    > # ...existing code...
    > ```
    >
    > #### Umgestaltete Version (verhindert Reflexion und if/elif, expliziter)
    >
    > ```python
    > # ...existing code...
    >    def _handle_patron_details_selection(self, selection, patron, valid_loans):
    >        def renew_membership():
    >           status = self._patron_service.renew_membership(patron.id)
    >           print(status)
    >           self.selected_patron_details = self._patron_repository.get_patron(patron.id)
    >           return ConsoleState.PATRON_DETAILS
    > # ...existing code...
    > ```
    >
    > **Vorteile:**
    >
    > - Es wird keine Reflexion verwendet.
    > - `if/elif` nicht wiederholt.
    > - Die Zuordnung ist explizit und einfach zu erweitern.
    > - Effizienter durch direkte Funktionssuche.
    >
    >
    > ### Zusammenfassung
    >
    > - Verwenden Sie Wörterbücher oder Schalterausdrücke anstelle von Reflexion oder langen `if/elseif`-Ketten.
    > - Machen Sie Zuordnungen explizit für Wartbarkeit und Effizienz.
    > - Verwenden Sie für unbekannte Fälle klare Vorgaben zur Fehlerbehandlung.
    >
    > Durch diese Änderungen ist Ihre Codebasis einfacher zu verwalten, effizienter und weniger fehleranfällig.

1. Zeigen Sie mit dem Mauszeiger in der Chatansicht auf das Codebeispiel, das in der Antwort enthalten ist.

1. Beachten Sie die drei Schaltflächen, die in der oberen rechten Ecke des Codeausschnitts angezeigt werden.

1. Zeigen Sie mit dem Mauszeiger auf die einzelnen Schaltflächen, um eine QuickInfo anzuzeigen, die die Aktion beschreibt.

    Die ersten beiden Schaltflächen kopieren Code in den Editor. Die dritte Schaltfläche kopiert Code in die Zwischenablage. Sie wenden die Bearbeitungen in diesem Schritt **nicht** an.

> **HINWEIS:** Sie könnten den Modus „Fragen“ verwenden, um den Code zu aktualisieren. Der Modus „Bearbeiten“ gestaltet Ihren Code jedoch direkt im Code-Editor um und bietet weitere Optionen zum Akzeptieren von Aktualisierungen.

### Umgestalten der Klasse ConsoleApp (console/console_app.py) mithilfe der Chatansicht im Bearbeitungsmodus

Der Modus „Bearbeiten“ der Chatansicht wurde für die Bearbeitung von Code in Ihrem Arbeitsbereich entwickelt. Sie können den Modus „Bearbeiten“ verwenden, um Code umzugestalten, Kommentare hinzuzufügen oder andere Änderungen an Ihrem Code vorzunehmen.

1. Wählen Sie in der Chatansicht **Modus festlegen** und dann **Bearbeiten** aus.

    Wenn Sie gefragt werden, ob Sie eine neue Sitzung im Modus „Bearbeiten“ starten möchten, wählen Sie **Ja** aus.

    Im Modus **Bearbeiten** zeigt GitHub Copilot Antworten als Empfehlungen zum Aktualisieren des Codes im Code-Editor an. Der Modus „Bearbeiten“ wird in der Regel verwendet, wenn ein neues Feature implementiert, ein Fehler behoben oder Code umgestaltet wird.

1. Fügen Sie die Datei „console/console_app.py“ zum Chatkontext hinzu:

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext

    @codebase I need to refactor the ConsoleApp class. Use static dictionaries to supply enum description attributes. Use dictionaries or switch expressions instead of reflection or long `if/elif` chains. Make mappings explicit for maintainability and efficiency. Use clear error handling for unknown cases.

    ```

    Die Antwort des Agents im Bearbeitungsmodus sollte Aktualisierungen in der `ConsoleApp`-Klasse vorschlagen und eine ähnliche Antwort wie folgende ausgeben:

    ```plaintext
    The ConsoleApp class has been refactored to use static dictionaries for enum descriptions, explicit dictionaries for state and input handling, and clear error handling for unknown cases, improving maintainability and efficiency.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die vorgeschlagenen Codeaktualisierungen in der Datei **console_app.py** zu überprüfen. In den Ergebnissen sollte Folgendes erfolgt sein:

    - Statische Wörterbücher für Enumerationsbeschreibungen (`CONSOLE_STATE_DESCRIPTIONS` und `COMMON_ACTIONS_DESCRIPTIONS`) zum Ersetzen von Reflexion und langen `if/elif`-Ketten eingefügt.
    - `write_input_options` umgestaltet, um das statische Wörterbuch zum Anzeigen von Eingabeoptionen zu verwenden.
    - Hauptzustandsschleife in `run` durch eine wörterbuchbasierte Handlersuche für Wartbarkeit und mehr Effizienz ersetzt.
    - Explizite Fehlerbehandlung für unbekannte Zustände und nächste Zustände hinzugefügt.
    - Alle Aktionszuordnungen in Eingabehandlern sind jetzt explizite Wörterbücher für mehr Übersichtlichkeit und bessere Wartbarkeit.

1. Wählen Sie in der Chatansicht die Option **Beibehalten** aus, um alle Aktualisierungen zu akzeptieren.

    Sie können auch die Symbolleiste „Chatbearbeitungen“ am unteren Rand der Registerkarte „Code-Editor“ verwenden, um Codeaktualisierungen anzunehmen oder abzulehnen.

1. Nehmen Sie sich einen Moment Zeit, um sich die aktualisierte **run**-Methode genauer anzusehen.

    GitHub Copilot sollte die **run**-Methode aktualisiert haben, um die lange if/elif-Kette durch ein state_handlers-Wörterbuch zu ersetzen, das jedem ConsoleState die entsprechende Handlerfunktion zuordnet. Die aktualisierte Methode sollte einem der folgenden Beispiele ähneln:

    ```python

    def run(self) -> None:
        state_handlers = {
            ConsoleState.PATRON_SEARCH: self.patron_search,
            ConsoleState.PATRON_SEARCH_RESULTS: self.patron_search_results,
            ConsoleState.PATRON_DETAILS: self.patron_details,
            ConsoleState.LOAN_DETAILS: self.loan_details,
            ConsoleState.QUIT: lambda: ConsoleState.QUIT
        }
        while True:
            handler = state_handlers.get(self._current_state)
            if handler is None:
                print(f"Unknown state: {self._current_state}")
                break
            next_state = handler()
            if next_state == ConsoleState.QUIT:
                print("Exiting application.")
                break
            if next_state not in state_handlers:
                print(f"Unknown next state: {next_state}")
                break
            self._current_state = next_state
    ```

    Dieser Code verwendet das `state_handlers`-Wörterbuch, das jeder `ConsoleState` der entsprechenden Handlerfunktion zuordnet. Nun wird der Handler aus dem Wörterbuch abgerufen, ein Fehler für unbekannte Zustände ausgelöst und der aktuelle Zustand basierend auf dem Rückgabewert des Handlers aktualisiert.

1. Führen Sie pytest aus, und testen Sie manuell, dass sich keine Fehler eingeschlichen haben.

    Es werden dieselben Warnungen angezeigt, die Sie am Anfang dieser Übung gesehen haben, aber es sollten keine Fehlermeldungen vorhanden sein.

## Gestalten Sie Code mithilfe von Inlinechat und der Chatansicht in den Modi „Bearbeiten“ und „Agent“ um.

Durch die Übernahme von Pythons **Listenverständnis**, **Generatorausdrücken** und **integrierten Funktionen** wie `any()`, `all()`, `sum()`, `map()`, `filter()` und `sorted()`, kann die Codebasis präziser, ausdrucksstarker und effizienter werden. So lassen sich redundanter Code und potenzielle Fehler im Zusammenhang mit manueller Iteration und Datenverarbeitung verringern.

Dieser Abschnitt der Übung umfasst die folgenden Aufgaben:

- **Inlinechat: Umgestaltung des Generatorausdrucks**
- **Chat im Bearbeitungsmodus: Listenverständnis und Umgestaltung von in Python integrierten Methoden**
- **Modus „Agent“: Umgestaltung integrierter Funktionen**

### Umgestaltung des Generatorausdrucks mithilfe von Inlinechat

1. Erweitern Sie in der EXPLORER-Ansicht das Projekt **infrastructure/json_patron_repository.py**, und öffnen Sie dann die Datei **json_loan_repository.py**. Untersuchen Sie die **`JsonLoanRepository`-Klasse**.

1. Um die **`JsonLoanRepository`-Klasse** zu wählen, heben Sie den gesamten Kurs hervor.

    ```python

    class JsonPatronRepository(IPatronRepository):
        def __init__(self, json_data: JsonData):
            self._json_data = json_data
    
        def get_patron(self, patron_id: int) -> Optional[Patron]:
            for patron in self._json_data.patrons:
                if patron.id == patron_id:
                    return patron
            return None
    
        def search_patrons(self, search_input: str) -> List[Patron]:
            results = []
            for p in self._json_data.patrons:
                if search_input.lower() in p.name.lower():
                    results.append(p)
            n = len(results)
            for i in range(n):
                for j in range(0, n - i - 1):
                    if results[j].name > results[j + 1].name:
                        results[j], results[j + 1] = results[j + 1], results[j]
            return results
    
        def update_patron(self, patron: Patron) -> None:
            for idx in range(len(self._json_data.patrons)):
                if self._json_data.patrons[idx].id == patron.id:
                    self._json_data.patrons[idx] = patron
                    self._json_data.save_patrons(self._json_data.patrons)
                    return
    
        def add_patron(self, patron: Patron) -> None:
            self._json_data.patrons.append(patron)
            self._json_data.save_patrons(self._json_data.patrons)
            self._json_data.load_data()
    
        def get_all_patrons(self) -> List[Patron]:
            return self._json_data.patrons
    
        def find_patrons_by_name(self, name: str) -> List[Patron]:
            result = []
            for patron in self._json_data.patrons:
                if patron.name.lower() == name.lower():
                    result.append(patron)
            return result
    
        def get_all_books(self):
            return self._json_data.books
    
        def get_all_book_items(self):
            return self._json_data.book_items

    ```

1. Öffnen Sie einen Copilot-Inlinechat, und geben Sie dann einen Prompt ein, durch den die Methode umgestaltet wird.

    ```plaintext
    #selection Refactor any manual aggregation or search over loans in this method to use generator expressions with built-in functions like any(), all(), sum(), or max() for improved readability and performance.
    ```

1. Nehmen Sie sich einen Moment Zeit, um das vorgeschlagene Update zu überprüfen.

    Die vorgeschlagenen Aktualisierungen sollten dem folgenden Code ähneln:

    ```python
    # --code continues-- 
    def get_patron(self, patron_id: int) -> Optional[Patron]:
        return next((patron for patron in self._json_data.patrons if patron.id == patron_id), None)

    def search_patrons(self, search_input: str) -> List[Patron]:
        results = [p for p in self._json_data.patrons if search_input.lower() in p.name.lower()]
        results.sort(key=lambda p: p.name)
        return results

    def update_patron(self, patron: Patron) -> None:
        for idx, existing_patron in enumerate(self._json_data.patrons):
            if existing_patron.id == patron.id:
                self._json_data.patrons[idx] = patron
                self._json_data.save_patrons(self._json_data.patrons)
                return

    # --code continues--    
    def find_patrons_by_name(self, name: str) -> List[Patron]:
        return [patron for patron in self._json_data.patrons if patron.name.lower() == name.lower()]
    # --code continues-- 
    ```

1. Um das vorgeschlagene Update zu akzeptieren, wählen Sie **Annehmen** aus.

#### Verwenden der **intelligenten Aktion „Erklären“ des Inlinechats** zum Untersuchen einer Methode

1. Verwenden Sie die intelligente Aktion **Erklären**, um eine Erklärung der `search_patrons`-Methode anzuzeigen.

1. wählen Sie die folgenden Codezeilen (nach dem Kommentar) aus der `search_patrons`-Methode aus:

    ```python
    # def search_patrons(self, search_input: str) -> List[Patron]:
        results = [p for p in self._json_data.patrons if search_input.lower() in p.name.lower()]
        results.sort(key=lambda p: p.name)
    ```

    Wählen Sie zur Auswahl der intelligenten Aktion **Erklären** aus, wählen Sie dann im Editor den `search_patrons`-Methodencode aus und klicken Sie mit der rechten Maustaste auf die ausgewählten Codezeilen. Wählen Sie Copilot und dann **Erklären** aus. Die intelligente Aktion **Erklären** liefert eine detaillierte Erklärung des ausgewählten Codes.

    Die Erklärung könnte z. B. wie folgt aussehen:

    ```plaintext

    The `search_patrons` method is responsible for finding patrons whose names contain a given search string, regardless of case. It takes a single argument, `search_input`, which is the string to search for. The method iterates over all patrons stored in `self._json_data.patrons` and uses a list comprehension to filter those whose `name` attribute contains the `search_input` substring. Both the patron's name and the search input are converted to lowercase to ensure the search is case-insensitive.
    
    After collecting the matching patrons, the method sorts the results alphabetically by the patron's name using the `sort()` method with a key function that extracts the `name` attribute from each patron. Finally, the sorted list of matching patrons is returned. This ensures that users receive a case-insensitive, alphabetically ordered list of patrons matching their search criteria.
    
    A potential consideration is that the search will match any part of the name, not just the beginning, which may lead to more results than expected. Also, the sorting is done in-place on a new list,

    ```

1. Testen Sie Ihr Projekt und führen Sie es aus, um sicherzustellen, dass sich keine Fehler eingeschlichen haben.

#### Fortsetzen der Umgestaltung des Generatorausdrucks mithilfe von Inlinechat

1. Fahren Sie als Nächstes mit dem Umgestaltungsprozess für **loan_service.py** fort.

1. Erweitern Sie in der EXPLORER-Ansicht das **Projekt application_core\services\loan_service.py**, öffnen Sie dann die Datei **loan_service.py**, und untersuchen Sie die **`LoanService`-Klasse**.

1. Um die **`LoanService`-Klasse** zu wählen, heben Sie die gesamte Klasse hervor und untersuchen die `checkout_book`-Methode.

    ```python

    class LoanService(ILoanService):
        EXTEND_BY_DAYS = 14
    
        def __init__(self, loan_repository: ILoanRepository):
            self._loan_repository = loan_repository
    
        def return_loan(self, loan_id: int) -> LoanReturnStatus:
            loan = self._loan_repository.get_loan(loan_id)
            if loan is None:
                return LoanReturnStatus.LOAN_NOT_FOUND
            if loan.return_date is not None:
                return LoanReturnStatus.ALREADY_RETURNED
            loan.return_date = datetime.now()
            try:
                self._loan_repository.update_loan(loan)
                return LoanReturnStatus.SUCCESS
            except Exception:
                return LoanReturnStatus.ERROR
    
        def extend_loan(self, loan_id: int) -> LoanExtensionStatus:
            loan = self._loan_repository.get_loan(loan_id)
            if loan is None:
                return LoanExtensionStatus.LOAN_NOT_FOUND
            if loan.patron and loan.patron.membership_end < datetime.now():
                return LoanExtensionStatus.MEMBERSHIP_EXPIRED
            if loan.return_date is not None:
                return LoanExtensionStatus.LOAN_RETURNED
            if loan.due_date < datetime.now():
                return LoanExtensionStatus.LOAN_EXPIRED
            try:
                loan.due_date = loan.due_date + timedelta(days=self.EXTEND_BY_DAYS)
                self._loan_repository.update_loan(loan)
                return LoanExtensionStatus.SUCCESS
            except Exception:
                return LoanExtensionStatus.ERROR
    
        def checkout_book(self, patron, book_item, loan_id=None) -> None:
            from ..entities.loan import Loan
            from datetime import datetime, timedelta
            # Generate a new loan ID if not provided
            if loan_id is None:
                all_loans = getattr(self._loan_repository, 'get_all_loans', lambda: [])()
                max_id = 0
                for l in all_loans:
                    if l.id > max_id:
                        max_id = l.id
                loan_id = max_id + 1 if all_loans else 1
            now = datetime.now()
            due = now + timedelta(days=14)
            new_loan = Loan(
                id=loan_id,
                book_item_id=book_item.id,
                patron_id=patron.id,
                patron=patron,
                loan_date=now,
                due_date=due,
                return_date=None,
                book_item=book_item
            )
            self._loan_repository.add_loan(new_loan)
            return new_loan

    ```

1. Öffnen Sie einen Inlinechat, und geben Sie dann einen Prompt ein, durch den die Methode umgestaltet wird.

    ```plaintext
    #selection Refactor any manual aggregation or search over loans in this method to use generator expressions with built-in functions like any(), all(), sum(), or max() for improved readability and performance.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die vorgeschlagene Aktualisierung mit dem hinzugefügten Code in der `checkout_book`-Methode zu überprüfen:

    ```python

            loan_id = max((l.id for l in all_loans), default=0) + 1 if all_loans else 1
    ```

    Die vollständige `checkout_book`-Methode sollte folgendem Code ähneln:

    ```python
    # --code continues-- 

    def checkout_book(self, patron, book_item, loan_id=None) -> None:
            from ..entities.loan import Loan
            from datetime import datetime, timedelta
            if loan_id is None:
                all_loans = getattr(self._loan_repository, 'get_all_loans', lambda: [])()
                loan_id = max((l.id for l in all_loans), default=0) + 1 if all_loans else 1
            now = datetime.now()
            due = now + timedelta(days=14)
            new_loan = Loan(
                id=loan_id,
                book_item_id=book_item.id,
                patron_id=patron.id,
                patron=patron,
                loan_date=now,
                due_date=due,
                return_date=None,
                book_item=book_item
            )
            self._loan_repository.add_loan(new_loan)
            return new_loan
    ```

    Die Umgestaltung zur Verwendung von Generatorausdrücken ersetzt manuelle Iteration durch präzise, speichereffiziente Konstrukte, die *nahtlos mit integrierten Funktionen* wie `max()`, `any()`und `sum()` funktionieren. Dadurch werden nicht nur Codebausteine und potenzielle Fehler reduziert, sondern auch die Leistung verbessert. Dies gilt besonders für die Verarbeitung großer Datasets, da Generatorausdrücke keine Zwischenlisten im Arbeitsspeicher erstellen. Insgesamt wird die Codebasis durch diese Änderungen mehr im Python-Stil geschrieben und ist besser lesbar und wartbar.

### Umgestalten der Klasse „JsonPatronRepository“ mithilfe der Chatansicht im Bearbeitungsmodus

Die Klasse **JsonPatronRepository** enthält die folgenden drei Methoden:

- SearchPatrons: Die Methode „SearchPatrons“ dient der Suche nach Kunden anhand ihres Namens. Diese Methode gibt eine sortierte Liste von Kunden zurück.
- GetPatron: Die Methode „GetPatron“ wird verwendet, um einen Kunden anhand seiner ID abzurufen. Diese Methode gibt ein aufgefülltes Kundenobjekt zurück.
- UpdatePatron: Die Methode „UpdatePatron“ wird verwendet, um die Informationen eines Kunden zu aktualisieren. Diese Methode aktualisiert den vorhandenen Kunden mit den neuen Daten und speichert die aktualisierte Kundensammlung.

Jede der drei Methoden verwendet eine Foreach-Schleife, um die Kunden zu durchlaufen und Übereinstimmungen basierend auf der Sucheingabe oder ID zu finden.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie die Datei **json_loan_repository.py**.

    Die Klasse **JsonPatronRepository** wurde entwickelt, um Bibliothekskunden zu verwalten.

1. Nehmen Sie sich kurz Zeit, um sich einige der in der Klasse **JsonPatronRepository** enthalten Methoden genauer anzusehen.

    Die Methode **SearchPatrons** dient der Suche nach Kunden anhand ihres Namens.

    ```python

    #  ----code continues----   
    class JsonLoanRepository(ILoanRepository):
        def **init**(self, json_data: JsonData):
            self._json_data = json_data
    
        #  ----code continues----   
        def get_loans_by_patron_id(self, patron_id: int):
            result = []
            for loan in self._json_data.loans:
                if loan.patron_id == patron_id:
                    result.append(loan)
            return result
    
        #  ----code continues----  
        def get_overdue_loans(self, current_date):
            overdue = []
            for loan in self._json_data.loans:
                if loan.return_date is None and loan.due_date < current_date:
                    overdue.append(loan)
            return overdue
    
        def sort_loans_by_due_date(self):
            # Manual bubble sort for demonstration
            n = len(self._json_data.loans)
            for i in range(n):
                for j in range(0, n - i - 1):
                    if self._json_data.loans[j].due_date > self._json_data.loans[j + 1].due_date:
                        self._json_data.loans[j], self._json_data.loans[j + 1] = self._json_data.loans[j + 1], self._json_data.loans[j]
            return self._json_data.loans

        #  ----code continues----  
    ```

1. Wählen Sie in der Chatansicht **Modus festlegen** und dann **Bearbeiten** aus.

    Wenn Sie gefragt werden, ob Sie eine neue Sitzung im Modus „Bearbeiten“ starten möchten, wählen Sie **Ja** aus.

    Im Modus **Bearbeiten** zeigt GitHub Copilot Antworten als Empfehlungen zum Aktualisieren des Codes im Code-Editor an. Der Modus „Bearbeiten“ wird in der Regel verwendet, wenn ein neues Feature implementiert, ein Fehler behoben oder Code umgestaltet wird.

1. Eingeben der Eingabeaufforderung

    ```plaintext
    @codebase Refactor methods in the JsonLoanRepository class with for-loops to use list comprehensions 
    or Python built-in methods to improve code clarity, conciseness, and efficiency.
    ```

1. Beachten Sie im aktualisierten Code, der folgt, dass `get_loans_by_patron_id`- und `get_overdue_loans`-Methoden jetzt Listenverständnis verwenden und die `sort_loans_by_due_date`-Methode jetzt die integrierte Python-Funktion `sorted` verwendet.

    ```python
    #  ----code continues----

    def get_loan(self, loan_id: int) -> Optional[Loan]:
        return next((loan for loan in self._json_data.loans if loan.id == loan_id), None)

    def update_loan(self, loan: Loan) -> None:
        idx = next((i for i, l in enumerate(self._json_data.loans) if l.id == loan.id), None)
        if idx is not None:
            self._json_data.loans[idx] = loan
            self._json_data.save_loans(self._json_data.loans)
            return

    #  ----code continues----
    def get_loans_by_patron_id(self, patron_id: int):
        return [loan for loan in self._json_data.loans if loan.patron_id == patron_id]
    
    #  ----code continues----
    def get_overdue_loans(self, current_date):
        return [loan for loan in self._json_data.loans if loan.return_date is None and loan.due_date < current_date]

    def sort_loans_by_due_date(self):
        # Use built-in sorted for clarity and efficiency
        self._json_data.loans = sorted(self._json_data.loans, key=lambda l: l.due_date)
        return self._json_data.loans
    ```

    Listenverständnis und integrierte Funktionen ersetzten manuelle For-Loops zum Filtern und Sortieren, wodurch der Code kürzer, übersichtlicher und effizienter wird.

### Umgestalten der JsonLoanRepository- und JsonPatronRepository-Klassen mithilfe der Chatansicht im Modus „Agent“

1. Ändern Sie in der Chatansicht den Modus zu **Agent**.

    Der Modus „Agent“ wurde für die Ausführung von GitHub Copilot als Agent entwickelt. Sie können natürliche Sprache verwenden, um eine übergeordnete Aufgabe zu erteilen. Der Agent wertet die zugewiesene Aufgabe aus, plant die erforderliche Arbeit und wendet die Änderungen auf Ihre Codebasis an.

    Der Modus „Agent“ verwendet eine Kombination aus Codebearbeitung und dem Aufruf von Tools, um die von Ihnen angegebene Aufgabe auszuführen. Während Ihre Anforderung verarbeitet wird, werden die Ergebnisse von Bearbeitungen und Tools überwacht und es wird iterativ an der Behebung aller auftretenden Probleme gearbeitet. Wenn der Agent ein Problem nicht beheben kann, wird er Sie bitten, einzugreifen. Wenn der Agent beispielsweise mehrere Iterationen benötigt, um dasselbe Problem zu beheben, wird der Prozess angehalten und Sie werden aufgefordert, zusätzlichen Kontext bereitzustellen, um Ihre Anfrage zu klären oder den Vorgang abzubrechen.

    > **WICHTIG:** Wenn Sie die Chatansicht im Agentmodus verwenden, kann GitHub Copilot mehrere Premiumanforderungen stellen, um eine einzelne Aufgabe abzuschließen. Premium-Anfragen können durch benutzerinitiierte Eingabeaufforderungen und Folgeaktionen verwendet werden, die Copilot in Ihrem Auftrag ausführt. Die Gesamtzahl der verwendeten Premiumanforderungen hängt von der Komplexität des Vorgangs, der Anzahl der beteiligten Schritte und dem ausgewählten Modell ab.

1. Nehmen Sie sich kurz Zeit, um sich Gedanken über die Aufgabe zu machen, die Sie dem Agent zuweisen möchten.

    Die Aufgabe besteht darin, die Klassen **JsonLoanRepository** & **JsonPatronRepository** umzugestalten. Ziel ist es, manuelle Schleifen zur Umgestaltung mit **integrierten Python-Funktionen** zu finden, die dasselbe Ergebnis wie der ursprüngliche Foreach-Code erzeugen.

    Sie können auf Ihre Erfahrung mit der vorherigen Umgestaltung zurückgreifen, um die Aufgabe für den Agent zu schreiben.

1. Geben Sie den folgenden Prompt im **AGENT-Modus** ein, um dem Agent die Aufgabe zuzuweisen:

    ```plaintext

    #codebase Review the manual loop code used in the methods of the JsonLoanRepository and JsonPatronRepository classes to make them more pythonic. Refactor with Built-in Python Functions that produce the same result as the original foreach code.

    ```

    Dieser Prompt weist den Agent an, die Klasse **JsonPatronRepository** umzugestalten. Er gibt an, dass die Foreach-Schleifen durch integrierte Python-Funktionen ersetzt werden sollen.

1. Überwachen Sie den Fortschritt des Agents, während er den Code umgestaltet.

    Beachten Sie, dass der Agent die Aufgabe in mehreren Iterationen abschließt. Auf jeden Codebearbeitungsdurchlauf folgt ein Überprüfungsdurchlauf, bei dem der Code auf Probleme überprüft wird. Wenn ein Problem auftritt, wird der Code umgestaltet, um das Problem zu beheben. Wenn der Agent ein Problem nicht beheben kann, wird er Sie bitten, einzugreifen.

1. Nachdem der Agent seine Aufgabe beendet hat, nehmen Sie sich kurz Zeit, um die vorgeschlagenen Aktualisierungen zu überprüfen.

    In JsonLoanRepository sollten folgende Änderungen vorgenommenen worden sein: - `update_patron` nutzt jetzt `next` mit `enumerate` für eine effiziente Indexsuche.
        - `search_patrons` verwendet einen Generatorausdruck und `sorted` für präzisen, lesbaren Code.
        - Alle manuellen Blasensortierungen und redundanten Codes wurden entfernt.

    > **HINWEIS:** Für JsonPatronRepository wurden keine Änderungen benötigt, da bereits integrierte Funktionen und Verständnis für die Filterung und Suche verwendet werden.

    Die vorgeschlagenen Aktualisierungen sollten dem folgenden Code ähneln:

    ```python
    #  ----code continues----
    def search_patrons(self, search_input: str) -> List[Patron]:
        return sorted(
            (p for p in self._json_data.patrons if search_input.lower() in p.name.lower()),
            key=lambda patron: patron.name
        )

    def update_patron(self, patron: Patron) -> None:
        idx = next((i for i, existing_patron in enumerate(self._json_data.patrons) if existing_patron.id == patron.id), None)
        if idx is not None:
            self._json_data.patrons[idx] = patron
            self._json_data.save_patrons(self._json_data.patrons)

        #  ----code continues----

    ```

1. Wählen Sie **Behalten** aus, um alle Aktualisierungen zu akzeptieren.

Mit diesen Aktualisierungen wird der Code präziser, lesbarer und Python-bezogen, während das ursprüngliche Verhalten beibehalten wird.

### Testen und Ausführen der Anwendung

Nachdem Sie den Code umgestaltet haben, ist es an der Zeit, die Anwendung zu testen und auszuführen, um sicherzustellen, dass alles ordnungsgemäß funktioniert. Außerdem müssen Sie die Anwendung testen, um sicherzustellen, dass der umgestaltete Code wie erwartet funktioniert.

1. Um die Anwendung in Visual Studio Code mit Python auszuführen, öffnen Sie im Editor **console/main.py**, drücken **STRG+UMSCHALT+D**, um den Bereich „Ausführen und Debuggen“ zu öffnen, und wählen **Python: Aktuelle Datei** oder einer anderen Debugkonfiguration aus, und **F5**, um mit dem Debuggen zu beginnen.

    Die folgenden Schritte führen Sie durch einen einfachen Anwendungsfall.

1. Wenn Sie zur Eingabe eines Kundennamens aufgefordert werden, geben Sie **One** ein, und drücken Sie anschließend die EINGABETASTE.

    Daraufhin sollte eine Liste mit Kunden angezeigt werden, die der Suchabfrage entsprechen.

    > **HINWEIS:** Die Anwendung verwendet einen Suchvorgang, bei dem die Groß-/Kleinschreibung beachtet wird.

1. Geben Sie an der Eingabeaufforderung „Eingabeoptionen“ die Zahl **2** ein, und drücken Sie anschließend die EINGABETASTE.

    Durch Eingeben von **2** wird der zweite Kunde in der Liste ausgewählt.

    Daraufhin sollten der Name und der Mitgliedschaftsstatus des Kunden angezeigt werden, gefolgt von Details zur Buchausleihe.

1. Geben Sie an der Eingabeaufforderung „Eingabeoptionen“ die Zahl **1** ein, und drücken Sie anschließend die EINGABETASTE.

    Wenn Sie **1** eingeben, wird das erste Buch in der Liste ausgewählt.

    Es sollten Buchdetails aufgeführt sein, einschließlich des Rückgabedatums und des -status.

1. Geben Sie an der Eingabeaufforderung „Eingabeoptionen“ die Option **r** ein, und drücken Sie anschließend die EINGABETASTE.

    Die Eingabe **r** gibt das Buch zurück.

1. Überprüfen Sie, ob die Meldung „Buch wurde erfolgreich zurückgegeben“ angezeigt.

    Die Meldung „Buch wurde erfolgreich zurückgegeben" sollten die Buchdetails folgen. Zurückgegebene Bücher werden mit **Zurückgegeben: Wahr** gekennzeichnet.

1. Um eine neue Suche zu beginnen, geben Sie **s** ein, und drücken Sie dann die EINGABETASTE.

1. Wenn Sie zur Eingabe eines Kundennamens aufgefordert werden, geben Sie **One** ein, und drücken Sie anschließend die EINGABETASTE.

1. Geben Sie an der Eingabeaufforderung „Eingabeoptionen“ die Zahl **2** ein, und drücken Sie anschließend die EINGABETASTE.

1. Überprüfen Sie, ob die erste Buchausleihe als **Zurückgegeben: Wahr** markiert ist.

1. Geben Sie an der Eingabeaufforderung „Eingabeoptionen“ die Option **q** ein, und drücken Sie anschließend die EINGABETASTE.

1. Beenden Sie die Debugsitzung.

## Zusammenfassung

In dieser Übung lag der Fokus auf der Umgestaltung und Verbesserung des vorhandenen Codes mithilfe von GitHub Copilot. Sie haben die Codebasis systematisch verbessert, indem Sie manuelle Schleifen und sich wiederholende Muster durch Python-Konstrukte wie Listenverständnis, Generatorausdrücke und integrierte Funktionen ersetzen. Sie haben die verschiedenen Modi von GitHub Copilot – Fragen, Inline, Bearbeiten und Agent – verwendet, um Code zu analysieren, Umgestaltungsempfehlungen zu generieren und Verbesserungen direkt in Visual Studio Code anzuwenden. Diese Ansätze verbessern die Qualität, Lesbarkeit, Wartbarkeit und Leistung des Codes. Mit diesen Skills können Sie jetzt Python-Projekte sicher umgestalten und modernisieren, wodurch Ihre Codebasis stabiler und effizienter wird, während Sie weiterhin neue Features entwickeln.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich kurz Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder Ihrem GitHub Copilot-Abonnement vorgenommen haben, die Sie nicht beibehalten möchten. Falls Sie unerwünschte Änderungen vorgenommen haben, machen Sie diese jetzt wieder rückgängig.
