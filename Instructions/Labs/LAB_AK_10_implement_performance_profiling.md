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

- Öffnen Sie eine Eingabeaufforderung, und führen Sie die folgenden Befehle aus:

    Um sicherzustellen, dass Visual Studio Code für die Verwendung der richtigen Version von .NET konfiguriert ist, führen Sie den folgenden Befehl aus:

    ```bash
    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org
    ```

    Um sicherzustellen, dass Git für die Verwendung Ihres Namens und Ihrer E-Mail-Adresse konfiguriert ist, aktualisieren Sie die folgenden Befehle mit Ihren Informationen, und führen Sie dann die Befehle aus:

    ```bash
    git config --global user.name "John Doe"
    ```

    ```bash
    git config --global user.email johndoe@example.com
    ```

### Beispielcodeprojekt herunterladen

Führen Sie die folgenden Schritte aus, um das Beispielprojekt herunterzuladen und in Visual Studio Code zu öffnen:

1. Öffnen Sie ein Browserfenster in Ihrer Lab-Umgebung.

1. Um eine ZIP-Datei mit den Beispiel-App-Projekten herunterzuladen, öffnen Sie die folgende URL in Ihrem Browser: [GitHub Copilot Lab – Implementieren von Leistungsprofilen](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx10LabApps.zip)

    Die ZIP-Datei heißt **GHCopilotEx10LabApps.zip**.

1. Extrahieren Sie die Dateien aus der **GHCopilotEx10LabApps.zip** Datei.

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner "Downloads" in Ihrer Lab-Umgebung.

    1. Klicken Sie mit der rechten Maustaste auf *GHCopilotEx10LabApps.zip*, und wählen Sie **dann "Alle**extrahieren" aus.

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

## Übungsszenario

Sie sind Softwareentwickler, die für eine Beratungsfirma arbeiten. Ihre Clients benötigen Hilfe bei der Implementierung von Leistungsprofilen in älteren Anwendungen. Ihr Ziel ist es, die Codeleistung zu verbessern und gleichzeitig die Lesbarkeit und die vorhandene Funktionalität zu erhalten. Sie werden der folgenden App zugewiesen:

- ContosoOnlineStore: Dies ist eine E-Commerce-Anwendung, die Kundenaufträge mit realistischer Geschäftskomplexität verarbeitet. Die Anwendung umfasst produktkatalogverwaltung mit Suchfunktionen, Bestandsverfolgung mit Bestandsreservierungen, Auftragsverarbeitung mit Validierung und Bestätigungen, E-Mail-Benachrichtigungsdienste und Sicherheitsüberprüfung. Die Anwendung verwendet moderne .NET-Architekturmuster, einschließlich Abhängigkeitseinfügung, strukturierter Protokollierung und Konfigurationsverwaltung, enthält jedoch Leistungsengpässe, die reale Szenarien spiegeln.

Diese Übung umfasst die folgenden Aufgaben:

1. Überprüfen Sie die ContosoOnlineStore-Codebasis manuell.
1. Ermitteln von Leistungsengpässen mithilfe des GitHub Copilot-Chats (Ask-Modus).
1. Umgestalten Sie leistungskritischen Code mit GitHub Copilot Chat (Agent-Modus).
1. Testen und überprüfen Sie den umgestalteten ContosoOnlineStore-Code.

### Manuelles Überprüfen der ContosoOnlineStore-Codebasis

Der erste Schritt bei der Codeumgestaltung besteht darin, die vorhandene Codebasis zu verstehen, einschließlich der Projektstruktur und Geschäftslogik. Wenn Sie an Leistungsverbesserungen arbeiten, ist es auch wichtig, grundlegende Leistungsmetriken einzurichten.

