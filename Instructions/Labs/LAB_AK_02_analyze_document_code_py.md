---
lab:
  title: 'Übung: Analysieren und Dokumentieren von Code mithilfe von GitHub Copilot (Python)'
  description: 'Hier erfahren Sie, wie Sie neuen oder unbekannten Code analysieren und Dokumentation mit GitHub Copilot in Visual Studio Code generieren.'
---

# Analysieren und Dokumentieren von Code mithilfe von GitHub Copilot

GitHub Copilot kann Ihnen dabei helfen, eine Codebasis zu verstehen und zu dokumentieren, indem Erklärungen und Dokumentation generiert werden. In dieser Übung verwenden Sie GitHub Copilot, um eine Codebasis zu analysieren und Dokumentation für das Projekt zu generieren.

Diese Übung dauert ca. **20** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, benötigen Sie ein eigenes GitHub-Konto und GitHub Copilot-Abonnement. Falls Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses Einzelkonto registrieren und den GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement in Ihrer Labumgebung haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement für diese Übung verwenden.

## Vor der Installation

Ihre Labumgebung muss die folgenden Voraussetzungen erfüllen: Git 2.48 oder höher, Python 3.10 oder höher, Visual Studio Code mit der Python-Erweiterung von Microsoft und Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

Wenn Sie einen lokalen PC als Labumgebung für diese Übung verwenden, gilt Folgendes:

- Wenn Sie Hilfe beim Konfigurieren Ihres lokalen PCs als Labumgebung benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://microsoftlearning.github.io/mslearn-github-copilot-dev/Instructions/Labs/LAB_AK_00_configure_lab_environment_py.html" target="_blank">Konfigurieren der Ressourcen für Ihre Labumgebung</a>.

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

Wenn Sie eine gehostete Labumgebung für diese Übung verwenden, gilt Folgendes:

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, fügen Sie den folgenden Link in die Navigationsleiste eines Browsers ein: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

- Öffnen Sie ein Befehlsterminal, und führen Sie die folgenden Befehle aus:

    Um sicherzustellen, dass Visual Studio Code für die Verwendung der richtigen Version von Python konfiguriert ist, stellen Sie sicher, dass die Python-Version 3.10 oder höher installiert ist:

    ```bash
    python --version
    ```

    Um sicherzustellen, dass Git für die Verwendung Ihres Namens und Ihrer E-Mail-Adresse konfiguriert ist, aktualisieren Sie die folgenden Befehle mit Ihren Informationen, und führen Sie sie dann aus:

    ```bash

    git config --global user.name "John Doe"

    ```

    ```bash

    git config --global user.email johndoe@example.com

    ```

## Übungsszenario

Sie arbeiten in der Programmierung, und zwar bei der IT-Abteilung Ihrer Gemeinde. Die Back-End-Systeme, die die öffentliche Bibliothek unterstützen, wurden bei einem Brand zerstört. Ihr Team muss ein temporäres Projekt entwickeln, damit die Mitarbeitenden der Bibliothek den Tagesbetrieb verwalten können, bis das System ersetzt werden kann. Ihr Team hat GitHub Copilot ausgewählt, um den Entwicklungsprozess zu beschleunigen.

Ein Teammitglied hat eine erste Version der Bibliotheksanwendung entwickelt. Aufgrund von Zeiteinschränkungen wurde der Code jedoch nicht dokumentiert. Sie müssen die Codebasis analysieren und ein Dokumentation für das Projekt erstellen.

Diese Übung umfasst die folgenden Aufgaben:

- Richten Sie die Bibliotheksanwendung in Visual Studio Code ein.
- Verwenden von GitHub Copilot zum Erklären der Codebasis der Bibliotheksanwendung
- Verwenden Sie GitHub Copilot, um eine README.md-Datei für die Bibliotheksanwendung zu erstellen.

## Einrichten der Bibliotheksanwendung in Visual Studio Code

