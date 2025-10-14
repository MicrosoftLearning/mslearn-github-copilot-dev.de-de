---
lab:
  title: Übung – Konsolidieren von doppeltem Code mit GitHub Copilot
  description: 'Erfahren Sie, wie Sie eine komplexe Codebasis analysieren und doppelte Codelogik mithilfe von GitHub Copilot-Tools konsolidieren.'
---

# Konsolidieren von doppeltem Code mithilfe von GitHub Copilot

Doppelte Codelogik wird häufig beim Entwickeln/Erweitern einer Codebasis eingeführt, die ähnliche oder verwandte Features enthält. Es war möglicherweise nicht beabsichtigt, und Sie haben einfach nur Code wiederverwendet – und dabei den Prototyp für ein neues Feature erstellt. Wenn sich die duplizierte Logik weiterentwickelt, um den umgebenden Code im Laufe der Zeit abzugleichen, kann das Problem komplizierter werden. Änderungen an Variablennamen, Funktionsnamen und Codestrukturen an einer Stelle (aber nicht an einer anderen) können doppelte Logik verbergen. Ein rauschiger Zeitplan, eine schlechte Dokumentation und ein Mangel an ordnungsgemäßen Codeüberprüfungen kann das Problem noch verstärken. Am Ende erschwert duplizierte Logik das Lesen, Warten, Debuggen und Testen des Codes.

In dieser Übung überprüfen Sie ein vorhandenes Projekt mit duplizierter Codelogik, analysieren Die Optionen für die Konsolidierung, konsolidieren die duplizierte Codelogik und testen den umgestalteten Code, um sicherzustellen, dass es wie beabsichtigt funktioniert. Sie verwenden GitHub Copilot im Ask-Modus, um ein Verständnis für ein vorhandenes Codeprojekt zu erhalten und Optionen für die Konsolidierung der Logik zu erkunden. Sie verwenden GitHub Copilot im Agent-Modus, um den Code umzugestalten, indem Sie doppelte Logik in freigegebene Hilfsmethoden kombinieren. Sie testen den ursprünglichen und umgestalteten Code, um sicherzustellen, dass die konsolidierte Logik wie beabsichtigt funktioniert.

Diese Übung dauert ca. **30** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, müssen Sie Ihr eigenes GitHub-Konto und GitHub Copilot-Abonnement bereitstellen. Wenn Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses eigenes Konto <a href="https://github.com/" target="_blank">registrieren</a> und einen GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement in Ihrer Labumgebung haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement für diese Übung verwenden.

## Vor der Installation

Ihre Labumgebung muss die folgenden Ressourcen enthalten: Git 2.48 oder höher, .NET SDK 9.0 oder höher, Visual Studio Code mit der C#Dev Kit-Erweiterung und Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

### Konfigurieren der Laborumgebung

Bei Nutzung eines lokalen PCs als Labumgebung für diese Übung:

- Wenn Sie Hilfe beim Konfigurieren Ihres lokalen PCs als Labumgebung benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320147" target="_blank">Konfigurieren Ihrer Labumgebungsressourcen</a>.

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

Bei Nutzung einer gehosteten Labumgebung für diese Übung:

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, fügen Sie die folgende URL in die Navigationsleiste eines Browsers ein: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

- So stellen Sie sicher, dass das .NET SDK für die Verwendung des offiziellen NuGet.org-Repositorys als Quelle zum Herunterladen und Wiederherstellen von Paketen konfiguriert ist:

    Öffnen Sie ein Befehlsterminal, und führen Sie den folgenden Befehl aus:

    ```bash

    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org

    ```

### Beispielcodeprojekt herunterladen

Führen Sie die folgenden Schritte aus, um das Beispielprojekt herunterzuladen und in Visual Studio Code zu öffnen:

1. Öffnen Sie ein Browserfenster in Ihrer Lab-Umgebung.

1. Um eine ZIP-Datei mit dem Beispiel-App-Projekt herunterzuladen, öffnen Sie die folgende URL in Ihrem Browser: [GitHub Copilot Lab – Konsolidieren von doppeltem Code](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx7LabApps.zip)

    Die ZIP-Datei heißt **GHCopilotEx7LabApps.zip**.

1. Extrahieren Sie die Dateien aus der **GHCopilotEx7LabApps.zip-Datei** .

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner "Downloads" in Ihrer Lab-Umgebung.

    1. Klicken Sie mit der rechten Maustaste auf **GHCopilotEx7LabApps.zip**, und wählen Sie **dann "Alle**extrahieren" aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Kopieren Sie den **Ordner GHCopilotEx7LabApps** an einen Leicht zugänglichen Speicherort, z. B. Ihren Windows-Desktopordner.