In dieser Aufgabe untersuchen Sie die Hauptkomponenten des ContosoOnlineStore-Projekts, führen die Anwendung aus, um grundlegende Leistungsmetriken einzurichten und potenzielle Bereiche für die Optimierung zu identifizieren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Nehmen Sie sich ein paar Minuten Zeit um die ContosoOnlineStore-Projektstruktur zu überprüfen.

    Die Codebasis folgt modernen NET Architekturmustern mit klarer Trennung von Bedenken. Zu den wichtigsten Architekturkomponenten gehören:

    - **Konfiguration:** Stark typierte Konfiguration mit Überprüfung
    - **Dienste:** Geschäftsdienste mit Schnittstellen zur Testbarkeit  
    - **Ausnahmen:** Benutzerdefinierte domänenspezifische Ausnahmen
    - **Benchmarks**: Professionelle Leistungstests mit BenchmarkDotNet
    - **Tests**: Komponententests mit Mocking-Framework

1. Untersuchen Sie die wichtigsten Geschäftslogikklassen.

    Öffnen Sie **ProductCatalog.cs**, **OrderProcessor.cs**und **InventoryManager.cs**. Diese Klassen enthalten die Hauptgeschäftslogik und sind wahrscheinlich Kandidaten für die Leistungsoptimierung.

    Beachten Sie die Produktdatenliste (20 Produkte mit Kategorien und Beschreibungen), den komplexen Auftragsverarbeitungsworkflow und die Bestandsverwaltung mit Bestandsreservierungen.

    > **HINWEIS:** Die Codebasis enthält Kommentare, mit denen Leistungsprobleme identifiziert werden können. Suchen Sie nach Kommentaren, die als "Leistungsengpässe" oder "Leistungsproblem" gekennzeichnet sind, die absichtliche Ineffizienzen hervorheben.

1. Überprüfen Sie die Dienstebene und -konfiguration.

    Navigieren Sie zum **Ordner "Dienste** ", und überprüfen **Sie EmailService.cs** und **SecurityValidationService.cs**. Überprüfen Sie auch die Datei **Configuration/AppSettings.cs**.

    Sie werden feststellen, dass diese Dienste realistische Geschäftslogik mit konfigurierbaren Timeouts, Sicherheitsüberprüfungsregeln und E-Mail-Benachrichtigungsworkflows implementieren. Die Dienste verwenden Abhängigkeitsinjektion und Protokollierung, die folgenden Unternehmensentwicklungsmustern folgen.

1. Führen Sie die Anwendung aus, und beobachten Sie die Grundlegende Leistung.

    Sie können die Anwendung über das integrierte Terminal von Visual Studio Code ausführen, indem Sie zum Projektordner navigieren und den folgenden .NET CLI-Befehl ausführen:

    ```bash
    dotnet run
    ```

    Die Anwendung führt einen umfassenden Leistungstest aus, der Folgendes umfasst:

    - Auftragsverarbeitung mit Zeitmessung
    - Produktkatalogvorgänge (Suche, Nachschlagevorgang, Kategoriefilterung)
    - Bestandsverwaltungsvorgänge
    - Testen des gleichzeitigen Vorgangs
    - Datei für Benachrichtigungssimulation

1. Speichern Sie die grundlegenden Leistungsmetriken in einer Datei namens **baseline_metrics.txt**.

    Erstellen Sie eine Textdatei mit dem Namen baseline_metrics.txt. Kopieren Sie die Konsolenausgabe in die datei baseline_metrics.txt.

    Achten Sie auf die Anzeigedauerinformationen in der Konsolenausgabe, z. B.:

    - Auftragsverarbeitungszeit (in der Regel 2000-3000 ms für eine einzelne Bestellung)
    - Leistung der Produktsuche (anzeigedauer des einzelnen Vorgangs)
    - Dauer des Abrufvorgangs
    - Anzeigedauern für die Bestandsüberprüfung
    - Gleichzeitige Vorgangsleistung

    Die Anwendung führt auch eine umfassende Leistungsanalysesuite aus, die verschiedene Vorgänge testet und Anzeigedauerdetails meldet.

1. Nehmen Sie sich eine Minute Zeit, um die Von der datei OrderProcessingBenchmarks.cs bereitgestellten Leistungs-Benchmark-Funktionen zu untersuchen.

    Die Anwendung umfasst professionelles Benchmarking mit BenchmarkDotNet. Sie können detaillierte Leistungsvergleiche ausführen, indem Sie Folgendes ausführen:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Dadurch werden detaillierte Leistungsberichte einschließlich Speicherzuordnungsmustern und statistischer Analysen generiert.

