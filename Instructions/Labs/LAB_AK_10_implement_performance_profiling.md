<!-- ---
lab:
    title: 'Exercise - Implement performance profiling using GitHub Copilot'
    description: 'Learn how to identify and address performance bottlenecks and code inefficiencies using GitHub Copilot tools.'
--- -->

# Implementieren von Leistungsprofilen mithilfe GitHub Copilot

Die Leistungsprofilerstellung ist ein wichtiger Aspekt der Softwareentwicklung, der dazu beiträgt, Leistungsengpässe und Codeineffizienzen zu erkennen und zu beheben.

In dieser Übung überprüfen Sie ein vorhandenes Projekt, das schlechte Leistung und ineffizienten Code enthält, Analysieren Sie Ihre Optionen zur Verbesserung der Codeleistung, umgestalten Sie den Code, um die identifizierten Probleme zu beheben, und testen Sie den umgestalteten Code, um sicherzustellen, dass die Codeleistung verbessert wurde, während Funktionalität und Lesbarkeit beibehalten werden. Sie verwenden GitHub Copilot im Ask-Modus, um ein Verständnis für ein vorhandenes Codeprojekt zu erhalten und Optionen zur Umgestaltung der identifizierten Probleme zu untersuchen. Sie verwenden GitHub Copilot im Agent-Modus, um den Code umzugestalten und die Leistung zu verbessern. Sie testen den ursprünglichen und umgestalteten Code, um die Auswirkungen Ihrer Änderungen zu messen.

Diese Übung dauert ca. **30** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, müssen Sie Ihr eigenes GitHub-Konto und GitHub Copilot-Abonnement bereitstellen. Wenn Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses eigenes Konto <a href="https://github.com/" target="_blank">registrieren</a> und einen GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement in Ihrer Labumgebung haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement für diese Übung verwenden.

## Vor der Installation

Ihre Labumgebung muss Folgendes enthalten: Git 2.48 oder höher, .NET SDK 9.0 oder höher, Visual Studio Code mit der C#Dev Kit-Erweiterung und Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

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

1. Um eine ZIP-Datei mit den Beispiel-App-Projekten herunterzuladen, öffnen Sie die folgende URL in Ihrem Browser: [GitHub Copilot Lab – Implementieren von Leistungsprofilen](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx10LabApps.zip)

    Die ZIP-Datei heißt **GHCopilotEx10LabApps.zip**.

1. Extrahieren Sie die Dateien aus der **GHCopilotEx10LabApps.zip** Datei.

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner "Downloads" in Ihrer Lab-Umgebung.

    1. Klicken Sie mit der rechten Maustaste auf **GHCopilotEx10LabApps.zip**, und wählen Sie **dann "Alle**extrahieren" aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Kopieren Sie den **Ordner GHCopilotEx10LabApps** an einen Speicherort, auf den sie leicht zugreifen können, z. B. Ihren Windows-Desktopordner.

1. Öffnen Sie den **Ordner GHCopilotEx10LabApps** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Lab-Umgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Ordner "Windows Desktop", wählen Sie **"GHCopilotEx10LabApps** " und dann "Ordner auswählen **"** aus.

1. Überprüfen Sie in der Visual Studio Code-Ansicht „PROJEKTMAPPEN-EXPLORER“ die folgende Projektmappenstruktur:

    - GHCopilotEx10LabApps\
        - ContosoOnlineStore\
            - Benchmarks\
            - Konfiguration\
            - Ausnahmen\
            - Dienste\
            - appsettings.json
            - InventoryManager.cs
            - Orders.cs
            - OrderItem.cs
            - OrderProcessor.cs
            - PERFORMANCE_GUIDE.md
            - Product.cs
            - ProductCatalog.cs
            - Program.cs
            - README.md
        - ContosoOnlineStore.Tests\
            - ContosoOnlineStoreTests.cs
            - Usings.cs
        - DataAnalyzerReporter\
            - data.txt
            - DataAnalyzer.cs
            - FileLoader.cs
            - output.txt
            - Program.cs
            - README.md
            - ReportGenerator.cs

## Übungsszenario

Sie sind Softwareentwickler, die für eine Beratungsfirma arbeiten. Ihre Clients benötigen Hilfe bei der Implementierung von Leistungsprofilen in älteren Anwendungen. Ihr Ziel ist es, die Codeleistung zu verbessern und gleichzeitig die Lesbarkeit und die vorhandene Funktionalität zu erhalten. Sie werden der folgenden App zugewiesen:

- ContosoOnlineStore: Dies ist eine E-Commerce-Anwendung, die Kundenaufträge verarbeitet. Die Anwendung umfasst produktkatalogverwaltung mit Suchfunktionen, Bestandsverfolgung mit Bestandsreservierungen, Auftragsverarbeitung mit Validierung und Bestätigungen, E-Mail-Benachrichtigungsdienste und Sicherheitsüberprüfung. Die Anwendung verwendet moderne .NET-Architekturmuster, einschließlich Abhängigkeitseinfügung, strukturierter Protokollierung und Konfigurationsverwaltung, enthält jedoch Leistungsengpässe, die reale Szenarien spiegeln.

> **HINWEIS:** Codeengpässe umfassen absichtliche Ineffizienzen und Leistungsprobleme sowie simulierte Verzögerungen, die die reale zeitliche Steuerung für externe Abhängigkeiten annähernd widerspiegeln. Simulierte Verzögerungen sollten beibehalten werden, wenn der Code umgestaltet wird, um Vorher/nachher-Leistungsvergleiche zu ermöglichen.

Diese Übung umfasst die folgenden Aufgaben:

1. Überprüfen Sie die ContosoOnlineStore-Codebasis manuell.
1. Ermitteln von Leistungsengpässen mithilfe des GitHub Copilot-Chats (Ask-Modus).
1. Umgestalten Sie leistungskritischen Code mit GitHub Copilot Chat (Agent-Modus).
1. Testen und überprüfen Sie den umgestalteten ContosoOnlineStore-Code.

### Manuelles Überprüfen der ContosoOnlineStore-Codebasis

Der erste Schritt bei der Codeumgestaltung besteht darin, die vorhandene Codebasis zu verstehen, einschließlich der Projektstruktur und Geschäftslogik. Wenn Sie an Leistungsverbesserungen arbeiten, ist es auch wichtig, grundlegende Leistungsmetriken einzurichten.

In dieser Aufgabe untersuchen Sie die Hauptkomponenten des ContosoOnlineStore-Projekts, führen die Anwendung aus, um grundlegende Leistungsmetriken einzurichten und potenzielle Bereiche für die Optimierung zu identifizieren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Nehmen Sie sich eine Minute Zeit, um die ContosoOnlineStore-Projektstruktur zu untersuchen.

    Die Codebasis folgt modernen NET Architekturmustern mit klarer Trennung von Bedenken. Zu den wichtigsten Architekturkomponenten gehören:

    - **Konfiguration:** Stark typierte Konfiguration mit Überprüfung
    - **Dienste:** Geschäftsdienste mit Schnittstellen zur Testbarkeit  
    - **Ausnahmen:** Benutzerdefinierte domänenspezifische Ausnahmen
    - **Benchmarks**: Professionelle Leistungstests mit BenchmarkDotNet
    - **Tests**: Komponententests mit Mocking-Framework

1. Nehmen Sie sich ein paar Minuten Zeit, um die Klassen **ProductCatalog.cs**, **OrderProcessor.cs** und **InventoryManager.cs** zu überprüfen.

    Diese Klassen enthalten die Hauptgeschäftslogik und sind wahrscheinlich Kandidaten für die Leistungsoptimierung.

    > **HINWEIS:** Die Codebasis enthält Kommentare, mit denen Leistungsprobleme identifiziert werden können. Suchen Sie nach Kommentaren, die als "Leistungsengpässe" oder "Leistungsproblem" gekennzeichnet sind, die absichtliche Ineffizienzen hervorheben. Simulierte Verzögerungen werden auch eingeschlossen, um die reale zeitliche Steuerung für externe Abhängigkeiten (langsame Abfragen, Netzwerkaufrufe usw.) annähernd widerzuspiegeln. Diese Verzögerungen werden beibehalten, wenn Sie die Codebasis umgestalten, um Vorher/nachher-Leistungsvergleiche zu ermöglichen.

    - **ProductCatalog.cs**: Die ProductCatalog-Klasse bietet Methoden zum Abrufen, Suchen und Kategorisieren von Produkten sowie zum Zwischenspeichern von Suchergebnissen.

    - **OrderProcessor.cs**: Die OrderProcessor-Klasse verarbeitet die Bestellüberprüfung, die Summenberechnung und die Fertigstellung, einschließlich Bestandsaktualisierungen und E-Mail-Benachrichtigungen.

    - **InventoryManager.cs**: Die InventoryManager-Klasse verwaltet Lagerbestände, Reservierungen und Warnmeldungen bei niedrigen Lagerbeständen.

