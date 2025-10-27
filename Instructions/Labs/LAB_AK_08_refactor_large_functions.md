---
lab:
  title: Übung – Umgestalten großer Funktionen mithilfe von GitHub Copilot
  description: 'Erfahren Sie, wie Sie komplexen Code analysieren und große Funktionen in kleinere, fokussiertere Methoden mithilfe von GitHub Copilot-Tools umgestalten.'
---

# Umgestalten großer Funktionen mithilfe von GitHub Copilot

Große Funktionen können schwer zu lesen, zu verwalten und zu testen sein. Sie enthalten häufig mehrere Verantwortlichkeiten und können auf einen Blick herausfordernd zu verstehen sein. Die Lesbarkeit und Wartung von Code verbessert sich, wenn große Funktionen in kleinere, fokussiertere Funktionen umgestaltet werden.

In dieser Übung überprüfen Sie ein vorhandenes Projekt, das eine große Funktion enthält, Analysieren Sie Ihre Optionen für kleinere Funktionen mit einfacherer Verantwortung, umgestalten Sie die große Funktion in kleinere Funktionen, und testen Sie den umgestalteten Code, um sicherzustellen, dass es wie beabsichtigt funktioniert. Sie verwenden GitHub Copilot im Ask-Modus, um ein Verständnis für ein vorhandenes Codeprojekt zu erhalten und Optionen für die Umgestaltung der Logik zu erkunden. Sie verwenden GitHub Copilot im Agent-Modus, um den Code umzugestalten, indem Sie Codeabschnitte aus der großen Funktion extrahieren, um kleinere Funktionen zu erstellen. Sie testen den ursprünglichen und umgestalteten Code, um sicherzustellen, dass der umgestaltete Code wie beabsichtigt funktioniert.

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

1. Um eine ZIP-Datei mit dem Beispiel-App-Projekt herunterzuladen, öffnen Sie die folgende URL in Ihrem Browser: [GitHub Copilot Lab – Umgestalten großer Funktionen](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx8LabApps.zip)

    Die ZIP-Datei heißt **GHCopilotEx8LabApps.zip**.

1. Extrahieren Sie die Dateien aus der **GHCopilotEx8LabApps.zip-Datei** .

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner "Downloads" in Ihrer Lab-Umgebung.

    1. Klicken Sie mit der rechten Maustaste auf **GHCopilotEx8LabApps.zip** und wählen Sie dann **Alle extrahieren** aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Kopieren Sie den **Ordner GHCopilotEx8LabApps** an einen Leicht zugänglichen Speicherort, z. B. Ihren Windows-Desktopordner.

1. Öffnen Sie den **Ordner GHCopilotEx8LabApps** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Lab-Umgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows Desktop-Ordner, wählen Sie **GHCopilotEx8LabApps** und dann "Ordner auswählen **"** aus.

1. Überprüfen Sie in der Visual Studio Code-Ansicht „PROJEKTMAPPEN-EXPLORER“ die folgende Projektmappenstruktur:

    - GHCopilotEx8LabApps\
        - ECommerceOrderProcessing\
            - src\
                - ECommerce.ApplicationCore\
                    - Entitäten\
                    - Ausnahmen\
                    - Schnittstellen\
                    - Dienste\
                        - OrderProcessor.cs
                - ECommerce.Console\
                    - order_audit_log.txt
                    - Program.cs
                - ECommerce.Infrastructure\
                    - Dienste\
        - ServerLogAnalysisUtility\

## Übungsszenario

Sie sind Softwareentwickler, die für eine Beratungsfirma arbeiten. Ihre Clients benötigen Hilfe beim Umgestalten großer Funktionen in älteren Anwendungen. Ihr Ziel ist es, die Lesbarkeit und Wartung von Code zu verbessern und gleichzeitig die vorhandene Funktionalität beizubehalten. Sie werden der folgenden App zugewiesen:

- E-CommerceOrderProcessing: Diese E-Commerce-App wird zum Verarbeiten von Kundenbestellungen verwendet. Der Prozess umfasst die Auftragsüberprüfung, die Bestandsverwaltung, die Zahlungsabwicklung, die Versandkoordination und Kundenbenachrichtigungen. Die Anwendung verwendet Clean Architecture-Prinzipien mit einer mehrschichtigen Struktur, enthält jedoch eine große Methode in der **OrderProcessor-Klasse** , die mehrere Verantwortlichkeiten behandelt und in kleinere, fokussiertere Methoden umgestaltet werden muss.

Diese Übung umfasst die folgenden Aufgaben:

1. Überprüfen Sie die Codebasis für die Verarbeitung von E-Commerce-Bestellungen manuell.
1. Identifizieren Sie die Umgestaltungsmöglichkeiten mithilfe von GitHub Copilot Chat (Ask-Modus).
1. Umgestalten Sie eine große Funktion in kleinere, verwaltbare Funktionen mithilfe von GitHub Copilot Chat (Agent-Modus).
1. Testen Sie den umgestalteten E-Commerce-Auftragsverarbeitungscode.

### Manuelles Überprüfen der Codebasis für die Verarbeitung von E-Commerce-Bestellungen

Der erste Schritt bei jeder Umgestaltung besteht darin, sicherzustellen, dass Sie die vorhandene Codebasis verstehen. Es ist wichtig, die Codestruktur, die Geschäftslogik und die Ergebnisse zu verstehen, die beim Ausführen des Codes generiert werden.