Das Verständnis der vorhandenen Architektur- und Basisleistungsmetriken bietet die Grundlage für die Identifizierung von Optimierungsmöglichkeiten. Die Anwendung zeigt realistische E-Commerce-Leistungsherausforderungen, die Sie in nachfolgenden Aufgaben behandeln werden.

### Identifizieren von Leistungsengpässen mithilfe von GitHub Copilot Chat (Ask-Modus)

Der Ask-Modus von GitHub Copilot Chat ist ein hervorragendes Tool zur Analyse komplexer Codebasen und zur Identifizierung von Leistungsengpässen. Im Ask-Modus kann Copilot Ihre Codemuster analysieren, ineffiziente Algorithmen identifizieren und Optimierungsstrategien basierend auf bewährten Methoden vorschlagen.

In dieser Aufgabe verwenden Sie GitHub Copilot, um die ContosoOnlineStore-Anwendung systematisch zu analysieren und spezifische Leistungsverbesserungsmöglichkeiten zu identifizieren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Öffnen Sie die GitHub Copilot-Chatansicht, und konfigurieren Sie dann den Ask-Modus und das GPT-4o-Modell.

    Wenn die Chatansicht noch nicht geöffnet ist, wählen Sie oben im Visual Studio Code-Fenster das **Chatsymbol** aus. Stellen Sie sicher, dass der Chatmodus auf **"Fragen"** festgelegt ist und Sie das **GPT-4o-Modell** verwenden.

    > **HINWEIS:** Das GPT-4o-Modell bietet hervorragende Codeanalysefunktionen und wird für diese Leistungsanalyseaufgabe empfohlen.

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

    Überprüfen Sie die Analyse von GitHub Copilot, die Probleme identifizieren sollte, z. B.:

    - Lineare Suchleistung in GetProductById für bestimmte Bedingungen.
    - Ineffiziente Cacheschlüsselgenerierung in SearchProducts.
    - Fehlende optimierte Datenstrukturen für die Kategoriefilterung in "GetProductsByCategory".
    - Sequenzielle Verarbeitung mit künstlichen Verzögerungen in verschiedenen Methoden.

1. Bitten Sie GitHub Copilot, Leistungsprobleme in der OrderProcessor-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Senden Sie beispielsweise die folgende Eingabeaufforderung:

    ```text
    Examine the OrderProcessor class, particularly the CalculateOrderTotal and FinalizeOrderAsync methods. What performance problems do you see and what optimization strategies would you recommend?
    ```

    GitHub Copilot sollte Probleme identifizieren, einschließlich:

    - Einzelne Produktsuche in Schleifen (N+1-Abfragemuster).
    - Redundante Steuer- und Versandberechnungen.
    - Sequenzielle Verarbeitung von Bestellelementen.
    - Blockieren von Vorgängen, die asynchron ausgeführt werden können.

1. Bitten Sie GitHub Copilot, Leistungsprobleme in der InventoryManager-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Verwenden Sie beispielsweise diese Eingabeaufforderung, um Bestandsvorgänge zu untersuchen:

    ```text
    Review the InventoryManager class, especially the GetLowStockProducts and UpdateStockLevels methods. What are the performance concerns and how could the inventory operations be improved?
    ```

    Die Analyse sollte Folgendes offenlegen:

    - Simulation einzelner Datenbankabfragen in Schleifen.
    - Ineffiziente Protokollierungsimplementierung mit Blockierungsvorgängen.
    - Fehlende Unterstützung des Batchvorgangs.
    - Unnötige Threadverzögerungen bei Überprüfungen auf Lagerebene.