1. Öffnen Sie den **Ordner GHCopilotEx7LabApps** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Lab-Umgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows Desktop-Ordner, wählen Sie **GHCopilotEx7LabApps** und dann "Ordner auswählen **"** aus.

1. Überprüfen Sie in der Visual Studio Code-Ansicht „PROJEKTMAPPEN-EXPLORER“ die folgende Projektmappenstruktur:

    - GHCopilotEx7LabApps\
        - ECommerceOrderAndReturn\
            - Abhängigkeiten\
            - Konfiguration\
                - AppConfig.cs
            - Modelle\
                - Order.cs
                - Return.cs
            - Sicherheit\
                - SecurityValidator.cs
            - Dienste\
                - AuditService.cs
                - EmailService.cs
                - InventoryService.cs
            - EXPECTED_OUTPUT.md
            - OrderProcessor.cs
            - Program.cs
            - README.md
            - ReturnProcessor.cs

## Übungsszenario

Sie sind Softwareentwickler, die für eine Beratungsfirma arbeiten. Ihre Clients benötigen Hilfe beim Konsolidieren doppelter Codelogik. Ihr Ziel ist es, die Code-Wartung zu verbessern und gleichzeitig die vorhandene Funktionalität beizubehalten. Sie werden der folgenden App zugewiesen:

- E-CommerceOrdersAndReturns: Dies ist eine E-Commerce-App, die Kundenbestellungen und Produktrückgaben bearbeitet. Sie enthält die Hauptgeschäftslogik für die Überprüfung von Bestellungen und Rückgaben, die Berechnung der Versandkosten, das Senden von E-Mail-Benachrichtigungen, das Protokollieren von Überwachungsaktivitäten und das Verwalten von Bestandsebenen.

Diese Übung umfasst die folgenden Aufgaben:

1. Überprüfen Sie die E-Commerce-Bestellungen, und gibt Sie codebase manuell zurück.
1. Identifizieren Sie doppelten Code mit GitHub Copilot Chat (Ask-Modus).
1. Konsolidieren Sie doppelte Logik mit GitHub Copilot Chat (Agent-Modus).
1. Testen Sie die umgestalteten E-Commerce-Bestellungen und geben Sie Code zurück.

### Überprüfen Sie die E-Commerce-Bestellungen, und gibt Sie codebase manuell zurück

Der erste Schritt bei jeder Umgestaltung besteht darin, sicherzustellen, dass Sie die vorhandene Codebasis verstehen. Es ist wichtig, die Codestruktur, die Geschäftslogik und die Ergebnisse zu verstehen, die beim Ausführen des Codes generiert werden.

In dieser Aufgabe überprüfen Sie die Hauptkomponenten des Projekts zur Bearbeitung von E-Commerce-Aufträgen und -Rückgaben, suchen im Code nach doppelten Codemustern, und testen den Code.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Nehmen Sie sich eine Minute Zeit, um die Projektstruktur von ECommerceOrderAndReturn zu überprüfen.

    Die Codebasis folgt einer schichtbasierten Architektur, die typisch für Unternehmensanwendungen ist. Zu den wichtigsten Architekturebenen gehören: Modelle, Konfiguration, Sicherheit, Dienste und Verarbeitung.

1. Untersuchen Sie die Hauptverarbeitungsklassen.

    Öffnen Sie **OrderProcessor.cs** und **ReturnProcessor.cs** nebeneinander. Diese Klassen stellen die Hauptgeschäftslogik für die Verarbeitung von Kundenbestellungen bzw. Produktrückführungen dar.

    Beachten Sie, dass die beiden Klassen ähnliche Methodensignaturen und Verarbeitungsmuster aufweisen. Diese Ähnlichkeit ist die offensichtlichste Art der Duplizierung, aber es gibt weitere, weniger auffällige Duplikate in der gesamten Codebasis.

1. Überprüfen Sie die Dienstebene.

    Navigieren Sie zum **Ordner "Dienste** ", und überprüfen **Sie EmailService.cs**, **AuditService.cs**und **InventoryService.cs**.

    Möglicherweise stellen Sie fest, dass diese Dienste ähnliche Muster für die Behandlung von E-Mail-Benachrichtigungen, Überwachungsprotokollierung und Bestandsverwaltung implementieren. Jeder Dienst verfügt über Methoden, die ähnlichen Strukturen folgen, aber für unterschiedliche Geschäftsprozesse dupliziert werden (Bestellungen oder Rückgaben).