In dieser Aufgabe überprüfen Sie die Hauptkomponenten des E-Commerce-Auftragsverarbeitungsprojekts und führen die App aus, um ihre Funktionalität zu beobachten.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Stellen Sie sicher, dass der Ordner GHCopilotEx8LabApps in Visual Studio Code geöffnet ist.

    Lesen Sie den **Abschnitt "Bevor Sie beginnen** ", wenn Sie das Beispielcodeprojekt nicht heruntergeladen haben.

1. Nehmen Sie sich eine Minute Zeit, um die Projektstruktur von ECommerceOrderProcessing zu überprüfen.

    Die Codebasis folgt einem Ebenenarchitekturmuster mit drei Hauptprojekten:

    - **ECommerce.ApplicationCore**: Enthält Domänenentitäten, Geschäftslogikschnittstellen und den Hauptauftragsverarbeiterdienst.
    - **ECommerce.Console**: Enthält den Einstiegspunkt der Konsolenanwendung und das Setup der Abhängigkeitseinfügung.
    - **ECommerce.Infrastructure**: Enthält Dienstimplementierungen für externe Integrationen (Zahlung, Versand, Bestand usw.).

    Diese Struktur stellt eine reale .NET-Anwendung mit Clean Architecture-Prinzipien dar, bei der Geschäftslogik von Infrastrukturbedenken getrennt ist.

1. Öffnen Sie die GitHub Copilot-Chatansicht.

    Wenn die Chatansicht noch nicht geöffnet ist, können Sie sie öffnen, indem Sie oben im Visual Studio Code-Fenster das **Chatsymbol** auswählen.

1. Stellen Sie in der Chatansicht sicher, dass der Chatmodus auf **"Fragen"** festgelegt ist und das Modell auf **GPT-4o**festgelegt ist.

    Diese Einstellungen sind in der unteren linken Ecke der Chatansicht verfügbar. Der Ask-Modus von **** GitHub Copilot wird verwendet, um allgemeine Codierungsfragen zu stellen und codebezogene Erklärungen zu generieren. Das **GPT-4o-Modell** , das im GitHub Copilot Free-Plan enthalten ist, ist eine gute Wahl für Codeanalyse und Umgestaltungsanleitungen.

    Sie verwenden den **Agent-Modus** von GitHub Copilot später in dieser Übung, aber jetzt verwenden Sie den **Fragemodus** für Codeanalyse und Erklärungen.

    > **HINWEIS:** Die Antworten von GitHub Copilot können je nach ausgewähltem Modell variieren. Es wird empfohlen, beim Ausführen dieser Übung das angegebene Modell zu verwenden. Sie können die Übung mit einem anderen Modell wiederholen, wenn Sie die Unterschiede sehen möchten.

1. Verwenden Sie die PROJEKTMAPPEn-EXPLORER-Ansicht, um die **OrderProcessor.cs** Datei zu suchen.

    Die **datei OrderProcessor.cs** befindet sich im **Ordner "src/ECommerce.ApplicationCore/Services** ".

1. Öffnen Sie die **datei OrderProcessor.cs** im Code-Editor.

    Die OrderProcessor-Klasse ist für die Verarbeitung von Kundenaufträgen verantwortlich. Sie enthält die haupt geschäftslogik für die Auftragsverarbeitung, einschließlich Validierung, Zahlungsverarbeitung und Benachrichtigung.

1. Nehmen Sie sich eine Minute Zeit, um die **OrderProcessor-Klasse** zu überprüfen.

    Beachten Sie die ProcessOrder-Methode. Diese Methode stellt die Hauptgeschäftslogik für die Verarbeitung von Kundenaufträgen dar. Beachten Sie, dass sie mehrere unterschiedliche Vorgänge verarbeitet. Die ProcessOrder-Methode ist absichtlich groß und komplex, um reale Szenarios zu veranschaulichen, in denen die Geschäftslogik im Laufe der Zeit komplexer wurde, was es schwierig macht, zu lesen, zu testen und zu verwalten.

1. Klicken Sie mit der rechten Maustaste auf die **ProcessOrder-Methode**, und wählen Sie **dann "Copilot** > **Erklären**" aus.

    Wenn Sie aufgefordert werden, einen eingeschlossenen Bereich auszuwählen **, der erläutert**werden soll, wählen Sie **"ProcessOrder**" aus.

    GitHub Copilot analysiert die ProcessOrder-Methode und bietet eine detaillierte Erläuterung der Funktionsweise des Codes, die Ihnen hilft, die Geschäftslogik zu verstehen, bevor Sie die Umgestaltungsoptionen untersuchen.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Erklärung von GitHub Copilot zu überprüfen.

    Die Erläuterung sollte die wichtigsten Verarbeitungsschritte und Geschäftsregeln hervorheben, z. B. die umfassenden Validierungsverfahren, Sicherheitsrisikobewertungen, Die Koordination mit mehreren Diensten und die Fehlerbehandlung mit Rollbackfunktionen.

1. Führen Sie die Anwendung aus, um ein Verständnis des aktuellen Verhaltens zu erhalten.

    Sie haben mehrere Optionen zum Ausführen der Anwendung. Zum Beispiel:

    Klicken Sie in der PROJEKTMAPPEn-EXPLORER-Ansicht mit der rechten Maustaste auf das **Projekt "ECommerce.Console"** , wählen Sie **"Debuggen"** aus, und wählen Sie **dann "Neue Instanz**starten" aus. Oder wenn die **Program.cs** Datei in Visual Studio Code geöffnet ist, können Sie die Schaltfläche "Ausführen" über dem Editor auswählen.

    Sie können auch zum **Ordner "src/ECommerce.Console"** im Terminal navigieren und den folgenden .NET CLI-Befehl eingeben:

    ```bash
    dotnet run
    ```