1. Bitten Sie GitHub Copilot, Leistungsprobleme in der EmailService-Klasse zu identifizieren und Optimierungen vorzuschlagen.

    Senden Sie z. B. diese Aufforderung, um den E-Mail-Dienst zu analysieren:

    ```text
    Analyze the EmailService class for performance issues. How does the email sending process impact overall application performance and what improvements could be made?
    ```

    GitHub Copilot sollte Folgendes identifizieren:

    - Sequenzielle E-Mail-Inhaltsgenerierung mit Blockierungsvorgängen.
    - Einzelne Produktsuche in E-Mail-Vorlagen.
    - Synchrone Überprüfungsvorgänge.
    - Fehlende Parallelisierungsmöglichkeiten für mehrere Empfänger.

Mithilfe der Analysefunktionen von GitHub Copilot haben Sie die wichtigsten Leistungsengpässe in der ContosoOnlineStore-Anwendung identifiziert. Die Analyse bietet eine Roadmap für Optimierungsbemühungen, die sich auf algorithmische Verbesserungen, Zwischenspeicherungsstrategien und asynchrone Verarbeitungsmuster konzentrieren.

### Umgestalten von leistungskritischem Code mithilfe von GitHub Copilot Chat (Agent-Modus)

Der Agent-Modus von GitHub Copilot bietet einen autonomen Agent, der programmieraufgaben unterstützt. Entwickler weisen allgemeine Aufgaben zu und starten dann eine agentische Codebearbeitungssitzung, um die Aufgabe auszuführen. Im Agent-Modus plant Copilot autonom die benötigten Arbeiten und bestimmt die relevanten Dateien und Kontexte. Der Agent kann Änderungen an Ihrem Code vornehmen, Tests ausführen und sogar Ihre Anwendung bereitstellen.

Im Agentmodus kann GitHub Copilot optimierte Codeimplementierungen generieren, Architekturverbesserungen vorschlagen und Leistungsverbesserungen implementieren.

In dieser Aufgabe verwenden Sie den GitHub Copilot Agent-Modus, um die in der vorherigen Aufgabe identifizierten Leistungsengpässe systematisch zu beheben.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Konfigurieren des GitHub Copilot-Chats für den Agent-Modus.

    Ändern Sie in der Chatansicht den Modus von **An** Agent** bitten**. Der Agentmodus bietet gezieltere Codegenerierungs- und Änderungsfunktionen.

1. Weisen Sie dem Agent eine Aufgabe zu, der die GetProductById-Methode in der ProductCatalog-Klasse optimiert.

    Öffnen Sie **ProductCatalog.cs** , und wählen Sie die **GetProductById-Methode** aus. Verwenden Sie den folgenden Prompt:

    ```text
    Optimize this GetProductById method to improve performance. Consider using a dictionary lookup instead of linear search and implement proper caching mechanisms.
    ```

    Überprüfen Sie die vorgeschlagenen Verbesserungen von GitHub Copilot, und implementieren Sie die Änderungen. Die optimierte Version sollte Folgendes enthalten:

    - Wörterbuchbasierte Produktsuche für O(1)-Leistung.
    - Richtige Cacheinitialisierung und -verwaltung.
    - Reduzierte redundante Vorgänge.

1. Weisen Sie dem Agent eine Aufgabe zu, die die Effizienz der SearchProducts-Methode verbessert.

    Wählen Sie die **SearchProducts-Methode** in **ProductCatalog.cs aus** , und verwenden Sie diese Eingabeaufforderung:

    ```text
    Refactor the SearchProducts method to eliminate performance bottlenecks. Optimize the search algorithm and remove unnecessary delays while maintaining search functionality.
    ```

    Wenden Sie die Vorschläge von GitHub Copilot an, um Folgendes zu implementieren:

    - Effiziente Zeichenfolgenabgleichsalgorithmen.
    - Parallele Verarbeitung für mehrere Suchkriterien.
    - Optimierte Cacheschlüsselgenerierung.