1. Erweitern Sie die Ordner **Dienste** und **Konfiguration**.

    Diese Ordner enthalten zusätzliche Geschäftslogik und Konfigurationseinstellungen, die die Hauptanwendungsfunktionalität unterstützen.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Dateien **Program.cs** und **AppSettings.cs** zu überprüfen.

    Untersuchen Sie die Beziehung zwischen den Dateien „Program.cs“ und „AppSettings.cs“. Beachten Sie, dass die Datei „Program.cs“ initialisiert wird und die AppSettings-Konfiguration in die Dienste der Anwendung einfügt. Damit wird eine zentrale und flexible Kontrolle über das Anwendungsverhalten ermöglicht. Die Anwendungskonfiguration ist stark typisiert und wird beim Start überprüft, um sicherzustellen, dass alle erforderlichen Einstellungen vorhanden und ordnungsgemäß formatiert sind.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Dateien **EmailService.cs** und **SecurityValidationService.cs** zu überprüfen.

    Untersuchen Sie die Implementierung dieser Dienste. Beachten Sie, dass sie Geschäftslogik mit konfigurierbaren Timeouts, Sicherheitsüberprüfungsregeln und E-Mail-Benachrichtigungsworkflows bereitstellen. Die Dienste verwenden Abhängigkeitsinjektion und Protokollierung, die folgenden Unternehmensentwicklungsmustern folgen.

1. Führen Sie die Anwendung aus, und beobachten Sie die Grundlegende Leistung.

    Sie können die Anwendung über das integrierte Terminal von Visual Studio Code ausführen, indem Sie zum Projektordner navigieren und den folgenden .NET CLI-Befehl ausführen:

    ```bash
    dotnet run
    ```

    Die Anwendung führt einen umfassenden Leistungstest aus, der Folgendes umfasst:

    - Auftragsverarbeitung mit Zeitmessung
    - Produktkatalogvorgänge (Suche, Nachschlagevorgang, Kategoriefilterung)
    - Bestandsverwaltungsvorgänge
    - Testen gleichzeitiger Vorgänge
    - Simulation von E-Mail-Benachrichtigungen

1. Speichern Sie die grundlegenden Leistungsmetriken in einer Datei namens **baseline_metrics.txt**.

    Verwenden Sie die EXPLORER-Ansicht, um eine Textdatei namens „baseline_metrics.txt“ im Ordner „Benchmarks“ zu erstellen, und kopieren Sie dann die Konsolenausgabe in die Datei „baseline_metrics.txt“.

1. Überprüfen Sie die Datei „baseline_metrics.txt“.

    Beachten Sie die Zeitsteuerungsinformationen im Abschnitt *Ausführen der Leistungsanalyse*. Zu den wichtigsten Leistungsmetriken gehören folgende:

    - Leistung bei der Produktsuche
    - Suchleistung
    - Leistung bei der Auftragsverarbeitung
    - Leistung bei Bestandsvorgängen
    - Leistung bei gleichzeitigen Vorgängen

    Die Anwendung führt auch eine umfassende Leistungsanalysesuite aus, die verschiedene Vorgänge testet und Anzeigedauerdetails meldet.

1. Nehmen Sie sich eine Minute Zeit, um die Von der datei OrderProcessingBenchmarks.cs bereitgestellten Leistungs-Benchmark-Funktionen zu untersuchen.

    Die Anwendung umfasst professionelles Benchmarking mit BenchmarkDotNet. Sie können detaillierte Leistungsvergleiche ausführen, indem Sie Folgendes ausführen:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Durch das Ausführen dieses Befehls werden detaillierte Leistungsberichte einschließlich Speicherzuordnungsmustern und statistischer Analysen generiert. Wenn Sie möchten, können Sie die detaillierten Leistungsbenchmarkberichte für einen späteren Vergleich speichern.

Das Verständnis der vorhandenen Architektur- und Baselineleistungsmetriken bereitet den Weg für die Identifizierung von Optimierungsmöglichkeiten.

### Identifizieren von Leistungsengpässen mithilfe von GitHub Copilot Chat (Ask-Modus)

Der Ask-Modus von GitHub Copilot Chat ist ein hervorragendes Tool zur Analyse komplexer Codebasen und zur Identifizierung von Leistungsengpässen. Im Ask-Modus kann Copilot Ihre Codemuster analysieren, ineffiziente Algorithmen identifizieren und Optimierungsstrategien basierend auf bewährten Methoden vorschlagen.