1. Überprüfen Sie die von der Anwendung generierte Konsolenausgabe.

    Die Anwendung generiert Ausgabe für vier Testfälle. Jeder Testfall veranschaulicht ein anderes Szenario:

    - **Test 1**: Gültige Auftragsverarbeitung mit mehreren Elementen.
    - **Test 2**: Ungültige E-Mail-Adressüberprüfung.
    - **Test 3**: Abgelehnte Zahlungsabwicklung.
    - **Test 4**: Verdächtige Sicherheitsüberprüfungen der Reihenfolge.

    Die Ausgabe für jeden Testfall zeigt die schrittweise Verarbeitung, einschließlich Validierungsmeldungen, Bestandsprüfungen, Zahlungsverarbeitung, Versandplanung und Benachrichtigungen. Die Ausgabe zeigt auch, wie verschiedene Fehlerszenarien mit entsprechenden Fehlermeldungen und Bereinigungsverfahren behandelt werden.

1. Nehmen Sie sich eine Minute Zeit, um Ihre Umgestaltungsmöglichkeiten für die ProcessOrder-Methode zu berücksichtigen.

    Die ProcessOrder-Methode hat mehrere unterschiedliche Zuständigkeiten. Jeder der entsprechenden Codeabschnitte kann in eine separate Methode extrahiert werden.

Wenn Sie die vorhandenen Funktionen verstehen und Möglichkeiten zur Umgestaltung identifizieren, können Sie eine Umgestaltungsstrategie erstellen, die die Geschäftslogik verwaltet und die Codestruktur verbessert. Die mehrschichtige Architektur bietet bereits eine gute Trennung von Bedenken auf Projektebene, aber die große ProcessOrder-Methode benötigt Aufmerksamkeit.

### Identifizieren von Umgestaltungsmöglichkeiten mithilfe von GitHub Copilot Chat (Ask-Modus)

Der Ask-Modus von GitHub Copilot Chat ist ein hervorragendes Tool zum Analysieren komplexer Code und zur Identifizierung von Möglichkeiten für die Umgestaltung großer Methoden. Im Ask-Modus kann Copilot Ihre Codestruktur analysieren und Methoden vorschlagen, um monolithische Methoden in kleinere, fokussiertere Methoden aufzuteilen.

In dieser Aufgabe verwenden Sie GitHub Copilot, um die ProcessOrder-Methode auszuwerten und Umgestaltungsmöglichkeiten zu identifizieren, die die Geschäftslogik verwalten und gleichzeitig die Codestruktur verbessern.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Stellen Sie sicher, dass die GitHub Copilot Chat-Ansicht mit **dem Ask-Modus** geöffnet ist und das **GPT-4o-Modell** ausgewählt ist.

1. Wenn Sie andere Dateien als OrderProcessor.cs geöffnet haben, schließen Sie sie jetzt.

    GitHub Copilot verwendet Dateien, die im Editor geöffnet sind, um den Kontext herzustellen. Wenn nur die Zieldatei geöffnet ist, können Sie die Analyse auf den Code konzentrieren, den Sie umgestalten möchten, und stellt sicher, dass GitHub Copilot die relevantesten Vorschläge bereitstellt.

1. Fügen Sie die OrderProcessor.cs Datei zum Chatkontext hinzu.

    Verwenden Sie einen Drag-and-Drop-Vorgang, um die **Datei "src/ECommerce.ApplicationCore/Services/OrderProcessor.cs** " aus dem PROJEKTMAPPEn-EXPLORER zum Chatkontext hinzuzufügen. Das Hinzufügen einer Datei zum Chatkontext weist GitHub Copilot an, diese Datei bei der Analyse Ihrer Eingabeaufforderung einzuschließen, wodurch die Genauigkeit der Analyse verbessert wird.

1. Bitten Sie GitHub Copilot, die ProcessOrder-Methode zur Umgestaltung von Verkaufschancen zu analysieren.

    Senden Sie eine Aufforderung, die GitHub Copilot auffordert, die ProcessOrder-Methode zu analysieren und bestimmte Verbesserungsbereiche zu identifizieren. Erwägen Sie, Details über das Zu erreichen, was Sie mit der Umgestaltung erreichen möchten.

    Zum Beispiel:

    ```text
    Analyze the ProcessOrder method in the OrderProcessor class. This method handles multiple responsibilities. Identify opportunities to break this large method into smaller, more focused methods. What specific functions could be extracted, and what would be the benefits of doing so?
    ```

1. Nehmen Sie sich ein paar Minuten Zeit, um die Antwort von GitHub Copilot zu überprüfen.

    GitHub Copilot sollte die verschiedenen Verantwortlichkeiten innerhalb der ProcessOrder-Methode identifizieren und vorschlagen, wie sie in separate Methoden extrahiert werden. Die Analyse sollte unterschiedliche logische Abschnitte identifizieren, die zu einzelnen Methoden werden können, z. B. Validierungslogik, Sicherheitsbewertungen, Bestandsvorgänge, Zahlungsverarbeitung, Versandkoordination, Benachrichtigungsverarbeitung und Auftragsabschluss.

    Beispielsweise kann GitHub Copilot Folgendes identifizieren:

    - Eingabeüberprüfung und Sicherheitsüberprüfungen als Kandidaten für die Extraktion.
    - Bestandsverwaltungsvorgänge, die gruppiert werden können.
    - Zahlungsverarbeitungslogik mit eigener Fehlerbehandlung.
    - Versand- und Benachrichtigungslogik als separate Bedenken.
    - Abschlussschritte der Reihenfolge, die isoliert werden können.