1. Weisen Sie dem Agent eine Aufgabe zu, die die Leistung der CalculateOrderTotal-Methode in der OrderProcessor-Klasse verbessert.

    Öffnen Sie **OrderProcessor.cs** , und wählen Sie die **CalculateOrderTotal-Methode** aus. Senden Sie diese Eingabeaufforderung:

    ```text
    Optimize the CalculateOrderTotal method to reduce redundant product lookups and improve calculation performance. Consider batch operations and caching strategies.
    ```

    Implementieren Sie die vorgeschlagenen Verbesserungen, die Folgendes umfassen sollten:

    - Batchproduktabruf, um N+1-Abfragemuster zu beseitigen.
    - Zwischengespeicherte Produktinformationen während der Auftragsverarbeitung.
    - Optimierte Steuer- und Versandberechnungen.

1. Optimieren Sie die FinalizeOrderAsync-Methode.

    Wählen Sie die **FinalizeOrderAsync-Methode** in **OrderProcessor.cs** aus, und verwenden Sie diese Eingabeaufforderung:

    ```text
    Refactor the FinalizeOrderAsync method to improve async performance. Focus on parallel processing where possible and optimizing await patterns.
    ```

    Wenden Sie die vorgeschlagenen Änderungen an, um folgendes zu erreichen:

    - Parallele Verarbeitung unabhängiger Vorgänge
    - Optimierte asynchrone/await-Nutzung
    - Bessere Ausnahmebehandlung in asynchronen Kontexten

1. Verbessern Sie InventoryManager-Batchvorgänge.

    Öffnen Sie **InventoryManager.cs** , und wählen Sie die **UpdateStockLevels-Methode** aus. Verwenden Sie diese Eingabeaufforderung:

    ```text
    Optimize the UpdateStockLevels method to support batch operations and reduce individual update overhead. Implement efficient logging and remove unnecessary delays.
    ```

    Implementieren Sie die Verbesserungen, um Folgendes einzuschließen:

    - Aktualisierungen auf Batchbestandsebene
    - Effiziente Protokollierungsstrategien
    - Reduzierte Blockierungsvorgänge

1. Verbessern Sie die asynchrone Verarbeitung von EmailService.

    Öffnen Sie **Dienste/EmailService.cs** , und wählen Sie die E-Mail-Sendemethoden aus. Senden Sie diese Eingabeaufforderung:

    ```text
    Optimize the email service to support parallel email processing and improve async performance. Consider implementing email queuing and batch operations.
    ```

    Wenden Sie die vorgeschlagenen Optimierungen für Folgendes an:

    - Parallele Generierung von E-Mail-Inhalten
    - Asynchrone E-Mail-Sendevorgänge
    - Verbesserte Fehlerbehandlungs- und Wiederholungslogik

Während dieses Umgestaltungsprozesses dient der GitHub Copilot Agent-Modus als Partner für die Zusammenarbeit und bietet spezifische Codeverbesserungen und Optimierungsstrategien. Der Schlüssel besteht darin, jeden Vorschlag sorgfältig zu überprüfen und an Ihre spezifischen Anforderungen und Codierungsstandards anzupassen.

### Testen und Überprüfen des umgestalteten ContosoOnlineStore-Codes

Nach der Implementierung von Leistungsoptimierungen ist es wichtig zu überprüfen, ob die Änderungen die Leistung verbessern und gleichzeitig die Funktionale Korrektheit beibehalten. Diese Aufgabe konzentriert sich auf umfassende Tests und Leistungsmessungen.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Erstellen und testen Sie die umgestaltete Anwendung.

    Führen Sie die folgenden Befehle im Visual Studio Code-Terminal aus, um sicherzustellen, dass die Anwendung erfolgreich erstellt wird:

    ```bash
    dotnet build
    ```

    Beheben Sie alle Kompilierungsfehler, die während des Umgestaltungsprozesses möglicherweise eingeführt wurden.

1. Führen Sie den Leistungstest aus.

    Führen Sie die Anwendung aus, um die Leistungsverbesserungen zu messen:

    ```bash
    dotnet run
    ```

    Vergleichen Sie die neuen Leistungsmetriken mit Ihren Basiswerten aus dem ersten Vorgang. Sie sollten Folgendes beachten:

    - Erheblich reduzierte Auftragsverarbeitungszeit (von 2000-3000 ms auf unter 500 ms)
    - Schnellere Produktsuche
    - Verbesserte Suchleistung
    - Bessere Reaktionszeiten für die Bestandsverwaltung