In dieser Aufgabe verwenden Sie GitHub Copilot, um die ContosoOnlineStore-Anwendung systematisch zu analysieren und spezifische Leistungsverbesserungsmöglichkeiten zu identifizieren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Öffnen Sie die GitHub Copilot Chat-Ansicht, und konfigurieren Sie dann den **Fragemodus** und das **GPT-4o**-Modell.

    Um die Chatansicht zu öffnen, wählen Sie oben im Fenster von Visual Studio Code das Symbol **Chat umschalten** aus.

    > **HINWEIS:** Das GPT-4o-Modell bietet hervorragende Codeanalysefunktionen und ist im GitHub Copilot Free-Plan enthalten. Die Auswahl eines anderen Modells kann zu unterschiedlichen Ergebnissen führen.

1. Schließen Sie alle Dateien, die Sie im Editor geöffnet haben.

    GitHub Copilot verwendet Dateien, die im Editor geöffnet sind, um den Kontext herzustellen. Wenn nur die Zieldateien geöffnet sind, können Sie die Analyse auf den Code konzentrieren, den Sie optimieren möchten.

1. Fügen Sie die **Dateien InventoryManager.cs**, **OrderProcessor.cs**und **ProductCatalog.cs** zum Chatkontext hinzu.

    Verwenden Sie einen Drag-and-Drop-Vorgang, um InventoryManager.cs **, **OrderProcessor.cs** und **ProductCatalog.cs** aus dem PROJEKTMAPPEn-EXPLORER zum Chatkontext hinzuzufügen**.

    Das Hinzufügen von Dateien zum Chatkontext weist GitHub Copilot an, diese Dateien beim Analysieren Ihrer Eingabeaufforderungen einzuschließen, wodurch die Genauigkeit und Relevanz der Analyse verbessert werden.

1. Bitten Sie GitHub Copilot, Leistungsengpässe in der ProductCatalog-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```text
    Analyze the ProductCatalog class for performance bottlenecks. Focus on the GetProductById, SearchProducts, and GetProductsByCategory methods. What are the main inefficiencies and how could they be optimized?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Analyse für die ProductCatalog-Klasse.

    Die Analyse sollte Probleme identifizieren, z. B.:

    - Lineare Suchleistung in GetProductById für bestimmte Bedingungen.
    - Ineffiziente Cacheschlüsselgenerierung in SearchProducts.
    - Fehlende optimierte Datenstrukturen für die Kategoriefilterung in "GetProductsByCategory".
    - Sequenzielle Verarbeitung mit künstlichen Verzögerungen in verschiedenen Methoden.

1. Bitten Sie GitHub Copilot, die vorgeschlagenen Optimierungen auf potenzielle Risiken zu überprüfen.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

    > **WICHTIG:** Die blinde Übernahme von Vorschlägen zur Codeumgestaltung kann Sicherheitsrisiken und andere Probleme mit sich bringen. Es ist wichtig, die vorgeschlagenen Optimierungen zu bewerten und mögliche Probleme zu identifizieren. Beispielsweise können Optimierungen, die Zwischenspeicherung oder parallele Verarbeitung erfordern, Probleme mit der Threadsicherheit oder der Datenkonsistenz hervorrufen. Eine manuelle Review wird empfohlen, um sicherzustellen, dass von der KI vorgeschlagene Optimierungen weder die Sicherheit noch die Funktionalität gefährden. Regelmäßige Sicherheitsüberprüfungen und Tests sollten Teil jeder Codeumgestaltung sein.

1. Überprüfen Sie die von GitHub Copilot generierte Risikoanalyse.

    Die Risikoanalyse sollte alle potenziellen Sicherheitsrisiken oder anderen Probleme im Zusammenhang mit den vorgeschlagenen Optimierungen hervorheben. Anhand dieser Informationen können Sie fundierte Entscheidungen darüber treffen, welche Optimierungen beim Umgestalten des Codes implementiert werden sollen.

1. Bitten Sie GitHub Copilot, Leistungsprobleme in der OrderProcessor-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Senden Sie beispielsweise die folgende Eingabeaufforderung:

    ```text
    Examine the OrderProcessor class, particularly the CalculateOrderTotal and FinalizeOrderAsync methods. What performance problems do you see and what optimization strategies would you recommend?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Analyse für die OrderProcessor-Klasse.

    Die Analyse sollte Probleme identifizieren, z. B.:

    - Einzelne Produktsuche in Schleifen (N+1-Abfragemuster).
    - Redundante Steuer- und Versandberechnungen.
    - Sequenzielle Verarbeitung von Bestellelementen.
    - Blockieren von Vorgängen, die asynchron ausgeführt werden können.