1. Bitten Sie GitHub Copilot, einen detaillierten Umgestaltungsplan bereitzustellen.

    Zum Beispiel:

    ```text
    Create a detailed refactoring plan for the ProcessOrder method. Show me what the ProcessOrder method would look like after refactoring and provide a list of the methods that should be extracted. I'd like to keep the input validation and security checks together in a single method. Include suggestions for method signatures and return types that would maintain the current error handling behavior.
    ```

    Nachverfolgungsaufforderungen wie diese können verwendet werden, um zusätzliche Einblicke zu erhalten, aber Sie sollten Keine Eingabeaufforderungen vermeiden, die von Ihrem Ziel abweichen. Das Side-Tracking der Chatunterhaltung kann die Antworten von GitHub Copilot beeinflussen. Ein sauberer Chatverlauf ist wichtig.

1. Nehmen Sie sich ein paar Minuten Zeit, um den Umgestaltungsplan von GitHub Copilot zu überprüfen.

    GitHub Copilot sollte eine klare Gliederung bereitstellen, die zeigt, wie die ProcessOrder-Methode von einer großen monolithischen Methode in eine Reihe kleinerer, fokussierter Methodenaufrufe transformiert werden kann. Dieser Plan sollte die vorhandene Geschäftslogik beibehalten und gleichzeitig die Codestruktur und Lesbarkeit verbessern.

    Die Antwort sollte Folgendes enthalten:
    - Ein Fluss auf hoher Ebene, der die Hauptschritte als separate Methodenaufrufe anzeigt.
    - Vorgeschlagene Methodennamen und Signaturen für die extrahierten Methoden.
    - Anleitung zur konsistenten Behandlung von Fehlern über Methoden hinweg.
    - Erläuterungen dazu, wie die umgestaltete Struktur die Verhaltbarkeit verbessert.

1. Bitten Sie um weitere Anleitungen zu Fehlerbehandlungsmustern.

    Das Verständnis des Fehlerbehandlungsprozesses ist entscheidend für die Aufrechterhaltung des vorhandenen Verhaltens, wenn Sie die ProcessOrder-Methode umgestalten. Sie können GitHub Copilot die aktuelle Fehlerbehandlungsstrategie analysieren und eine Möglichkeit vorschlagen, das vorhandene Verhalten aufrechtzuerhalten oder zu verbessern.

    Zum Beispiel:

    ```text
    In the current ProcessOrder method, there are multiple error scenarios with specific cleanup procedures (like releasing inventory on payment failure). In the refactored version, how should I handle errors consistently across the extracted methods? Should each method return an OrderResult object, throw exceptions, or use another pattern to maintain the existing error handling behavior?
    ```

1. Nehmen Sie sich ein paar Minuten Zeit, um die Empfehlungen zur Fehlerbehandlung zu überprüfen.

    GitHub Copilot sollte Anleitungen zur Aufrechterhaltung konsistenter Fehlerbehandlungsmuster in den umgestalteten Methoden bereitstellen. Diese Anleitung ist wichtig, da die aktuelle Methode komplexe Fehlerbehandlungen mit Rollbackprozeduren aufweist, die beibehalten werden müssen.

    Die Empfehlungen sollten folgendes ansprechen:
    - Wie Sie das aktuelle Rollbackverhalten beibehalten (z. B. das Freigeben des Inventars bei Zahlungsfehlern).
    - Gibt an, ob Rückgabewerte, Ausnahmen oder Ergebnisobjekte für die Fehlersignalisierung verwendet werden sollen.
    - So bewahren Sie die Überwachungsprotokollierung während der umgestalteten Methoden auf.
    - Möglichkeiten, um sicherzustellen, dass Bereinigungsprozeduren weiterhin in Fehlerszenarien ausgeführt werden.

Der Ask-Modus von GitHub Copilot zeichnet sich durch die Analyse komplexer Codestrukturen und die Bereitstellung strategischer Anleitungen für die Umgestaltung aus. Die Erkenntnisse aus dieser Analyse informieren den spezifischen Umgestaltungsansatz, den Sie im nächsten Abschnitt implementieren, um sicherzustellen, dass Sie die Geschäftslogikintegrität beibehalten und gleichzeitig eine bessere Codeorganisation erreichen.

### Umgestalten großer Funktionen mithilfe von GitHub Copilot Chat (Agent-Modus)

Der Agentmodus ermöglicht ihnen das Zuweisen komplexer Codeumgestaltungsaufgaben zu GitHub Copilot. Die zugewiesenen Aufgaben können das Erstellen und/oder Aktualisieren mehrerer Dateien umfassen. GitHub Copilot Agent verarbeitet Aufgaben autonom, Test- und Debuggingupdates während der Funktionsweise und informiert Sie, indem Sie ihren Fortschritt in der Chatansicht melden.

In dieser Aufgabe verwenden Sie GitHub Copilot Agent, um die ProcessOrder-Methode systematisch umzugestalten, indem Sie kleinere, fokussierte Methoden extrahieren und dabei die vorhandene Geschäftslogik und das Fehlerbehandlungsverhalten beibehalten.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Stellen Sie sicher, dass die GitHub Copilot-Chatansicht in Visual Studio Code geöffnet ist.

1. Wählen Sie in der Chatansicht den **Agentmodus** aus.

    Das **Dropdownmenü "Modus festlegen"** befindet sich in der unteren linken Ecke der Chatansicht. Im **Agent-Modus** verarbeitet GitHub Copilot seine zugewiesenen Aufgaben (Ihre Eingabeaufforderungen) autonom.