Ihr Kollege hat eine erste Version der Bibliotheksanwendung entwickelt und als ZIP-Datei zur Verfügung gestellt. Sie müssen die ZIP-Datei herunterladen, die Codedateien extrahieren und dann das Projekt in Visual Studio Code öffnen.

Gehen Sie folgendermaßen vor, um die Bibliotheksanwendung einzurichten:

1. Öffnen Sie ein Browserfenster in Ihrer Labumgebung.

1. Um eine ZIP-Datei mit der Bibliotheksanwendung herunterzuladen, fügen Sie die folgende URL in die Adressleiste Ihres Browsers ein: [GitHub Copilot-Lab: Analysieren und Dokumentieren von Code](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM2Python.zip)

    Die ZIP-Datei namens AZ2007LabAppM2Python.zip wird in Ihre Labumgebung heruntergeladen.

1. Extrahieren Sie die Dateien aus der Datei **AZ2007LabAppM2Python.zip**.

    Zum Beispiel:

    1. Navigieren Sie zu dem Downloadordner Ihrer Labumgebung.

    1. Klicken Sie mit der rechten Maustaste auf **AZ2007LabAppM2Python.zip**, und wählen Sie **Alle extrahieren** aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Öffnen Sie den Ordner mit den extrahierten Dateien, und kopieren Sie dann den Ordner **AccelerateDevGHCopilot** an einen Speicherort, auf den Sie einfach zugreifen können, z. B. Ihren Windows-Ordner „Desktop“.

1. Öffnen Sie den Ordner **AccelerateDevGHCopilot** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Labumgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows-Ordner „Desktop“, und wählen Sie **AccelerateDevGHCopilot** und dann **Ordner auswählen** aus.

1. Überprüfen Sie in der EXPLORER-Ansicht von Visual Studio Code die folgende Projektstruktur:

    - AccelerateDevGHCopilot/library   ├── application_core   ├── console   ├── infrastructure   └── tests

1. Stellen Sie sicher, dass die Anwendung erfolgreich ausgeführt wird.

    Öffnen Sie beispielsweise ein Terminal in Visual Studio Code, navigieren Sie zum Verzeichnis **AccelerateDevGHCopilot/library**, und führen Sie den folgenden Befehl aus:

    ```bash
    python -m unittest discover tests
    ```

    Es werden einige Warnungen angezeigt, es sollten aber keine Fehler auftreten.

## Verwenden von GitHub Copilot zum Erklären der Codebasis der Bibliotheksanwendung

GitHub Copilot kann Ihnen helfen, eine unbekannte Codebasis zu verstehen, indem Erklärungen auf Projekt-, Datei- und Codeebene generiert werden.

### Analysieren von Code mithilfe von Prompts in der Chatansicht

Die Chatansicht von GitHub Copilot enthält eine chatbasierte Schnittstelle, über die Sie mit Prompts in natürlicher Sprache mit GitHub Copilot interagieren können. Beim erstmaligen Auswerten einer bestehenden Codebasis können Sie Prompts erstellen, die eine Erklärung auf Arbeitsbereichs- oder Projektebene oder auf Codeblock- oder Codezeilenebene generieren. Um Ihnen bei der Angabe des Kontexts Ihres Prompts zu helfen, stellt GitHub Copilot Chatkomponenten, Chatvariablen und Slashbefehle bereit.

- Chatkomponenten werden verwendet, um Ihren Prompt auf eine bestimmte Domäne festzulegen.
- Chatvariablen werden verwendet, um bestimmten Kontext in Ihren Prompt einzuschließen.
- Slashbefehle werden verwendet, um komplexe Prompts für häufige Szenarios zu vermeiden.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Stellen Sie sicher, dass das Projekt „AccelerateDevGHCopilot/library“ in Visual Studio Code geöffnet ist.

1. Öffnen Sie die Chatansicht von GitHub Copilot.

    Um die Chatansicht zu öffnen, wählen Sie oben im Fenster von Visual Studio Code die Schaltfläche **Chat umschalten** aus.

    ![Screenshot des Statusmenüs von GitHub Copilot.](./Media/m02-github-copilot-toggle-chat.png)

    Sie können die Chatansicht auch mit der Tastenkombination **STRG+ALT+I** öffnen.