1. Bitten Sie GitHub Copilot, die vorgeschlagenen Optimierungen auf potenzielle Risiken zu überprüfen.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Risikoanalyse.

1. Bitten Sie GitHub Copilot, Leistungsprobleme in der InventoryManager-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Verwenden Sie beispielsweise diese Eingabeaufforderung, um Bestandsvorgänge zu untersuchen:

    ```text
    Review the InventoryManager class, especially the GetLowStockProducts and UpdateStockLevels methods. What are the performance concerns and how could the inventory operations be improved?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Analyse für die InventoryManager-Klasse.

    Die Analyse sollte Probleme identifizieren, z. B.:

    - Simulation einzelner Datenbankabfragen in Schleifen.
    - Ineffiziente Protokollierungsimplementierung mit Blockierungsvorgängen.
    - Fehlende Unterstützung des Batchvorgangs.
    - Unnötige Threadverzögerungen bei Überprüfungen auf Lagerebene.

1. Bitten Sie GitHub Copilot, die vorgeschlagenen Optimierungen auf potenzielle Risiken zu überprüfen.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Risikoanalyse.

1. Bitten Sie GitHub Copilot, Leistungsprobleme in der EmailService-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Senden Sie z. B. diese Aufforderung, um den E-Mail-Dienst zu analysieren:

    ```text
    Analyze the EmailService class for performance issues. How does the email sending process impact overall application performance and what improvements could be made?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Analyse für die EmailService-Klasse.

    Die Analyse sollte Probleme identifizieren, z. B.:

    - Sequenzielle E-Mail-Inhaltsgenerierung mit Blockierungsvorgängen.
    - Einzelne Produktsuche in E-Mail-Vorlagen.
    - Synchrone Überprüfungsvorgänge.
    - Fehlende Parallelisierungsmöglichkeiten für mehrere Empfänger.

1. Bitten Sie GitHub Copilot, die vorgeschlagenen Optimierungen auf potenzielle Risiken zu überprüfen.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```text
    Do any of the suggested optimizations include security risks or introduce other adverse effects?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Risikoanalyse.

Mithilfe der Analysefunktionen von GitHub Copilot haben Sie Leistungsengpässe in der ContosoOnlineStore-Anwendung identifiziert. Die Analyse bietet eine Roadmap für Optimierungsbemühungen, die sich auf algorithmische Verbesserungen, Zwischenspeicherungsstrategien und asynchrone Verarbeitungsmuster konzentrieren. Durch die Analyse der von der KI vorgeschlagenen Codeoptimierungen können Risiken identifiziert werden, die mit potenziellen Leistungsverbesserungen verbunden sind. Manuelle Reviews, Sicherheitsüberprüfungen und Tests sollten Teil jeder Codeumgestaltung sein.

### Umgestalten von leistungskritischem Code mithilfe von GitHub Copilot Chat (Agent-Modus)

Der Agent-Modus von GitHub Copilot bietet einen autonomen Agent, der programmieraufgaben unterstützt. Fachkräfte in der Entwicklung weisen dem Agent allgemeine Aufgaben zu und starten dann eine Agent-Codebearbeitungssitzung, um die Aufgabe auszuführen. Der GitHub Copilot-Agent wertet die erforderliche Arbeit autonom aus, bestimmt die relevanten Dateien und den Kontext und plant, wie die Aufgabe ausgeführt werden soll. Der Agent kann Änderungen an Ihrem Code vornehmen, Tests ausführen und sogar Ihre Anwendung bereitstellen.

Im Agentmodus kann GitHub Copilot optimierte Codeimplementierungen generieren, Architekturverbesserungen vorschlagen und Leistungsverbesserungen implementieren.

In dieser Aufgabe verwenden Sie den GitHub Copilot Agent-Modus, um die in der vorherigen Aufgabe identifizierten Leistungsengpässe systematisch zu beheben.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Konfigurieren des GitHub Copilot-Chats für den Agent-Modus.

    Ändern Sie in der Chatansicht den Modus von **An** Agent** bitten**. Der Agentmodus bietet gezieltere Codegenerierungs- und Änderungsfunktionen.

1. Öffnen Sie die Datei **ProductCatalog.cs**, und wählen Sie dann die Methode **GetProductById** aus.

1. Weisen Sie dem Agent, der die GetProductById-Methode optimiert, eine Aufgabe zu.

    Geben Sie in der Chatansicht beispielsweise die folgende Aufgabe ein:

    ```text
    Review the current chat session. Optimize the GetProductById method to improve performance. Consider using a dictionary lookup instead of linear search and implement proper caching mechanisms. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot vorgeschlagenen Bearbeitungen zu überprüfen, und akzeptieren Sie dann die Änderungen.

    Die optimierte Version sollte Folgendes enthalten:

    - Wörterbuchbasierte Produktsuche für O(1)-Leistung.
    - Richtige Cacheinitialisierung und -verwaltung.
    - Reduzierte redundante Vorgänge.

    Sie können einzelne Bearbeitungen im Code-Editor überprüfen und annehmen (oder ablehnen), oder Sie können alle Änderungen auf einmal annehmen, indem Sie in der Chatansicht **Beibehalten** auswählen.

    > **HINWEIS:** Berücksichtigen Sie beim Abschließen dieses Abschnitts der Übung die Sicherheitsrisiken und andere Probleme, die in der vorherigen Aufgabe identifiziert wurden. Fachkräfte in der Entwicklung sollten sicherstellen, dass während des Optimierungsprozesses keine neuen Sicherheitsrisiken eingeführt werden. In einer Produktionsumgebung sollten manuelle Reviews, Sicherheitsüberprüfungen und Tests Teil Ihres Prozesses sein.