1. Nehmen Sie sich eine Minute Zeit, um Ihre Umgestaltungsstrategie zu berücksichtigen.

    Verwenden Sie die Analyse aus dem vorherigen Vorgang, um eine Strategie zum Umgestalten der ProcessOrder-Methode zu formulieren. Ihr Ansatz sollte inkrementelle Tests unterstützen.

    Betrachten Sie z. B. diese phasenweise Umgestaltungsstrategie:

    - **Phase 1**: Erstellen Sie Stubmethoden innerhalb der OrderProcessor-Klasse.
    - **Phase 2**: Extrahieren Sie Eingabeüberprüfungs- und Sicherheitsbewertungslogik.
    - **Phase 3**: Extrahieren von Bestandsverwaltungsvorgängen (Überprüfung und Reservierung).
    - **Phase 4**: Extrahieren Sie die Zahlungsverarbeitung mit Betrugserkennung und Fehlerbehandlung.
    - **Phase 5**: Extrahieren Sie die Versandkoordination und das Tracking-Management.
    - **Phase 6**: Extrahieren Sie Benachrichtigungs- und Kommunikationslogik.
    - **Phase 7**: Extrahieren Sie die Prozeduren zum Abschließen der Reihenfolge und zum Abschluss.

    Dieser phasenweise Ansatz stellt sicher, dass Änderungen überschaubar sind und Updates inkrementell getestet werden können. Der umgestaltete Code sollte dieselbe Geschäftslogik und Fehlerbehandlung wie die ursprüngliche Methode beibehalten.

1. Scrollen Sie im Code-Editor nach unten in der OrderProcessor-Klasse, und erstellen Sie dann den folgenden Codekommentar nach der schließenden geschweiften Klammer der ProcessOrder-Methode:

    ```csharp

        }
    
        // Add stub methods here
        
    }

    ```

    Der Codekommentar sollte sich nach der endgültigen schließenden Klammer der ProcessOrder-Methode und vor der schließenden Klammer der OrderProcessor-Klasse befinden.

    Sie können GitHub Copilot anweisen, diesen Speicherort zu verwenden, wenn er die neuen Einzelzweckmethoden innerhalb der OrderProcessor-Klasse erstellt.

1. Bitten Sie GitHub Copilot Agent, Stubmethoden zu erstellen, die zum Speichern des extrahierten Codes verwendet werden können.

    Zum Beispiel:

    ```text
    Review the current conversation. I want to start by creating stub code for the new single-purpose methods that will be used when refactoring the ProcessOrder method. Use the method declarations that you proposed in this conversation. Create the new stub methods below the "Add stub methods here" comment in the OrderProcessor class. Ensure that you're using appropriate method parameters and return types. Do not extract any code from the ProcessOrder method, just create the stub methods. After the stub methods are created, open the terminal, navigate to the "ECommerceOrderProcessing/src/ECommerce.Console" directory, then run a "dotnet build" command. Ensure that there are no build errors.
    ```

    Durch das Erstellen der Stubmethoden wird zunächst sichergestellt, dass die neuen Methoden ordnungsgemäß definiert und in die vorhandene Codestruktur integriert sind. Dieser Ansatz ermöglicht inkrementelle Tests und Überprüfungen der Funktionalität der einzelnen Methoden, bevor der Code vollständig aus ProcessOrder extrahiert wird.

1. Überwachen Sie den Fortschritt des Agenten, und stellen Sie bei Bedarf Unterstützung bereit.

    GitHub Copilot Agent erstellt die neuen Methoden am angegebenen Speicherort und fordert dann die Berechtigung zum Ausführen eines Buildbefehls im Terminal auf. Wählen Sie die **Schaltfläche "Weiter"** aus, wenn Sie dazu aufgefordert werden (damit der Agent fortfahren kann).

    Wenn ein Problem auftritt, sollte der Agent Sie benachrichtigen und dann automatisch versuchen, das Problem zu beheben. Geben Sie bei Bedarf weiterhin Unterstützung an.

    Nach dem Ausführen der Buildaufgabe sollte der Agent Sie darüber informieren, dass die neuen Methoden ordnungsgemäß definiert sind und dass keine Syntaxfehler vorhanden sind.

1. Um die Bearbeitungen zu akzeptieren, wählen Sie **"Beibehalten" aus**.

    Sie können Bearbeitungen einzeln im Code-Editor oder auf einmal in der GitHub Copilot-Chatschnittstelle annehmen (oder ablehnen).