1. Öffnen Sie die Chatansicht, und geben Sie dann einen Prompt ein, der die Chatkomponente **@workspace** von GitHub Copilot verwendet, um eine Beschreibung des Projekts zu generieren.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```plaintext
    @workspace describe this project
    ```

    Verwenden Sie Chatkomponenten, z. B. **@workspace**, um die von GitHub Copilot generierten Antworten zu verbessern. Chatkomponenten funktionieren wie Domänenfachleute, die Ihnen in ihren speziellen Bereichen helfen können. Verwenden Sie **@workspace**, wenn GitHub Copilot berücksichtigen soll, wie Ihr Projekt aufgebaut ist, wie verschiedene Teile Ihres Codes interagieren oder welche Entwurfsmuster in Ihrem Projekt vorhanden sind.

    Wenn Sie eine Liste aller verfügbaren Chatkomponenten anzeigen möchten, geben Sie **@** in das Feld für Chatprompts ein.

1. Nehmen Sie sich eine Minute Zeit, um die Antwort von GitHub Copilot mit den tatsächlichen Projektdateien zu vergleichen.

    Es sollte eine Antwort angezeigt werden, die die einzelnen Projekte im Projekt beschreibt:

    - **application_core**
    - **infrastructure**
    - **Konsole**
    - **Tests**

1. Verwenden Sie die EXPLORER-Ansicht, um die Projektordner zu erweitern.

1. Suchen und öffnen Sie die Datei **console_app.py**.

    Die Datei **console_app.py** befindet sich im Ordner **application _core\console**.

1. Nehmen Sie sich einen Moment Zeit, um die Codedatei zu überprüfen.

1. Geben Sie in der Chatansicht einen Prompt ein, der eine Beschreibung der Klasse **console_app.py** generiert.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```plaintext
    @workspace #usages How is the ConsoleApp class used?
    ```

    Verwenden Sie Chatvariablen, z. B. **#usages**, um bestimmten Kontext in Ihren Prompt einzuschließen. Wenn Sie eine Liste der Chatvariablen anzeigen möchten, geben Sie **#** in das Feld für Chatprompts ein.

    > **HINWEIS:** GitHub Copilot berücksichtigt Ihren Chatverlauf und die Codedateien, die Sie in Visual Studio Code geöffnet haben, wenn Sie einen Kontext für Ihren Prompt erstellen und eine Antwort generieren.

1. Nehmen Sie sich eine Minute Zeit, um die Korrektheit der Antwort von GitHub Copilot zu überprüfen.

    Es sollte eine Antwort angezeigt werden, die beschreibt, wo die **ConsoleApp**-Klasse definiert ist und wie sie in der Codebasis verwendet wird. In der Antwort wird auf die Dateien **console_app.py** und **main.py** sowie auf die Zeilennummern verwiesen.

1. Öffnen Sie die Datei **main.py** im Stamm des Ordners **application _core\console**, und untersuchen Sie den Code.