1. Wählen Sie im Code-Editor die Methode **SearchProducts** aus.

1. Weisen Sie dem Agent eine Aufgabe zu, die die Effizienz der SearchProducts-Methode verbessert.

    Geben Sie in der Chatansicht beispielsweise die folgende Aufgabe ein:

    ```text
    Review the current chat session. Refactor the SearchProducts method to eliminate performance bottlenecks. Optimize the search algorithm while maintaining search functionality. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot vorgeschlagenen Bearbeitungen zu überprüfen, und akzeptieren Sie dann die Änderungen.

    Die optimierte Version sollte Folgendes enthalten:

    - Effiziente Zeichenfolgenabgleichsalgorithmen.
    - Parallele Verarbeitung für mehrere Suchkriterien.
    - Optimierte Cacheschlüsselgenerierung.

1. Speichern Sie die Datei **ProductCatalog.cs**, und schließen Sie sie.

1. Öffnen Sie die Datei **OrderProcessor.cs**, und wählen Sie dann die Methode **CalculateOrderTotal** aus.

1. Weisen Sie dem Agent, der die Leistung der CalculateOrderTotal-Methode verbessert, eine Aufgabe zu.

    Geben Sie in der Chatansicht beispielsweise die folgende Aufgabe ein:

    ```text
    Review the current chat session. Optimize the CalculateOrderTotal method to reduce redundant product lookups and improve calculation performance. Consider batch operations and caching strategies. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot vorgeschlagenen Bearbeitungen zu überprüfen, und akzeptieren Sie dann die Änderungen.

    Die optimierte Version sollte Folgendes enthalten:

    - Batchproduktabruf, um N+1-Abfragemuster zu beseitigen.
    - Zwischengespeicherte Produktinformationen während der Auftragsverarbeitung.
    - Optimierte Steuer- und Versandberechnungen.

1. Wählen Sie im Code-Editor die Methode **FinalizeOrderAsync** aus.

1. Weisen Sie dem Agent, der die Leistung der FinalizeOrderAsync-Methode verbessert, eine Aufgabe zu.

    Geben Sie in der Chatansicht beispielsweise die folgende Aufgabe ein:

    ```text
    Review the current chat session. Refactor the FinalizeOrderAsync method to improve async performance. Focus on parallel processing where possible and optimizing await patterns. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot vorgeschlagenen Bearbeitungen zu überprüfen, und akzeptieren Sie dann die Änderungen.

    Die optimierte Version sollte Folgendes enthalten:

    - Parallele Verarbeitung unabhängiger Vorgänge
    - Optimierte asynchrone/await-Nutzung
    - Bessere Ausnahmebehandlung in asynchronen Kontexten

1. Speichern Sie die Datei **OrderProcessor.cs**, und schließen Sie sie.

1. Öffnen Sie die Datei **InventoryManager.cs**, und wählen Sie dann die Methode **UpdateStockLevels** aus.

1. Weisen Sie dem Agent, der die Leistung der UpdateStockLevels-Methode verbessert, eine Aufgabe zu.

    Geben Sie in der Chatansicht beispielsweise die folgende Aufgabe ein:

    ```text
    Review the current chat session. Optimize the UpdateStockLevels method to support batch operations and reduce individual update overhead. Implement efficient logging, but retain any existing artificial delays for performance comparison. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot vorgeschlagenen Bearbeitungen zu überprüfen, und akzeptieren Sie dann die Änderungen.

    Die optimierte Version sollte Folgendes enthalten:

    - Aktualisierungen auf Batchbestandsebene
    - Effiziente Protokollierungsstrategien
    - Reduzierte Blockierungsvorgänge