1. Bitten Sie GitHub Copilot Agent, die ProcessOrder-Methode umzugestalten.

    Das Umgestalten großer Methoden funktioniert am besten, wenn Sie die Aufgabe in verwaltbare Phasen unterteilen können. In diesem Fall richten sich die Phasen an den bereits identifizierten Einzelprozessmethoden aus. Der gleiche Ansatz sollte angewendet werden, wenn ein Agent zum Umgestalten des Codes für Sie verwendet wird. Schreiben Sie eine Aufgabe, die den Agent anweist, jeweils einen Abschnitt umzugestalten, und testen Sie dann die Updates, bevor Sie zum nächsten Abschnitt wechseln.

    Die Arbeit mit GitHub Copilot Agent kann jedoch wie ein Entwickler verfügbar sein, der unabhängig an einer Reihe von Aufgaben arbeiten kann. In diesem Fall besteht die Reihe von Zuordnungen darin, jeden Codeabschnitt umzugestalten und die Aktualisierungen zu testen, bevor sie zum nächsten Abschnitt wechseln. Mit anderen Worten, Sie können eine einzelne Aufgabe (Eingabeaufforderung) schreiben, die GitHub Copilot Agent auffordert, jeden Codeabschnitt umzugestalten, und jede der Einzelzweckmethoden zu testen, bevor sie zum Umgestalten des nächsten Abschnitts wechselt.

    Zum Beispiel:

    ```text
    Review the current conversation. Examine the ProcessOrder method and identify the code sections that should be extracted into the single-purpose stub methods that you already created. Move the identified code sections into the associated single-purpose stub methods, constructing and testing the methods in the suggested order. Replace the extracted code sections with a call to the associated single-purpose method. Use local variables of the associated return value type to ensure that the ProcessOrder method maintains the same error handling behavior that's provided by the original code. As each method is updated, use a "dotnet run" command to ensure that the code features and error handling processes work correctly (including rollback features, like releasing inventory on payment failure). Also verify that the four test case scenarios generate the expected console output when the app is run (all test cases should pass). Continue extracting code into the new single-purpose methods (and testing the app) until all methods are complete and the application generates the expected console output for the four test case scenarios. Don't stop working on this task until all methods are constructed and tested. Display the step-by-step approach that you'll use to complete this task and then begin.
    ```

    > **HINWEIS:** Wenn Sie an Produktionscode arbeiten, ist es wichtig, den Code nach erheblichen Umgestaltungsvorgängen gründlich zu testen. Dies umfasst das Erstellen und Testen der Anwendung, um zu überprüfen, ob Features wie beabsichtigt funktionieren, Komponententests bestehen, und die Ausgabe bleibt mit dem ursprünglichen Verhalten konsistent. Um Zeit während dieser Schulungsübung zu sparen, verlassen wir uns auf den Agent, um inkrementelle Tests durchzuführen. Sie führen einen zusätzlichen Test (manuelle Überprüfung) aus, nachdem die Codeumgestaltungsaufgaben abgeschlossen wurden.

1. Überwachen Sie den Fortschritt des Agenten, und stellen Sie bei Bedarf Unterstützung bereit.

    GitHub Copilot Agent sollte zunächst seinen Plan für die Umgestaltung jedes Abschnitts der ProcessOrder-Methode beschreiben. Der Plan sollte einen schrittweisen Ansatz für jeden Codeabschnitt enthalten, der Folgendes umfasst: Verschieben von Code aus der ProcessOrder-Methode in die entsprechende Einzelprozessmethode, Ersetzen des extrahierten Codes in ProcessOrder durch einen Methodenaufruf und Testen der App, um sicherzustellen, dass der umgestaltete Code wie beabsichtigt funktioniert.

    Der Agent stellt außerdem Updates in der Chatansicht bereit, die den Fortschritt beschreiben, einschließlich aller auftretenden Probleme. Sie können mit dem Agent interagieren, um Anweisungen zu klären oder bei Bedarf zusätzlichen Kontext bereitzustellen.

    GitHub Copilot Agent fordert in der Regel die Berechtigung zum Erstellen oder Ausführen der Anwendung während des Umgestaltungsprozesses auf. Wählen Sie in der Chatansicht die **Schaltfläche "Weiter** " aus, damit der Agent fortfahren kann.

    > **WICHTIG:** Wenn GitHub Copilot Agent die Verarbeitung der zugewiesenen Aufgabe beendet, bevor alle Abschnitte in der ProcessOrder-Methode umgestaltet werden, geben Sie eine Eingabeaufforderung ein, die dem Agent mitteilt, mit der Umgestaltungsaufgabe fortzufahren.

1. Nachdem der Umgestaltungsprozess abgeschlossen ist, akzeptieren Sie die Änderungen.

    Wählen Sie in der Chatansicht die **Schaltfläche "Beibehalten** " aus, um alle vom Agent vorgenommenen Änderungen anzunehmen.

1. Nehmen Sie sich eine Minute Zeit, um die aktualisierte OrderProcessor-Klasse zu überprüfen.

    Nachdem der Agent seine Umgestaltungsaufgaben abgeschlossen hat, sollte die OrderProcessor-Klasse mehrere kleinere, fokussierte Methoden enthalten, die bestimmte Aspekte der Auftragsverarbeitung behandeln. Die ProcessOrder-Methode sollte deutlich kürzer und lesbarer sein, wobei jeder Schritt des Auftragsverarbeitungsworkflows in seiner eigenen Methode klar definiert ist.

    Die aktualisierte ProcessOrder-Methode sollte z. B. wie folgt aussehen:

    ```csharp
    public OrderResult ProcessOrder(Order order)
    {
        // Log the start of order processing for audit trail
        _auditLogger.LogOrderProcessingStarted(order.Id, order.CustomerEmail);

        try
        {
            // Validate order and perform security checks
            if (!ValidateOrderAndSecurity(order, out string? validationFailure))
            {
                return OrderResult.Failure(validationFailure ?? "Validation failed for unknown reasons");
            }

            Console.WriteLine($"Processing Order {order.Id} for {_securityValidator.MaskEmail(order.CustomerEmail)}...");
            Console.WriteLine($"Order contains {order.Items.Count} items, Total: ${order.TotalAmount:F2}");

            // Check inventory and reserve stock
            if (!CheckAndReserveInventory(order, out string? inventoryFailure))
            {
                return OrderResult.Failure(inventoryFailure ?? "Inventory check failed for unknown reasons");
            }
            Console.WriteLine("Inventory reserved successfully.");
            _auditLogger.LogInventoryReserved(order.Id, order.Items.Count);

            // Payment Processing with Enhanced Security
            Console.WriteLine("Processing payment...");
            // Process payment
            if (!ProcessPayment(order, out string? paymentFailure))
            {
                return OrderResult.Failure(paymentFailure ?? "Payment processing failed for unknown reasons");
            }

            // Shipping and Logistics Management
            Console.WriteLine("Scheduling shipping...");
            // Schedule shipping
            if (!ScheduleShipping(order, out string? shippingFailure))
            {
                return OrderResult.Failure(shippingFailure ?? "Shipping scheduling failed for unknown reasons");
            }

            // Customer Communication and Notifications
            Console.WriteLine("Sending notifications...");
            // Send notifications
            SendNotifications(order);

            // Order Finalization and Data Recording
            Console.WriteLine("Finalizing order...");
            order.Status = OrderStatus.Completed;
            order.CompletionDate = DateTime.UtcNow;
            order.ProcessingDuration = DateTime.UtcNow - order.OrderDate;

            // In a real app, this would update the order record in a database
            // _orderRepository.UpdateOrder(order);

            Console.WriteLine($"Order {order.Id} completed successfully in {order.ProcessingDuration.TotalSeconds:F1} seconds.");
            _auditLogger.LogOrderCompleted(order.Id, order.TotalAmount);

            // Finalize the order
            FinalizeOrder(order);

            return OrderResult.Success(order.Id, order.TrackingNumber ?? "");
        }
        catch (Exception ex)
        {
            HandleUnexpectedError(order, ex);
            return OrderResult.Failure("An unexpected error occurred during order processing");
        }
    }

    ```