1. Geben Sie in der Chatansicht einen Prompt ein, der eine Erklärung der Datei **main.py** generiert.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```plaintext
    @workspace /explain Explain the main.py file
    ```

    Verwenden Sie Slashbefehle, z. B. **/explain**, um komplexe Prompts für häufige Szenarios zu vermeiden. Um eine Liste aller verfügbaren Slashbefehle anzuzeigen, geben Sie **/** in das Feld für Chatprompts ein. Die verfügbaren Schrägstrichbefehle können je nach Chatumgebung und -kontext variieren.

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot generierte Detailantwort zu überprüfen.

    Es sollte eine Antwort angezeigt werden, die eine Übersicht und eine Aufschlüsselung enthält, in denen erläutert wird, wie die Datei in der Anwendung verwendet wird.

1. Schließen Sie die Datei **main.py**.

### Verbessern von Chatantworten durch Hinzufügen von Kontext

GitHub Copilot verwendet Kontext, um relevantere Antworten zu generieren.

Das Öffnen von Dateien im Code-Editor ist eine Möglichkeit zum Einrichten des Kontexts. Sie können dem Chatkontext jedoch auch per Drag & Drop oder über die Schaltfläche **Kontext anfügen** in der Chatansicht Dateien hinzufügen.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Erweitern Sie den Ordner **Infrastructure**.

1. Verwenden Sie einen Drag & Drop-Vorgang, um die folgenden Dateien aus der EXPLORER-Ansicht zum Chatkontext hinzuzufügen: **json_data.py**, **json_loan_repository.py** und **json_patron_repository.py**.

    GitHub Copilot verwendet den Chatkontext, um die Codedateien zu verstehen, die für Ihren Prompt relevant sind. Sie können dem Chatkontext per Drag & Drop oder über die Schaltfläche **Kontext anfügen** in der Chatansicht Dateien hinzufügen.

    Anstatt einzelne Dateien manuell hinzuzufügen, können Sie Copilot die richtigen Dateien automatisch in Ihrer Codebasis suchen lassen. Dies kann hilfreich sein, wenn Sie nicht wissen, welche Dateien für Ihre Frage relevant sind.

    Damit Copilot die richtigen Dateien automatisch findet, fügen Sie ihrem Prompt „#codebase“ hinzu, oder wählen Sie „Codebasis“ aus der Liste der Kontexttypen aus.

1. Geben Sie einen Prompt in der Chat-Ansicht ein, der eine Erklärung der Datenzugriffsklassen generiert.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```plaintext
    @workspace /explain Explain how the data access classes work
    ```

1. Nehmen Sie sich ein paar Minuten Zeit, um die Antwort durchzulesen.

    Sie sollten eine Antwort sehen, die jede der Datenzugriffsklassen (**json_data.py**, **json_loan_repository.py** und **json_patron_repository.py**) und die Art beschreibt, wie sie zusammenarbeiten, um den Datenzugriff in der Anwendung zu verwalten. Wichtige Methoden wie **load_data**, **save_loans** und **save_patrons** sollten in der Antwort erwähnt werden.

1. Nehmen Sie sich eine Minute Zeit, um die JSON-Datendateien zu untersuchen, die zum Simulieren von Bibliotheksdatensätzen verwendet werden.

    Die JSON-Datendateien befinden sich im Ordner **infrastructure/json**.

    Die Datendateien verwenden ID-Eigenschaften, um Entitäten zu verknüpfen. Ein **loan**-Objekt hat beispielsweise eine **patron_id**-Eigenschaft, die mit einem **patron**-Objekt mit derselben ID verknüpft ist. Die JSON-Dateien enthalten Daten für Autoren, Bücher, Buchelemente, Kunden und Ausleihen.

    > **HINWEIS:** Beachten Sie, dass Autorennamen, Buchtitel und Kundennamen für die Zwecke dieser Schulung anonymisiert wurden.

### Erstellen und Ausführen der Anwendung

Das Ausführen der Anwendung hilft Ihnen, die Benutzeroberfläche, die wichtigsten Anwendungsfeatures und die Interaktion von App-Komponenten zu verstehen.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Stellen Sie sicher, dass die **Explorer**-Ansicht geöffnet ist.

1. Um die Anwendung in Visual Studio Code mit Python auszuführen, öffnen Sie **console/main.py** im Editor, drücken Sie **STRG+UMSCHALT+D**, um das Panel „Ausführen und debuggen“ zu öffnen, und klicken Sie auf **Python: Aktuelle Datei** oder eine andere Debugkonfiguration, und wählen Sie **F5** aus, um das Debuggen zu starten.

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

## Erstellen der Projektdokumentation für die Infodatei

Readme-Dateien bieten Projektmitwirkenden und Projektbeteiligten wichtige Informationen zu einem Code-Repository. Sie helfen Benutzenden, den Zweck des Projekts zu verstehen, wie es verwendet wird und wie sie etwas beitragen können. Eine gut strukturierte README-Datei kann die Benutzerfreundlichkeit und Wartbarkeit eines Projekts erheblich verbessern.

Sie benötigen eine README-Datei, die die folgenden Abschnitte enthält:

- **Projekttitel:** Ein kurzer, klarer Titel für das Projekt.
- **Beschreibung:** Eine detaillierte Erläuterung, worum es sich bei dem Projekt handelt und wofür es verwendet wird.
- **Projektstruktur**: Eine Aufschlüsselung der Projektstruktur einschließlich der wichtigen Ordner und Dateien
- **Wichtige Klassen und Schnittstellen**: Eine Liste der wichtigsten Klassen und Schnittstellen im Projekt
- **Verwendung:** Anleitung zur Verwendung des Projekts (häufig mit Codebeispielen).
- **Lizenz:** Die Lizenz für das Projekt.

In diesem Übungsabschnitt erstellen Sie mithilfe von GitHub Copilot eine Projektdokumentation und fügen diese Ihrer **README.md**-Datei hinzu.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Fügen Sie dem Stammordner des Projekts **AccelerateDevGHCopilot** eine neue Datei namens **README.md** hinzu.

1. Öffnen Sie die Chatansicht.

1. Um die Projektdokumentation für Ihre Infodatei zu generieren, geben Sie den folgenden Prompt ein:

    ```plaintext
    @workspace Generate the contents of a README.md file for a code repository. 
    Use "Library App" as the project title. The README file should include the 
    following sections: Description, Project Structure, Key Classes and Interfaces, 
    Usage, License. Format all sections as raw markdown. Use a bullet list with 
    indents to represent the project structure. Do not include ".gitignore", ".
    pyc", or the ".github", "__pycache__" folders.
    ```

    > **HINWEIS:** Wenn Sie mehrere Eingabeaufforderungen verwenden, würde eine pro Abschnitt der Infodatei detailliertere Ergebnisse liefern. In dieser Übung wird ein einziger Prompt verwendet, um den Prozess zu vereinfachen.

1. Überprüfen Sie die Antwort, um sicherzustellen, dass jeder Abschnitt als Markdown formatiert ist.

    Sie können Abschnitte einzeln aktualisieren, um detailliertere Informationen bereitzustellen oder wenn sie nicht ordnungsgemäß formatiert sind. Sie können auch die Antwort von GitHub Copilot in die Infodatei kopieren und dann direkt in der Markdowndatei Korrekturen vornehmen.

1. Kopieren Sie die vorgeschlagene Dokumentation, und fügen Sie sie dann in die README.md-Datei ein.

    Um die gesamte Antwort zu kopieren, scrollen Sie nach unten in der Antwort, klicken Sie mit der rechten Maustaste auf den leeren Bereich rechts neben dem Symbol mit dem Daumen nach oben, und wählen Sie dann **Kopieren** aus.

1. Formatieren Sie die README.md-Datei nach Bedarf.

    Sie können die Einstellungen für GitHub Copilot aktualisieren, um Markdown-Formatierung zu aktivieren, und dann GitHub Copilot verwenden, um Abschnitte der README.md-Datei zu aktualisieren.

    Wenn Sie fertig sind, sollten Sie über eine README.md-Datei verfügen, die jeden der angegebenen Abschnitte mit einer entsprechenden Detailebene enthält.

## Zusammenfassung

In dieser Übung haben Sie gelernt, wie Sie GitHub Copilot zum Analysieren und Dokumentieren einer Codebasis verwenden. Sie haben GitHub Copilot verwendet, um Erklärungen für die Projektstruktur, wichtigen Klassen und Datenzugriffsklassen zu generieren. Sie haben auch GitHub Copilot verwendet, um eine README.md-Datei für das Projekt zu erstellen.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich eine Minute Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder GitHub Copilot-Abonnement vorgenommen haben, die Sie nicht beibehalten möchten. Falls Sie Änderungen vorgenommen haben, machen Sie diese jetzt wieder rückgängig.