1. Führen Sie die Anwendung aus, und überprüfen Sie die Konsolenausgabe.

    > **HINWEIS:** Eine Kopie der Konsolenausgabe wird in der datei EXPECTED_OUTPUT.md gespeichert, die im Projektverzeichnis enthalten ist. Sie verwenden diese Datei, um zu überprüfen, ob sich das Anwendungsverhalten nach der Konsolidierung des doppelten Codes nicht geändert hat.

    Sie können die Anwendung in der Projektmappen-Explorer-Ansicht ausführen, indem Sie mit der rechten Maustaste auf das **-Projekt klicken, ****Debuggen** auswählen und dann **Neue Instanz starten** auswählen.

    Die Konsolenausgabe umfasst:

    - Anfängliche Bestandsebenen
    - Auftragsverarbeitung mit Validierung, Versandberechnung, Zahlungsabwicklung, Bestandsreservierung, E-Mail-Benachrichtigungen und Überwachungsprotokollierung
    - Rückgabeverarbeitung mit ähnlichen Schritten, aber für Rückgaben angepasst
    - Aktualisierte Bestandsebenen
    - Sicherheitsüberprüfungstests mit verschiedenen ungültigen Eingaben

    Die Anwendung führt fünf Testszenarios aus, um sowohl erfolgreiche Verarbeitungs- als auch Sicherheitsüberprüfungsfehler zu veranschaulichen.

1. Nehmen Sie sich eine Minute Zeit, um alle duplizierten Codemuster zu kategorisieren, die Sie beobachtet haben.

    Zum Beispiel:

    **Duplizierte Methoden**: OrderProcessor und ReturnProcessor verfügen über identische `Validate()` und ähnliche `CalculateShipping()` Methoden.

    **Ähnliche Muster in der Dienstebene**: Jeder Dienst verfügt über Methoden, die ähnlichen Mustern folgen, aber für unterschiedliche Geschäftsprozesse dupliziert werden (Bestellungen oder Rückgaben).

Es ist wichtig, die vorhandene Funktionalität zu verstehen, bevor Sie Änderungen vornehmen. Indem Sie den Code ausführen und die Ausgabe überprüfen, richten Sie einen Basisplan ein, mit dem Sie überprüfen können, ob ihre Umgestaltung die vorhandenen Funktionen nicht unterbricht.

### Identifizieren von doppeltem Code mithilfe von GitHub Copilot Chat (Ask-Modus)

Der Ask-Modus von GitHub Copilot Chat ist ein hervorragendes Tool zum Analysieren komplexer Codebasen und zur Identifizierung subtiler Duplizierungsmuster, die möglicherweise nicht sofort offensichtlich sind. Im Ask-Modus fungiert Copilot als intelligenter Codeprüfer, der mehrere Dateien gleichzeitig analysieren und sowohl offensichtliche als auch ausgeblendete Duplikate (Codelogik) identifizieren kann.

In dieser Aufgabe verwenden Sie GitHub Copilot, um die verschiedenen Arten von doppelten Codemustern in der E-Commerce-Anwendung systematisch zu identifizieren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Öffnen Sie die GitHub Copilot Chat-Ansicht, und konfigurieren Sie dann den Ask-Modus und das GPT-4.1-Modell.

    Wenn die Chatansicht noch nicht geöffnet ist, wählen Sie oben im Visual Studio Code-Fenster das **Chatsymbol** aus. Stellen Sie sicher, dass der Chatmodus auf **"Fragen"** festgelegt ist und Sie das **GPT-4.1-Modell** verwenden.

    Das GPT-4.1-Modell ist mit dem GitHub Copilot Free-Plan verfügbar, ist für die Verarbeitung komplexer Aufgaben konzipiert und bietet intelligente Codeanalyse/-vorschläge.

1. Schließen Sie alle Dateien, die im Editor geöffnet sind.

    GitHub Copilot verwendet Dateien, die im Editor geöffnet sind, um den Kontext herzustellen. Das Schließen unerwünschter Dateiregisterkarten trägt dazu bei, Rauschen in der Analyse zu reduzieren.

1. Fügen Sie die Dateien OrderProcessor und ReturnProcessor zum Chatkontext hinzu.

    Verwenden Sie einen Drag-and-Drop-Vorgang, um die **OrderProcessor.cs** und **ReturnProcessor.cs** Dateien aus dem PROJEKTMAPPEn-EXPLORER zum Chatkontext hinzuzufügen.

    Das Hinzufügen einer Datei zum Chatkontext weist GitHub Copilot an, diese Datei beim Analysieren ihrer Eingabeaufforderung im Kontext einzuschließen.

    Wenn Sie die Standardordneransicht anstelle des PROJEKTMAPPEN-EXPLORERs verwenden, können Sie mit der rechten Maustaste auf eine Datei klicken und dann "Datei zum Chat** hinzufügen" auswählen**. Sie können auch eine Datei im Code-Editor öffnen, um den Kontext zu etablieren.