1. Speichern Sie die Datei **OrderProcessor.cs**, und schließen Sie sie.

1. Öffnen Sie die Datei **EmailService.cs**.

1. Weisen Sie dem Agent, der die Leistung der Methoden zum Senden von E-Mails verbessert, eine Aufgabe zu.

1. Verbessern Sie die asynchrone Verarbeitung von EmailService.

    Geben Sie in der Chatansicht beispielsweise die folgende Aufgabe ein:

    ```text
    Review the current chat session. Optimize the email service methods to support parallel email processing and improve async performance. Consider implementing email queuing and batch operations. Retain any existing artificial/simulated delays for "before and after" performance comparisons. Ensure that the refactored code doesn't introduce security vulnerabilities or other issues.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot vorgeschlagenen Bearbeitungen zu überprüfen, und akzeptieren Sie dann die Änderungen.

    Die optimierte Version sollte Folgendes enthalten:

    - Parallele Generierung von E-Mail-Inhalten
    - Asynchrone E-Mail-Sendevorgänge
    - Verbesserte Fehlerbehandlungs- und Wiederholungslogik

Während dieses Umgestaltungsprozesses dient der GitHub Copilot Agent-Modus als Partner für die Zusammenarbeit und bietet spezifische Codeverbesserungen und Optimierungsstrategien. Der Schlüssel besteht darin, jeden Vorschlag sorgfältig zu überprüfen und an Ihre spezifischen Anforderungen und Codierungsstandards anzupassen.

### Testen und Überprüfen des umgestalteten ContosoOnlineStore-Codes

Nach der Implementierung von Leistungsoptimierungen ist es wichtig zu überprüfen, ob die Änderungen die Leistung verbessern und gleichzeitig die Funktionale Korrektheit beibehalten. Diese Aufgabe konzentriert sich auf umfassende Tests und Leistungsmessungen.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Erstellen Sie die umgestaltete Anwendung, und führen Sie sie aus.

    Führen Sie den folgenden Befehl im Visual Studio Code-Terminal aus, um sicherzustellen, dass die Anwendung erfolgreich erstellt wird:

    ```bash
    dotnet build
    ```

    Beheben Sie alle Kompilierungsfehler, die während des Umgestaltungsprozesses möglicherweise eingeführt wurden.

1. Führen Sie den Leistungstest aus.

    Führen Sie den folgenden Befehl im Visual Studio Code-Terminal aus, um Leistungsmetriken für den umgestalteten Code zu generieren:

    ```bash
    dotnet run
    ```

1. Speichern Sie die neuen Leistungsmetriken in einer Datei namens **optimized_metrics.txt**.

    Verwenden Sie die EXPLORER-Ansicht, um eine Textdatei namens „optimized_metrics.txt“ im Ordner „Benchmarks“ zu erstellen, und kopieren Sie dann die Konsolenausgabe in die Datei „optimized_metrics.txt“.

1. Nehmen Sie sich eine Minute Zeit, um die optimierten Leistungsmetriken manuell mit Ihren Baselinemessungen aus der ersten Aufgabe zu vergleichen.

    Sie sollten die folgenden Leistungsverbesserungen sehen:

    - Wesentlich schnellere Produktsuchvorgänge
    - Verbesserte Suchleistung
    - Kürzere Auftragsverarbeitungszeit
    - Verbesserte Leistung gleichzeitiger Vorgänge

    Überprüfen Sie die funktionale Korrektheit für den umgestalteten Code.

    - Überprüfen Sie, ob Bestellsummen richtig berechnet werden.
    - Vergewissern Sie sich, dass Lagerbestände ordnungsgemäß aktualisiert werden.
    - Überprüfen Sie, ob E-Mail-Benachrichtigungen erfolgreich gesendet werden.
    - Überprüfen Sie, ob die Sicherheitsüberprüfung weiterhin funktioniert.

1. Erstellen Sie das Komponententestprojekt, und führen Sie es aus.

    Navigieren Sie beispielsweise im Visual Studio Code-Terminal zum Ordner **ContosoOnlineStore.Tests**, und führen Sie den folgenden Befehl aus:

    ```bash
    dotnet test
    ```

    Alle Tests sollten bestehen und bestätigen, dass der umgestaltete Code das erwartete Verhalten aufrecht erhält.

    Die Ausgabe sollte in etwa wie folgt aussehen:

    ```plaintext
    Restore complete (0.6s)
      ContosoOnlineStore succeeded (0.6s) → C:\Users\cahowd\Desktop\GHCopilotEx10LabApps\ContosoOnlineStore\bin\Debug\net9.0\ContosoOnlineStore.dll
      ContosoOnlineStore.Tests succeeded (0.2s) → bin\Debug\net9.0\ContosoOnlineStore.Tests.dll
    [xUnit.net 00:00:00.00] xUnit.net VSTest Adapter v2.4.5+1caef2f33e (64-bit .NET 9.0.9)
    [xUnit.net 00:00:02.94]   Discovering: ContosoOnlineStore.Tests
    [xUnit.net 00:00:03.02]   Discovered:  ContosoOnlineStore.Tests
    [xUnit.net 00:00:03.02]   Starting:    ContosoOnlineStore.Tests
    [xUnit.net 00:00:03.18]   Finished:    ContosoOnlineStore.Tests
      ContosoOnlineStore.Tests test succeeded (4.7s)
    
    Test summary: total: 16, failed: 0, succeeded: 16, skipped: 0, duration: 4.7s
    Build succeeded in 7.0s
    ```

1. Bitten Sie GitHub Copilot, die Leistungsverbesserungen zu analysieren.

    Geben Sie in der Chat-Ansicht beispielsweise den folgenden Prompt ein:

    ```text
    Compare the baseline_metrics.txt and optimized_metrics.txt files. Summarize the performance improvements achieved through the optimizations. Review the codebase and calculate the time associated with simulated delays for each performance test. Subtract the time associated with simulated delays from the performance data and summarize the impact of code optimizations.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die von GitHub Copilot generierte Analyse (der Leistungsverbesserungen) zu überprüfen.

    Die Analyse sollte die spezifischen Leistungsverbesserungen hervorheben, die durch die Optimierungen erzielt wurden, ohne die Auswirkungen simulierter Verzögerungen. Dies vermittelt ein klareres Bild von der Wirksamkeit der Codeänderungen.