GitHub Copilot Agent zeichnet sich bei systematischen Umgestaltungsaufgaben aus, die ein Verständnis von Codefluss-, Geschäftslogik- und Fehlerbehandlungsmustern erfordern. Indem Sie die Umgestaltung in logische Phasen aufteilen, stellen Sie sicher, dass jede Änderung verwaltbar, testbar ist und das ursprüngliche Systemverhalten aufrecht erhält und gleichzeitig die Codeorganisation und -wartung erheblich verbessert.

### Testen des umgestalteten E-Commerce-Auftragsverarbeitungscodes

Manuelle Tests und Überprüfungen stellen sicher, dass Ihr umgestalterter Code die beabsichtigte Geschäftslogik und -funktionalität verwaltet. Ein erfolgreicher Umgestaltungsprozess sollte die Codestruktur verbessern und gleichzeitig identisches Verhalten mit der ursprünglichen Implementierung erzeugen.

In dieser Aufgabe testen Sie den umgestalteten Code, um zu überprüfen, ob die gesamte Geschäftslogik beibehalten wird und die Lesbarkeit und Wartung von Code verbessert wird.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Führen Sie die umgestaltete Anwendung aus, und überprüfen Sie das erwartete Verhalten.

    Vergleichen Sie die Ausgabe mit dem Verhalten, das Sie vor der Umgestaltung beobachtet haben. Die Konsolenausgabe sollte identisch sein, einschließlich:

    - **Test 1 (Gültige Bestellung)**: Sollte erfolgreich mit zahlungsabwicklung, Versandplanung und Benachrichtigungen abgeschlossen werden
    - **Test 2 (Ungültige E-Mail)**: Sollte die Überprüfung mit derselben Fehlermeldung fehlschlagen
    - **Test 3 (Abgelehnte Zahlung)**: Sollte die Zahlungsverarbeitung fehlschlagen und bestandsrollback auslösen
    - **Test 4 (Verdächtige Reihenfolge)**: Sollte von der Sicherheitsbewertung gekennzeichnet und abgelehnt werden

    Der umgestaltete Code sollte genau die gleichen Ergebnisse erzeugen, was zeigt, dass die Geschäftslogik während des gesamten Umgestaltungsprozesses beibehalten wurde.

1. Erstellen und testen Sie weitere Edgefallszenarios, um die Stabilität zu gewährleisten.

    Erstellen Sie zusätzliche Testszenarios, um zu überprüfen, ob die Fehlerbehandlung in verschiedenen Edgefällen weiterhin ordnungsgemäß funktioniert. Sie können die Testfälle in **Program.cs** vorübergehend ändern, um andere Szenarios zu testen.

    Sie können z. B. den folgenden Codeausschnitt vor dem Code hinzufügen, der die Testzusammenfassung anzeigt:

    ```csharp
    // Test with empty items list (should fail validation)
    System.Console.WriteLine("\n--- Test Case 5: Empty Order ---");
    var emptyOrder = CreateSampleOrder("ORD-EMPTY", "test@example.com", "123 Test St",
        new List<OrderItem>(),
        new PaymentInfo { CardNumber = "4111111111111111", CardCVV = "123", CardHolderName = "Test User", ExpiryMonth = "12", ExpiryYear = "2025", BillingAddress = "123 Test St" });

    var result5 = processor.ProcessOrder(emptyOrder);
    testResults.Add($"Test 5: {(result5.IsSuccess ? "FAILED" : "PASSED")} - Should reject empty order");

    // Test with invalid shipping address (should fail validation)
    System.Console.WriteLine("\n--- Test Case 6: Invalid Shipping Address ---");
    var invalidAddressOrder = CreateSampleOrder("ORD-ADDR", "user@example.com", "",
        new List<OrderItem> { new() { ProductId = "BOOK-001", Quantity = 1, Price = 15.99m } },
        new PaymentInfo { CardNumber = "4111111111111111", CardCVV = "123", CardHolderName = "Test User", ExpiryMonth = "12", ExpiryYear = "2025", BillingAddress = "123 Test St" });

    var result6 = processor.ProcessOrder(invalidAddressOrder);
    testResults.Add($"Test 6: {(result6.IsSuccess ? "FAILED" : "PASSED")} - Should reject invalid shipping address");
    ```

    Diese zusätzlichen Tests helfen sicherzustellen, dass die umgestaltete Überprüfungslogik Edgefälle korrekt verarbeitet und Fehlermeldungen mit der ursprünglichen Implementierung konsistent bleiben.