1. Bitten Sie GitHub Copilot, doppelte Codemuster in den ausgewählten Dateien zu identifizieren.

    Senden Sie beispielsweise die folgende Eingabeaufforderung, um die Kernduplizierung zu analysieren:

    ```text
    What duplicate code exists between OrderProcessor.cs and ReturnProcessor.cs? Identify specific methods and logic that are duplicated between these classes. Describe opportunities to consolidate duplicate code.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die Antwort von GitHub Copilot zu überprüfen.

    GitHub Copilot sollte die `Validate()` Methodenduplizierung und die ähnlichen Muster in `CalculateShipping()` Methoden identifizieren. Möglicherweise werden auch ähnliche Muster in Bezug auf die Überwachungsprotokollierung, Fehlerbehandlung und Zahlungs-/Rückerstattungsverarbeitung aufgeführt.

1. Aktualisieren Sie den Chatkontext, um die **EmailService.cs** Datei anzugeben.

    Öffnen Sie **EmailService.cs** im Editor. Sie können die **EmailService.cs** Datei auch mithilfe eines Drag-and-Drop-Vorgangs zum Chatkontext hinzufügen. Entfernen Sie alle anderen Dateien aus dem Kontext.

1. Bitten Sie GitHub Copilot, Duplikate in der EmailService-Klasse zu identifizieren.

    Zum Beispiel:

    ```text
    Analyze the EmailService class. What duplicate logic exists within this service for handling order confirmations versus return confirmations? Describe opportunities to consolidate duplicate code.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die Antwort von GitHub Copilot zu überprüfen.

    GitHub Copilot sollte die doppelte Logik für die Verarbeitung von Bestellbestätigungen und Rückgabebestätigungen identifizieren. Die Antwort umfasst Vorlagen zum Vorbereiten und Senden von E-Mails. GitHub Copilot kann auch doppelte Muster im Zusammenhang mit Hilfsmethoden und Konsolenausgaben identifizieren.

1. Aktualisieren Sie den Chatkontext, um die **dateien AuditService.cs** und **InventoryService.cs** anzugeben.

    Öffnen Sie **AuditService.cs** und **InventoryService.cs** im Editor. Sie können diese Dateien auch mithilfe eines Drag-and-Drop-Vorgangs zum Chatkontext hinzufügen. Entfernen Sie alle anderen Dateien aus dem Kontext.

1. Bitten Sie GitHub Copilot, Duplikate in den Überwachungs- und Bestandsdienstdateien zu identifizieren.

    Zum Beispiel:

    ```text
    Analyze the AuditService and InventoryService classes. Identify the methods that contain duplicate logic patterns that could be consolidated. Describe opportunities to consolidate duplicate code.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die Antwort von GitHub Copilot zu überprüfen.

    GitHub Copilot sollte Muster wie die Erstellung/Validierung/Speicherung von Überwachungseinträgen in AuditService und die Bestandsüberprüfung/Aktualisierung/Protokollierung in InventoryService identifizieren. GitHub Copilot kann auch doppelte Muster im Zusammenhang mit Hilfsmethoden identifizieren.

1. Bitten Sie GitHub Copilot, eine umfassende Duplizierungsanalyse durchzuführen.

    Zum Beispiel:

    ```text
    @workspace Analyze the entire ECommerceOrderAndReturn codebase and identify all forms of code duplication, including method-level, service-level, and architectural pattern duplications. Prioritize the duplications by impact and refactoring difficulty. Describe an approach for consolidating this code.
    ```

    Nachdem Sie bestimmte Dateien analysiert haben, können Sie eine breitere Ansicht erhalten, indem Sie GitHub Copilot bitten, die gesamte Codebasis in die Analyse einzuschließen. Durch den erweiterten Bereich können weitere Duplizierungsmuster angezeigt werden, z. B. ähnliche Logik bei Fehlerbehandlung, Protokollierung und Validierung über mehrere Dateien oder Ebenen hinweg. Eine einzelne Antwort, die Ihre Umgestaltungsstrategie informiert und priorisiert, ist häufig hilfreich.

    > **HINWEIS:** Die `@workspace` Schlüsselwörter `#codebase` weisen GitHub Copilot an, die gesamte Codebasis im Kontext der Analyse einzuschließen. Das `@workspace` Schlüsselwort ist nur verfügbar, wenn GitHub Copilot im Ask-Modus verwendet wird. Das `#codebase` Schlüsselwort kann in jedem Modus verwendet werden (Fragen, Bearbeiten oder Agent).