1. Führen Sie die umfassende Benchmark-Suite aus.

    Führen Sie die detaillierten Leistungs-Benchmarks aus, um präzise Messungen zu erhalten:

    ```bash
    dotnet run -c Release -- benchmark
    ```

    Überprüfen Sie die BenchmarkDotNet-Berichte, die detaillierte Statistiken bereitstellen, einschließlich:

    - Mittlere Ausführungszeiten mit Konfidenzintervallen
    - Speicherzuordnungsmuster
    - Durchsatzmessungen
    - Statistische Bedeutung von Verbesserungen

1. Überprüfen Sie die Funktionale Korrektheit.

    Stellen Sie sicher, dass die Optimierungen keine funktionalen Regressionen eingeführt haben:

    - Überprüfen, ob Die Bestellsummen richtig berechnet werden
    - Vergewissern Sie sich, dass Bestandsebenen ordnungsgemäß aktualisiert werden
    - Testen, dass E-Mail-Benachrichtigungen erfolgreich gesendet werden
    - Überprüfen, ob die Sicherheitsüberprüfung weiterhin funktioniert

1. Führen Sie die Komponententestsuite aus.

    Führen Sie die vorhandenen Komponententests aus, um die Codekorrektur sicherzustellen:

    ```bash
    dotnet test
    ```

    Alle Tests sollten bestehen und bestätigen, dass der umgestaltete Code das erwartete Verhalten aufrecht erhält.

1. Überprüfen der Leistungsverbesserungen

    Verwenden Sie GitHub Copilot, um die Änderungen zu dokumentieren. Senden Sie diese Eingabeaufforderung im Chat:

    ```text
    Help me create a summary of the performance optimizations implemented in this ContosoOnlineStore project. Include before/after metrics and the main optimization strategies used.
    ```

    Erstellen Sie einen Bericht zur Leistungsverbesserung, der Folgendes umfasst:

    - Baseline vs. optimierte Leistungsmetriken
    - Schlüsseloptimierungstechniken angewendet
    - Bereiche der wichtigsten Verbesserung
    - Empfehlungen für zukünftige Verbesserungen

Der Test- und Überprüfungsprozess bestätigt, dass Ihre Leistungsoptimierung erfolgreich war. Die ContosoOnlineStore-Anwendung zeigt nun eine deutlich verbesserte Leistung und gleichzeitig ihre funktionalen Anforderungen und die Architekturintegrität.

In dieser Übung haben Sie gelernt, wie Sie GitHub Copilot als leistungsstarkes Tool zur Leistungsanalyse und Optimierung verwenden und den Wert der KI-unterstützten Entwicklung bei der Bewältigung komplexer Leistungsprobleme demonstrieren.

## Zusammenfassung

In dieser Übung haben Sie GitHub Copilot erfolgreich verwendet, um Leistungsengpässe in einer komplexen E-Commerce-Anwendung zu identifizieren und zu beheben. Zu den wichtigsten Leistungen gehören:

- **Leistungsanalyse**: Verwendeter GitHub Copilot Ask-Modus, um Code systematisch zu analysieren und Engpässe zu identifizieren
- **Strategische Optimierung**: Gezielte Optimierungen zur Behandlung von N+1-Abfragemustern, ineffizienten Algorithmen und Blockierungsvorgängen
- **Gemeinsame Umgestaltung**: Nutzen des GitHub Copilot Agent-Modus zur Implementierung von Leistungsverbesserungen
- **Validierung**: Durch umfassende Tests sowohl Leistungsverbesserungen als auch Funktionskorrekturen bestätigt

Der optimierte ContosoOnlineStore zeigt dramatische Leistungsverbesserungen bei gleichzeitiger Aufrechterhaltung der Codequalität und der bewährten Methoden der Architektur. Dieser Ansatz zeigt, wie KI-basierte Entwicklungstools Leistungsoptimierungsbemühungen beschleunigen und Entwicklern helfen können, datengesteuerte Verbesserungen an komplexen Anwendungen vorzunehmen.