1. Ausführen der Anwendung und Überprüfen der Ergebnisse

    Wenn Sie die Anwendung ausführen, sollten die Testergebnisse in der Konsole angezeigt werden, die angeben, ob jeder Testfall bestanden oder fehlgeschlagen ist. Achten Sie auf alle Fehlermeldungen oder Protokolle, die während der Testausführung generiert werden.

    Wenn Sie beispielsweise die oben aufgeführten Szenarios „Test 5“ und „Test 6“ hinzugefügt haben, sollte die neue Testausgabe und die aktualisierte Zusammenfassung dem folgenden Beispiel ähneln:

    ```text

    --- Test Case 5: Empty Order ---
    [AUDIT] 2025-08-20 18:28:11.099 UTC | ORDER_PROCESSING_STARTED | Order: ORD-EMPTY | Started processing order for t***@example.com
    [AUDIT] 2025-08-20 18:28:11.100 UTC | VALIDATION_FAILURE | Order: ORD-EMPTY | Empty order items
    
    --- Test Case 6: Invalid Shipping Address ---
    [AUDIT] 2025-08-20 18:28:11.101 UTC | ORDER_PROCESSING_STARTED | Order: ORD-ADDR | Started processing order for u***@example.com
    [AUDIT] 2025-08-20 18:28:11.101 UTC | VALIDATION_FAILURE | Order: ORD-ADDR | Invalid shipping address
    
    === TEST SUMMARY ===
    Test 1: PASSED - ORD-001
    Test 2: PASSED - Should reject invalid email
    Test 3: PASSED - Should reject declined payment
    Test 4: PASSED - Should flag suspicious order
    Test 5: PASSED - Should reject empty order
    Test 6: PASSED - Should reject invalid shipping address

    ```

1. Führen Sie die Anwendung erneut aus, um zu überprüfen, ob die Überwachungsprotokollierung weiterhin ordnungsgemäß funktioniert.

    Überprüfen Sie die **order_audit_log.txt** Datei, um sicherzustellen, dass die Überwachungsprotokollierung während der umgestalteten Methoden weiterhin ordnungsgemäß funktioniert. Die neuesten Ereignisse befinden sich am Ende der Datei.

    Der Überwachungspfad sollte abgeschlossen sein und nachweisen, dass die Protokollierung über alle extrahierten Methoden hinweg beibehalten wird.

    > **TIPP**: Die order_audit_log.txt Datei wird im aktuellen Arbeitsverzeichnis der Anwendung erstellt/aktualisiert. Je nachdem, wie Sie das ECommerce.Console-Projekt ausführen, könnte das Arbeitsverzeichnis das Verzeichnis "src/ECommerce.Console/bin/Debug/net9.0" anstelle des Verzeichnisses "src/ECommerce.Console" sein. Um die Überwachungsdatei im Verzeichnis "src/ECommerce.Console" zu generieren, führen Sie die Anwendung über das Terminal mit einem .NET CLI-Befehl aus.

    Die folgenden Ereignistypen können in der Überwachungsprotokolldatei der Reihenfolge gespeichert werden:

    - Bestellverarbeitungsereignisse:
        - LogOrderProcessingStarted(string orderId, string email)
        - LogOrderCompleted(string orderId, Dezimalbetrag)
    - security-events:
        - LogSecurityEvent(string eventType, Zeichenfolgendetails)
    - Validierungsereignisse:
        - LogValidationFailure(string orderId, Zeichenfolgengrund)
    - Bestandsereignisse:
        - LogInventoryIssue(string orderId, string productId, string issue)
        - LogInventoryReserved(string orderId, int itemCount)
    - Zahlungsereignisse:
        - LogPaymentProcessed(string orderId, Dezimalbetrag, Zeichenfolgenverweis)
        - LogPaymentFailure(string orderId, Zeichenfolgengrund)
    - Versandereignisse:
        - LogShippingScheduled(string orderId, string trackingNumber)
        - LogShippingFailure(string orderId, Zeichenfolgengrund)
    - Benachrichtigungsereignisse
        - LogNotificationSent(string orderId, string type)
        - LogNotificationFailure(string orderId, Zeichenfolgengrund)
    - Unerwartete Fehler.
        - LogUnexpectedError(string orderId, Zeichenfolgenfehler)

Manuelle Tests stellen sicher, dass Ihre Umgestaltungsbemühungen das Ziel erreicht haben, die Codestruktur zu verbessern und gleichzeitig die Systemfunktionalität aufrechtzuerhalten. Der umgestaltete Code bietet jetzt eine viel besser verwendbare Grundlage, in der jede Methode eine klare, fokussierte Zuständigkeit hat, um zukünftige Verbesserungen und Fehlerbehebungen einfacher zu implementieren.

## Zusammenfassung

In dieser Übung haben Sie gelernt, wie Sie GitHub Copilot verwenden, um große Funktionen in einer Anwendung umzugestalten. Sie haben das E-Commerce Order Processing System untersucht, große Funktionen identifiziert, die eine Umgestaltung benötigten, und GitHub Copilot verwendet, um monolithische Methoden in kleinere, fokussiertere Funktionen zu zerlegen, um die Wartung und Lesbarkeit zu verbessern.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich kurz Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder GitHub Copilot-Abonnement vorgenommen haben, die Sie nicht beibehalten möchten. Wenn Sie Änderungen vorgenommen haben, setzen Sie sie nach Bedarf zurück. Wenn Sie einen lokalen PC als Lab-Umgebung verwenden, können Sie den Beispielprojektordner archivieren oder löschen, den Sie für diese Übung erstellt haben.