1. Nehmen Sie sich eine Minute Zeit, um die Antwort von GitHub Copilot zu überprüfen.

    Die Antwort sollte eine umfassende Analyse aller Duplizierungsmuster bereitstellen und einen Ansatz für die Konsolidierung von doppeltem Code vorschlagen. In einem Produktionsszenario sollten Sie jeden Abschnitt der Antwort analysieren und die Verwendung von Nachverfolgungsaufforderungen in Betracht ziehen, um tiefer in bestimmte Bereiche einzutauchen.

    Für diese Schulungsübung ist es wichtig zu verstehen, welche Arten von Informationen GitHub Copilot bereitstellen kann, aber Sie können sich auf den Zusammenfassungsabschnitt konzentrieren, wenn Sie Ihre Umgestaltungsstrategie berücksichtigen.

    Zum Beispiel:

    ```md
    
    **Summary**

    The codebase contains significant method-level and service-level duplication, especially in validation, shipping calculation, audit logging, email notification, and inventory management. The highest priority and easiest wins are consolidating validation and shipping logic. Service-level helper methods should be refactored next. The processor workflow pattern can be abstracted for further maintainability, though this is more complex.

    Start with shared services for validation and shipping, then refactor service helpers, and finally consider architectural abstraction for processors.

    ```

1. Überprüfen Sie die Analyse von GitHub Copilot mit manueller Codeüberprüfung.

    Referenzieren Sie die Ergebnisse von GitHub Copilot mit Ihren eigenen Beobachtungen. Stellen Sie sicher, dass Sie nicht nur verstehen, was dupliziert ist, sondern auch, warum diese Muster vorhanden sind und wie sie konsolidiert werden sollten, während die Geschäftslogikintegrität beibehalten wird.

Der Fragemodus von GitHub Copilot ist geeignet, um weniger auffällige Duplikate zu identifizieren, die über einfache Szenarios nach dem Motto „Kopieren und Einfügen“ hinausgehen. Sie kann ähnliche logische Muster, gleichwertige Geschäftsregeln, die unterschiedlich implementiert wurden, und architektonische Duplikate erkennen, die sich über mehrere Dateien erstrecken.

> **HINWEIS:** Die während dieser Aufgabe generierte Analyse wird verwendet, um die Umgestaltungsstrategie zu informieren, die Sie im nächsten Abschnitt implementieren.

### Konsolidieren doppelter Logik mit GitHub Copilot Chat (Agent-Modus)

Mit dem Agentmodus von GitHub Copilot können Sie etwas komplexere, mehrstufige Umgestaltungsaufgaben zuweisen, die mehrere Dateien und Architekturebenen umfassen. Der Agent kann autonom neue Dateien erstellen, vorhandenen Code ändern und umfassende Umgestaltungsstrategien implementieren und gleichzeitig den Fortschritt auf dem Laufenden halten.

In dieser Aufgabe verwenden Sie den GitHub Copilot-Agent, um die in der vorherigen Aufgabe identifizierten doppelten Codemuster systematisch zu beseitigen. Dabei beginnen Sie mit den einfachen Duplizierungen, bevor Sie mit komplexeren Konsolidierungen auf Dienstebene fortfahren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Wechseln Sie die GitHub Copilot Chat-Ansicht in den Agentmodus.

    Wenn Sie den Agentmodus verwenden, kann GitHub Copilot autonome Änderungen an Ihrer Codebasis vornehmen. Der Agentmodus eignet sich für etwas komplexere, mehrstufige Umgestaltungsaufgaben.

    Um Modi zu ändern, suchen Sie die Modusauswahl (in der Regel in der unteren linken Ecke der Chatansicht), und wählen Sie "Agent"** aus**.

1. Nehmen Sie sich eine Minute Zeit, um Ihre Umgestaltungsstrategie zu planen.

    Bevor Sie GitHub Copilot Agent Aufgaben zuweisen, sollten Sie die logische Reihenfolge für die Umgestaltung berücksichtigen. Verwenden Sie die Analyse aus der vorherigen Aufgabe, um Ihre Entscheidungen zu informieren.

    Zum Beispiel:

    Wenn GitHub Copilot folgendes vorgeschlagen hat:

    "Beginnen Sie mit gemeinsamen Diensten für Validierung und Versand, dann umgestalten Sie Servicehilfskräfte, und ziehen Sie schließlich die Architekturabstraktion für Prozessoren in Betracht."

    Sie können den folgenden phasenweisen Ansatz verwenden:

    - **Phase 1**: Haupt-Geschäftslogikduplizierung (Validierungs- und Versandberechnung)
    - **Phase 2**: Duplikate auf Dienstebene (E-Mail, Überwachung, Bestandsdienste)
    - **Phase 3**: Querschneidende Anliegen und Architekturverbesserungen

    Dieser phasenweise Ansatz stellt sicher, dass Änderungen verwaltbar sind und inkrementell getestet werden können.