1. Optional: Wenn Sie die detaillierte Leistungsbenchmark-Suite zu Beginn dieser Übung ausgeführt und die Ergebnisse gespeichert haben, können Sie den detaillierten Leistungsbenchmark erneut ausführen und GitHub Copilot die Ergebnisse vergleichen lassen.

    Führen Sie zum Ausführen der detaillierten Leistungsbenchmarks den folgenden Befehl im Visual Studio Code-Terminal aus:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Bitten Sie GitHub Copilot, Ihnen bei der Überprüfung der BenchmarkDotNet-Berichte zu helfen.

Der Test- und Überprüfungsprozess bestätigt, dass Ihre Leistungsoptimierung erfolgreich war. Die ContosoOnlineStore-Anwendung zeigt nun eine verbesserte Leistung, während ihre funktionalen Anforderungen und ihre architektonische Integrität erhalten bleiben.

## Zusammenfassung

In dieser Übung haben Sie GitHub Copilot erfolgreich verwendet, um Leistungsengpässe in einer komplexen E-Commerce-Anwendung zu identifizieren und zu beheben. Zu den wichtigsten Leistungen gehören:

- **Leistungsanalyse**: Verwendeter GitHub Copilot Ask-Modus, um Code systematisch zu analysieren und Engpässe zu identifizieren
- **Strategische Optimierung**: Gezielte Optimierungen zur Behandlung von N+1-Abfragemustern, ineffizienten Algorithmen und Blockierungsvorgängen
- **Gemeinsame Umgestaltung**: Nutzen des GitHub Copilot Agent-Modus zur Implementierung von Leistungsverbesserungen
- **Validierung**: Durch umfassende Tests sowohl Leistungsverbesserungen als auch Funktionskorrekturen bestätigt

Der optimierte ContosoOnlineStore zeigt dramatische Leistungsverbesserungen bei gleichzeitiger Aufrechterhaltung der Codequalität und der bewährten Methoden der Architektur. Dieser Ansatz zeigt, wie KI-basierte Entwicklungstools Leistungsoptimierungsbemühungen beschleunigen und Entwicklern helfen können, datengesteuerte Verbesserungen an komplexen Anwendungen vorzunehmen.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich eine Minute Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder GitHub Copilot-Abonnement vorgenommen haben, das Sie nicht beibehalten möchten. Wenn Sie Änderungen vorgenommen haben, setzen Sie sie nach Bedarf zurück. Wenn Sie einen lokalen PC als Lab-Umgebung verwenden, können Sie den Beispielprojektordner archivieren oder löschen, den Sie für diese Übung erstellt haben.