1. Bitten Sie GitHub Copilot Agent, die Validierungslogik in den Klassen OrderProcessor und ReturnProcessor zu konsolidieren.

    Übermitteln Sie beispielsweise die folgende Aufgabe an GitHub Copilot Agent:

    ```text
    Create a shared ValidationService class that consolidates the duplicate Validate() method logic from OrderProcessor and ReturnProcessor. The service should handle ID validation for both orders and returns while maintaining all existing security checks, business rules, and logging. Update both processor classes to use the new shared service and remove the duplicate private methods. Build and test the code to ensure the functionality remains intact. Continue working until the validation service is fully integrated.
    ```

1. Überwachen Sie den Fortschritt des Agents in der Chatansicht.

    Der Status des Agents sollte im Chat sichtbar sein, da er die zugewiesene Aufgabe abgeschlossen hat.

    Um den Agent während der Verarbeitung der Aufgabe zu unterstützen, erteilen Sie die Berechtigung, den Vorgang fortzusetzen, oder stellen Sie bei Bedarf weiteren Kontext bereit. Wenn der Agent beispielsweise die Berechtigung zum Erstellen oder Ausführen der Anwendung anfragt, wählen Sie **"Weiter" aus**

    Der Agent führt während dieser Aufgabe die folgenden Schritte aus:

    - Erstellen einer neuen **ValidationService.cs** Datei im Ordner "Dienste"
    - Extrahieren der Validierungslogik in eine wiederverwendbare Methode
    - Aktualisieren beider Prozessorklassen (für die Verwendung des neuen Diensts)
    - Entfernen der doppelten privaten Überprüfungsmethoden
    - Überprüfen der Funktionalität mit einem erfolgreichen Build- und Testlauf

1. Überprüfen und akzeptieren Sie die Änderungen des Überprüfungsdiensts.

    Verwenden Sie die Code-Editor-Registerkarten, um die vom Agent vorgeschlagenen Änderungen zu untersuchen. Sie können durch die Chatbearbeitungen scrollen, um die spezifischen Codeänderungen anzuzeigen. Wählen Sie **auf der Registerkarte "Editor beibehalten** " aus, um die aktuelle Bearbeitung zu übernehmen. Sie können auf der Registerkarte "Editor" die Option "Rückgängig **" auswählen**, um eine Bearbeitung abzulehnen.

    Wählen Sie **in der Chatansicht "Beibehalten** " oder **"Rückgängig"** aus, um alle Änderungen anzunehmen oder abzulehnen.

    Der neue Überprüfungsdienst sollte alle vorhandenen Validierungslogik beibehalten und gleichzeitig eine einzige wiederverwendbare Implementierung bereitstellen. Wenn die Änderungen korrekt aussehen, akzeptieren Sie sie.

    > **HINWEIS:** Wenn Sie an Produktionscode arbeiten, ist es wichtig, den Code nach erheblichen Umgestaltungsvorgängen gründlich zu testen. Dies umfasst das Erstellen und Testen der Anwendung, um zu überprüfen, ob Features wie beabsichtigt funktionieren, Komponententests bestehen, und die Ausgabe bleibt mit dem ursprünglichen Verhalten konsistent. Um Zeit während dieser Schulungsübung zu sparen, verlassen wir uns auf den Agent, um inkrementelle Tests durchzuführen. Nach Abschluss aller Umgestaltungsaufgaben wird ein zusätzlicher (manueller Überprüfungstest) durchgeführt.

1. Bitten Sie GitHub Copilot Agent, die Versandberechnungslogik zu konsolidieren.

    Verwenden Sie beispielsweise die folgende Aufgabe, um Versandberechnungen zu konsolidieren:

    ```text
    Create a shared ShippingCalculationService that consolidates the similar CalculateShipping() logic from OrderProcessor and ReturnProcessor. The service should handle both order shipping (with free shipping thresholds) and return shipping (with processing fees) while maintaining the different business rules for each type. Update both processor classes to use the new shared service. Build and test the code to ensure the functionality remains intact. Continue working until the shipping calculation service is fully integrated.
    ```

    Der Agent sollte einen Versanddienst erstellen, der beide Szenarien verarbeitet und gleichzeitig die unterschiedlichen Geschäftsregeln für Bestellungen im Vergleich zu Rückgaben bewahrt.

    > **HINWEIS:** Wenn während des Codeumgestaltungsprozesses Probleme auftreten, sollte er sich auf die ursprünglichen Prozessorklassen beziehen, um Anleitungen zu erhalten, und er sollte den Code weiterhin aktualisieren und testen, bis der Versandberechnungsdienst vollständig integriert ist. Wenn der Agent die zugewiesene Aufgabe nicht ausführen kann oder wenn der Agent eine Coderevisionsschleife eingibt, die nicht aufgelöst werden kann, beenden Sie den Agent, und machen Sie die Bearbeitungen rückgängig. Die Chatsitzung sollte über ausreichenden Kontext verfügen, um das Problem zu beheben und die Aufgabe zu aktualisieren (Eingabeaufforderung). Sie können GitHub Copilot auch bitten, hilfe beim Aktualisieren der zugewiesenen Aufgabe auf eine Weise zu erhalten, die das Problem behebt.

1. Lesen und akzeptieren Sie den Endbenutzer-Lizenzvertrag.

1. Bitten Sie GitHub Copilot Agent, die EmailService-Duplizierungen umzugestalten.

    Verwenden Sie beispielsweise die folgende Aufgabe, um die E-Mail-Dienstduplizierungen zu konsolidieren:

    ```text
    Refactor the EmailService class to eliminate duplicate logic in the helper methods. Create a unified approach for template building, subject formatting, email sending, and activity logging that can handle both order and return confirmations. The public methods SendOrderConfirmation and SendReturnConfirmation should remain, but they should use shared private helper methods. Build and test the code to ensure the functionality remains intact. Continue working until the unified approach is fully integrated.
    ```

1. Lesen und akzeptieren Sie den Endbenutzer-Lizenzvertrag.

1. Bitten Sie GitHub Copilot Agent, AuditService-Duplizierungen zu konsolidieren.

    Verwenden Sie beispielsweise die folgende Aufgabe, um die Duplizierungen des Überwachungsdiensts zu konsolidieren:

    ```text
    Refactor the AuditService class to consolidate the duplicate logic in LogOrderActivity and LogReturnActivity. Create shared helper methods for audit entry creation, validation, storage, and compliance checking. The public methods should remain but use common underlying logic. Build and test the code to ensure the functionality remains intact. Continue working until the shared helper methods are fully integrated.
    ```

1. Lesen und akzeptieren Sie den Endbenutzer-Lizenzvertrag.

1. Bitten Sie GitHub Copilot Agent, InventoryService-Duplizierungen zu adressieren.

    Verwenden Sie beispielsweise die folgende Aufgabe, um die Inventurdienstduplizierungen zu behandeln:

    ```text
    Refactor the InventoryService class to eliminate duplicate logic between ReserveOrderInventory and RestoreReturnInventory. Create shared helper methods for inventory validation, level updates, and transaction logging while maintaining the different business logic for reservations versus restorations. Build and test the code to ensure the functionality remains intact. Continue working until the shared helper methods are fully integrated.
    ```

1. Bitten Sie GitHub Copilot Agent, alle verbleibenden Duplikate in der Codebasis zu konsolidieren.

    Verwenden Sie beispielsweise die folgende Aufgabe, um alle verbleibenden Duplikate zu beheben:

    ```text
    Analyze the entire ECommerceOrderAndReturn codebase and identify any remaining duplicate code patterns that should be consolidated. Focus on cross-cutting concerns like payment processing, status updates, and error handling. Create shared services or helper methods as needed to eliminate these duplications while maintaining existing functionality. Build and test the code to ensure the functionality remains intact. Continue working until all identified duplications are fully integrated.
    ```

    Das Zuweisen von Aufgaben wie dieser "Alle verbleibenden Probleme abfangen" zu GitHub Copilot Agent sollte nur am Ende des Umgestaltungsprozesses erfolgen und sollte nur bei Bedarf verwendet werden. Wenn Sie zu früh versuchen, diese Art von Strichanalyse zu früh zu versuchen, können unerwartete Ergebnisse oder Vorgangsfehler auftreten, die zurückgesetzt werden müssen. Es ist am besten, mithilfe eines mehrstufigen Prozesses einen geplanten Ansatz zu erstellen und Überarbeitungen vorrangig zu behandeln.

    > **Hinweis:** Auch nachdem GitHub Copilot die verbleibenden duplizierten Codemuster konsolidiert hat, gibt es möglicherweise Möglichkeiten für eine weitere Konsolidierung. Der geplante Ansatz, den Sie implementiert haben, sollte jedoch alle wichtigen Duplikate in der Codebasis konsolidieren. Wenn Sie Bedenken haben, können Sie den Analyse- und Umgestaltungsprozess wiederholen. Denken Sie daran, dass GitHub Copilot nicht als Ersatz für einen formalen Codeüberprüfungsprozess verwendet werden sollte.

Der GitHub Copilot Agent zeichnet sich durch komplexe Refactoring-Aufgaben über mehrere Dateien hinweg aus, die ein Verständnis der Geschäftslogik und architektonischer Muster erfordern. Indem Sie die Umgestaltung in logische Phasen unterteilen und inkrementelle Tests durchführen, stellen Sie sicher, dass die Konsolidierung die Systemintegrität beibehält und gleichzeitig die Codequalität, Wartungsfähigkeit, Erweiterbarkeit und Wiederverwendbarkeit erheblich verbessert.

### Testen der umgestalteten E-Commerce-Bestellungen und Zurückgeben von Code

Manuelle Tests und Überprüfungen sind entscheidend, um sicherzustellen, dass der umgestaltete Code die beabsichtigte Geschäftslogik und Funktionalität beibehält. Ein erfolgreicher Umgestaltungsprozess sollte das beabsichtigte Ziel erreichen (z. B. das Konsolidieren doppelter Codelogik) und gleichzeitig das identische Verhalten mit der ursprünglichen Implementierung erzeugen.

In dieser Aufgabe überprüfen Sie, ob der umgestaltete Code alle ursprünglichen Funktionen beibehalten hat und die Konsolidierung erfolgreich war.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Erstellen Sie das umgestaltete Projekt, um auf Kompilierungsfehler zu überprüfen.

    Wenn Kompilierungsfehler auftreten, überprüfen Sie den umgestalteten Code, und beheben Sie Probleme. Sie können GitHub Copilot verwenden, um Probleme zu diagnostizieren und zu beheben, die sich aus dem Umgestaltungsprozess ergeben.

1. Führen Sie die umgestaltete Anwendung aus, und erfassen Sie die Ausgabe.

    Die Anwendung sollte alle fünf Testszenarios genau wie zuvor ausführen:

    - Anfängliche Bestandsanzeige
    - Gültige Auftragsverarbeitung mit vollständigem Workflow
    - Gültige Rückgabeverarbeitung mit vollständigem Workflow
    - Aktualisierte Bestandsebenen
    - Sicherheitsüberprüfungstests mit ungültigen Eingaben

1. Bitten Sie GitHub Copilot, die vom umgestalteten Code generierte Ausgabe mit der ursprünglichen Ausgabe zu vergleichen.

    Zum Beispiel:

    ```text
    Run the app and compare the generated output with the contents of the EXPECTED_OUTPUT.md file. Does the current output match the stored output? Explain any differences.
    ```

    Die ursprüngliche Ausgabe, **EXPECTED_OUTPUT.md**, ist im Ordner ECommerceOrderAnd Return enthalten.

    Sie können eine zweite Ausgabedatei erstellen und GitHub Copilot bitten, alle Unterschiede zwischen den beiden Dateien zu ermitteln.

    Die Ausgabe sollte identisch sein und bestätigt, dass die Geschäftslogik unverändert bleibt, während die doppelte Codelogik konsolidiert wird.

1. Führen Sie eine abschließende Codeüberprüfung durch.

    Überprüfen Sie die umgestaltete Codebasis, um Folgendes sicherzustellen:

    - **Codequalität**: Methoden sind gut benannt und folgen konsistenten Mustern
    - **Wartbarkeit**: Änderungen an Geschäftsregeln erfordern jetzt updates nur an einem Ort.
    - **Lesbarkeit**: Die Codestruktur ist klar und logisch.
    - **Wiederverwendbarkeit**: Gemeinsame Dienste können für zukünftige Anforderungen problemlos erweitert werden
    - **Erweiterbarkeit:** Neue Features können mit minimalen Auswirkungen auf vorhandenen Code hinzugefügt werden.

Mit manuellen Tests überprüfen Sie, ob Ihre Konsolidierungsmaßnahmen den beabsichtigten Zweck erfüllt haben: doppelten Code vermeiden und die Systemfunktionalität beibehalten. Die Architektur bietet jetzt eine besser verwendbare Grundlage für die zukünftige Entwicklung, bei der Änderungen von Geschäftsregeln an einem einzigen Ort implementiert werden können, anstatt Updates über mehrere doppelte Implementierungen hinweg zu erfordern.

## Zusammenfassung

In dieser Übung haben Sie gelernt, wie Sie GitHub Copilot verwenden, um doppelten Code in einer Anwendung zu konsolidieren. Sie haben das E-Commerce Order and Return Processing System untersucht, doppelte Codemuster identifiziert und GitHub Copilot verwendet, um die Codebasis umzugestalten, um die Wartung und Lesbarkeit zu verbessern.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich kurz Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder GitHub Copilot-Abonnement vorgenommen haben, das Sie nicht beibehalten möchten. Wenn Sie Änderungen vorgenommen haben, setzen Sie sie nach Bedarf zurück. Wenn Sie einen lokalen PC als Lab-Umgebung verwenden, können Sie den Beispielprojektordner archivieren oder löschen, den Sie für diese Übung erstellt haben.
