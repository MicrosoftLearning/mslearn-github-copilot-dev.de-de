---
lab:
  title: 'Übung: Vereinfachen komplexer Bedingungen mithilfe von GitHub Copilot'
  description: 'Erfahren Sie, wie Sie komplexe bedingte Logik in C#-Codebasen mithilfe von GitHub Copilot-Tools umgestalten.'
---

# Vereinfachen komplexer Bedingungen mithilfe von GitHub Copilot

Die bedingte Logik in Geschäftsanwendungen wird oft komplexer und tief verschachtelter im Laufe der Zeit, wodurch der Code schwer zu lesen, zu verwalten und zu testen ist. Leider kann die gleiche Komplexität, die die Verwaltung des Codes erschwert, auch die Umgestaltung erschweren. Die Schwierigkeit steigt, wenn der Code eng mit der Geschäftslogik gekoppelt ist.

In dieser Übung verwenden Sie GitHub Copilot, um Code mit tief verschachtelter Logik zu analysieren, die Codelogik umzugestalten und dann den umgestalteten Code zu testen und so sicherzustellen, dass er wie beabsichtigt funktioniert. Sie verwenden GitHub Copilot im Fragemodus, um ein Verständnis des Codes zu erhalten und Optionen zu erkunden, die die Logik vereinfachen. Sie verwenden GitHub Copilot im Agent-Modus, um den Code umzugestalten, indem Sie komplexe bedingte Logik in kleinere, fokussierte Hilfsmethoden extrahieren und die Schachtelung reduzieren. Die Vereinfachung komplexer Bedingungen erleichtert das Lesen, Warten und Testen des Codes.

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

### Herunterladen von Beispielcodeprojekten

Führen Sie die folgenden Schritte aus, um die Beispielprojekte herunterzuladen und in Visual Studio Code zu öffnen:

1. Öffnen Sie ein Browserfenster in Ihrer Übungsumgebung.

1. Um eine ZIP-Datei mit den Beispiel-App-Projekten herunterzuladen, öffnen Sie die folgende URL in Ihrem Browser: [GitHub Copilot-Übung – Entwickeln von Codefeatures](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/GHCopilotEx9LabApps.zip)

    Die ZIP-Datei heißt **GHCopilotEx9LabApps.zip**.

1. Extrahieren Sie die Dateien aus der Datei **GHCopilotEx9LabApps.zip**.

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner mit Downloads in Ihrer Übungsumgebung.

    1. Klicken Sie mit der rechten Maustaste auf **GHCopilotEx9LabApps.zip** und wählen Sie dann **Alle extrahieren** aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Kopieren Sie den Ordner **GHCopilotEx9LabApps** an einen leicht zugänglichen Speicherort, z. B. Ihren Windows-Ordner „Desktop“.

1. Öffnen Sie den Ordner **GHCopilotEx9LabApps** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Lab-Umgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows-Ordner „Desktop“, und wählen Sie **GHCopilotEx9LabApps** und dann **Ordner auswählen** aus.

1. Überprüfen Sie in der PROJEKTMAPPEN-EXPLORER-Ansicht von Visual Studio Code die folgende Lösungstruktur:

    - GHCopilotEx9LabApps\
        - ECommercePricingEngine\
            - Dependencies\
            - ECommercePricingDemo.cs
            - Output-ECommercePricingEngine.txt
            - SecurityTest.cs
        - LoanApprovalWorkflow\
            - Dependencies\
            - LoanApprovalDemo.cs
            - Output-LoanApprovalWorkflow.txt
            - SecurityTest.cs

## Übungsszenario

Sie sind Softwareentwicklerin bzw. Softwareentwickler und arbeiten für eine Beratungsfirma. Ihre Kundschaften benötigen Hilfe beim Umgestalten komplexer bedingter Logik, um die Lesbarkeit und Wartung von Code zu verbessern. Sie werden den folgenden Apps zugewiesen:

- E-Commerce-Preismodul: Die erste App ist ein E-Commerce-Preismodul, das dynamische Preise basierend auf verschiedenen Geschäftsregeln berechnet. Bedingungen umfassen Mitgliedschaftsstufen, Bestellwerte, Coupon-Codes, Produktkategorien und Versandregeln.
- Workflow zur Genehmigung von Krediten: Die zweite App ist ein Workflow zur Genehmigung von Krediten, der Kreditanträge basierend auf verschiedenen Faktoren auswertet. Zu den Bedingungen gehören Einkommen, Beschäftigungsstatus, Schuldenquote, Sicherheiten und Kredithistorie.

Diese Übung umfasst die folgenden Aufgaben:

1. Überprüfen Sie die Codebasis des E-Commerce-Preismoduls.
1. Identifizieren Sie die Umgestaltungsmöglichkeiten im Code des E-Commerce-Preismoduls mithilfe von GitHub Copilot.
1. Gestalten Sie den Code des E-Commerce-Preismoduls mithilfe von GitHub Copilot-Agent um.
1. Testen Sie den umgestalteten Code des E-Commerce-Preismoduls.
1. (OPTIONAL) Vereinfachen Sie komplexe Bedingungen in der Demo-App „LoanApprovalWorkflow“

### Überprüfen der Codebasis des E-Commerce-Preismoduls

Der erste Schritt bei jeder Umgestaltung besteht darin, sicherzustellen, dass Sie die vorhandene Codebasis verstehen.

In dieser Aufgabe öffnen Sie das E-Commerce-Preismodul-Projekt und verwenden GitHub Copilot, um die komplexe bedingte Logik zu analysieren.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Stellen Sie sicher, dass der Ordner „GHCopilotEx9LabApps“ in Visual Studio Code geöffnet ist.

    Lesen Sie den Abschnitt **Vorbereitung**, wenn Sie die Beispielcodeprojekte nicht heruntergeladen haben.

1. Überprüfen Sie, ob das Codeprojekt **ECommercePricingEngine** erfolgreich erstellt wird.

    Klicken Sie beispielsweise in der PROJEKTMAPPEN-EXPLORER-Ansicht mit der rechten Maustaste auf **ECommercePricingEngine** und wählen Sie dann **Erstellen** aus.

    Es werden Warnungen angezeigt: „Cannot convert null literal to non-nullable reference type.“, wenn Sie das Projekt erstellen, aber es sollten keine Fehler auftreten. Sie können die Warnungen im Rahmen dieser Übung ignorieren.

1. Öffnen Sie die Chat-Ansicht von GitHub Copilot.

    Wenn die Chat-Ansicht noch nicht geöffnet ist, können Sie sie öffnen, indem Sie das **Chatsymbol** oben im Visual Studio Code-Fenster rechts neben dem Suchtextfeld auswählen.

1. Stellen Sie in der Chat-ansicht sicher, dass der Chat-Modus auf **Fragemodus** festgelegt ist und das Modell auf **GPT-4.1**.

    Diese Einstellungen sind in der unteren linken Ecke der Chat-Ansicht verfügbar. Der **Fragemodus** von GitHub Copilot wird verwendet, um allgemeine Codierungsfragen zu stellen und codebezogene Erklärungen zu generieren. Das Modell **GPT-4.1**, das im GitHub Copilot Free-Plan enthalten ist, ist eine gute Wahl für Codeanalyse, Erklärungen und Anleitungen im Zusammenhang mit der Codeumgestaltung.

    Sie verwenden den **Agent-Modus** von GitHub Copilot später in dieser Übung, aber jetzt verwenden Sie den **Fragemodus** für Codeanalyse und Erklärungen.

    > [!NOTE]
    > Einige Modelle eignen sich besser für bestimmte Aufgaben als andere. Das ausgewählte Modell kann sich auf die von GitHub Copilot generierten Antworten auswirken. Nachdem Sie diese Übung mit den empfohlenen Einstellungen abgeschlossen haben, sollten Sie die Übung mit verschiedenen Modellen wiederholen und die Ergebnisse vergleichen.

1. Öffnen Sie die Datei **ECommercePricingDemo.cs** in Visual Studio Code.

    Diese Datei enthält die folgenden Klassen:

    - Benutzer: Stellt eine Kundin bzw. einen Kunden mit Eigenschaften für Mitgliedschaftsebene, Kaufverlauf und besondere Status (Schülerin/Schüler, Mitarbeiterin/Mitarbeiter, Unternehmen usw.) dar. Wird verwendet, um die Berechtigung für verschiedene Rabatte und Vorteile zu ermitteln.
    - Coupon: Stellt einen Rabatt oder Versandgutschein mit Eigenschaften für Code, Gültigkeit, Typ (Prozent oder Versand) und Wert dar. Wird bei Preisberechnungen verwendet, um zusätzliche Rabatte oder kostenlosen Versand anzuwenden.
    - Artikel: Stellt ein Produkt in einer Bestellung mit Name, Kategorie und Preis dar. Wird verwendet, um Bestellungen zu erstellen und Teilergebnisse und kategoriespezifische Rabatte zu berechnen.
    - Auftrag: Stellt die Bestellung einer Kundin bzw. eines Kunden dar, die eine Liste der Artikel, Versandregion, Coupon, Ereignis, Zahlungsmethode und andere bestellspezifische Kennzeichnungen enthält. Stellt Methoden zum Berechnen von Teilergebnissen bereit, sucht nach dem Vorhandensein der Kategorie und bestimmt die Reihenfolgemerkmale (z. B. „Hoher Wert“, „Gemischte Kategorien“).
    - PricingEngine: Enthält die Hauptlogik zum Berechnen des Endpreises einer Bestellung. Wendet Rabatte basierend auf Benutzerstatus, Bestelldetails, Coupons und kategoriespezifischen Regeln an. Übernimmt Sicherheitsprüfungen und stellt sicher, dass Rabatte und Preise in sicheren Grenzen bleiben.
    - Program: Der Einstiegspunkt. Erstellt Testbenutzende, Coupons und Bestellungen und führt dann eine Reihe komplexer Preisszenarien mithilfe der oben genannten Klassen aus. Veranschaulicht, wie das Preismodul seine Logik in verschiedenen Situationen anwendet.

    Jede Klasse modelliert eine reale Entität oder einen Prozess in einem E-Commerce-Preissystem und interagiert in der Klasse „Programm“, um Preisberechnungen zu simulieren und zu testen. Beispielsweise werden die Instanzen „User“, „Order“ und „Coupon“ an „PricingEngine.CalculateFinalPrice“ übergeben, um den Endpreis mit allen anwendbaren Rabatten zu berechnen und anzuzeigen.

1. Suchen Sie die Klasse **PricingEngine** und wählen Sie dann die gesamte Methode **CalculateFinalPrice** aus.

    Die Methode „CalculateFinalPrice“ enthält komplexe und tief verschachtelte bedingte Logik, die Mitgliedschaftsstufen, saisonale Ereignisse, Unternehmenskonten, Abonnementdienste und verschiedene Rabattszenarien auswertet.

1. Nehmen Sie sich eine Minute Zeit, um durch die bedingte Logik in der Methode **CalculateFinalPrice** zu scrollen.

    Die Methode ist komplex und schwer zu lesen, mit mehreren verschachtelten Bedingungen, die verschiedene Rabattszenarien behandeln. Die Komplexität ergibt sich aus den verschiedenen Geschäftsregeln, die basierend auf Benutzerstatus, Auftragsdetails und Coupon-Codes angewendet werden müssen.

1. Klicken Sie mit der rechten Maustaste auf den ausgewählten Code, und wählen Sie dann **Copilot** > **Erklären** aus.

    GitHub Copilot analysiert die Methode „CalculateFinalPrice“ und bietet eine detaillierte Erläuterung der Funktionsweise des Codes.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Erklärung von GitHub Copilot zu überprüfen.

    Die Erklärung sollte die wichtigsten Rabattkategorien wie hierarchische Mitgliedschaft, Coupon-Anwendungen, Massenkaufanreize und kategoriespezifische Regeln hervorheben.

    Zum Beispiel:

    ```md
    The CalculateFinalPrice method is a comprehensive pricing engine for an e-commerce scenario. It starts by validating its inputs, ensuring that both the user and order objects are not null and that the order data is valid. This prevents null reference exceptions and guards against invalid or malicious input. The method then calculates the base total of the order and checks that it falls within a reasonable range, aborting the calculation if the total is suspiciously low or high.
    
    Next, the method initializes variables for the discount percentage, shipping cost, and a list to track all applied discounts. The core of the function is a series of nested conditional blocks that determine which discounts the user is eligible for. These are based on membership level (Premium, Gold, Silver), user attributes (such as being a student, employee, or first-time buyer), order characteristics (like high value, bulk purchase, or mixed categories), and special events (such as Black Friday or Back to School). Each eligible discount is added using the SafeAddDiscount helper, which ensures the total discount does not exceed a maximum cap and records a description of the discount.
    
    The method also handles coupon codes, applying either a percentage discount or free shipping, with additional enhancements for certain membership levels or order types. For example, Premium members may receive a boosted coupon value, and further stacking is possible during special events or for corporate accounts.
    
    After all discounts are considered, the method applies additional bulk purchase incentives if the order contains a large number of items. It then enforces a final cap on the total discount to prevent excessive reductions. The final price is calculated using ApplyCategorySpecificDiscounts, which applies category-based discount caps (e.g., electronics discounts are limited to 15%). The shipping cost is added, and the final price is ensured to be above a minimum threshold.
    
    Finally, the method outputs a summary of the calculation, including the base total, all applied discounts, the total discount percentage (with a note about category caps), the shipping cost, and the final price. This approach ensures transparency and traceability in how the final price is determined, while also enforcing business rules and security best practices.
    ```

    Wenn Sie sich Zeit nehmen, um den vorhandenen Code zu verstehen, ist es später in dieser Übung leichter für Sie, die Umgestaltungsoptionen zu erkennen und auszuwählen.

1. Geben Sie in der Chat-Ansicht den folgenden Prompt ein, um eine umfassendere Analyse des Berechnungsprozesses zu erhalten:

    ```plaintext
    @workspace Explain the business logic flow in the CalculateFinalPrice method. What are the different discount paths and how do they interact with each other? What are the key business rules that govern pricing calculations?
    ```

    Diese Analyse sollte Ihnen helfen, zu verstehen, wie die verschiedenen Rabattkategorien interagieren und welche Geschäftsregeln bei jedem Schritt der Preisberechnung angewendet werden.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Erklärung zu überprüfen, die von GitHub Copilot generiert wurde.

    Die Antwort sollte die primären Rabattpfade und ihre Interaktion miteinander identifizieren. Zum Beispiel:

    ```md
    The `CalculateFinalPrice` method in `ECommercePricing.PricingEngine` implements a layered, rule-driven approach to pricing calculation for an e-commerce order. Here’s how the business logic flows and how the discount paths interact:
    
    ### 1. **Input Validation**
    - The method first validates that both `user` and `order` are not null and that the order data is valid (e.g., no negative prices, all required fields present).
    - It checks that the order subtotal is within allowed bounds (greater than zero and less than $1,000,000).
    
    ### 2. **Base Discount Initialization**
    - The method initializes the discount percentage (`discountPercent`) to 0 and calculates the base shipping cost.
    
    ### 3. **Membership-Based Discount Paths**
    - The first major decision point is the user's membership level:
      - **Premium:** Starts with a 15% discount, then applies additional discounts for high-value orders, seasonal events, corporate accounts, subscriptions, loyalty (years as member), lifetime spending, and express shipping. Each condition is nested, so deeper benefits require all previous conditions to be met.
      - **Gold:** Starts with a 12% discount, then adds bonuses for seasonal events, bulk purchases, category diversity, employee status, pre-orders, and alternative payment methods. These are also nested, but less deeply than Premium.
      - **Silver:** Starts with 8%, with further bonuses for students, back-to-school events, bulk purchases, electronics focus, gift wrap, and express shipping. These are nested within the student path.
      - **First-Time Buyer:** If the user is a first-time buyer (and not a member), a 10% discount is applied, with further bonuses for seasonal events, order size, payment method, high-value orders, premium shipping regions, and express shipping.
    
    ### 4. **Coupon Application**
    - If a coupon is present:
      - **Valid Percent Coupon:** The coupon value is capped at 50%. Premium and Gold members get a multiplier (Premium: 1.3x up to 50%, Gold: 1.2x up to 40%). Additional stacking occurs for Premium members on Black Friday, corporate accounts, and bulk orders, with each step further capping the discount.
      - **Valid Shipping Coupon:** Shipping is set to zero for domestic orders or Premium members.
      - **Expired Coupon:** No discount is applied, and a message is logged.
    
    ### 5. **Bulk Purchase Incentives**
    - Additional discounts are applied for orders with 10+ items (5%) or 20+ items (8%).
    
    ### 6. **Discount Capping**
    - The total discount percentage is capped at 95% to prevent excessive reductions.
    
    ### 7. **Category-Specific Discount Rules**
    - The final discount is applied with category-specific caps:
      - **Electronics:** Discount capped at 15%.
      - **Clothing:** Discount capped at 20% (25% during Back-to-School).
      - **Accessories/Other:** Full discount applies.
    
    ### 8. **Final Price Calculation**
    - The final price is the sum of all discounted category subtotals plus shipping, with a minimum enforced price of $0.01.
    
    ### 9. **Result Output**
    - The method prints the base total, all applied discounts, the total discount percentage (with a note about the electronics cap), shipping cost, and the final price.
    
    ---
    
    ## **Discount Path Interactions**
    - **Nesting:** Many discounts are nested, meaning deeper discounts require all previous conditions to be true (e.g., Premium members with high-value orders, during Black Friday, who are also corporate accounts, etc.).
    - **Stacking:** Discounts from different sources (membership, coupons, bulk, etc.) are added together, but always subject to the overall cap.
    - **Category Caps:** Even if the total discount is high, certain categories (like electronics) have stricter caps, so the effective discount for those items may be lower than the overall discount.
    
    ---
    
    ## **Key Business Rules**
    - **Validation:** Orders and users must be valid; otherwise, pricing is aborted.
    - **Membership Drives Discounts:** Higher membership levels unlock deeper and more complex discount paths.
    - **Coupons Are Enhanced by Membership:** Premium and Gold members get more value from percent-off coupons.
    - **Bulk and Seasonal Bonuses:** Large orders and seasonal events can trigger additional discounts.
    - **Category Protection:** Electronics and clothing have maximum discount caps to protect margins.
    - **Shipping Can Be Discounted:** Shipping can be free with certain coupons or for Premium members.
    - **Discount Caps:** No combination of discounts can exceed 95% off the order.
    - **Transparency:** All applied discounts are tracked and displayed for auditability.
    
    For more details, see the full implementation in ECommercePricingDemo.cs, especially the `ECommercePricing.PricingEngine.CalculateFinalPrice` method.
    ```

1. Vergleichen Sie die Erklärung von GitHub Copilot mit Ihren eigenen Beobachtungen der komplexen bedingten Logik in der Methode `CalculateFinalPrice`.

    Sie können die wichtigsten Rabattquellen: Mitgliedschaftsstufen, Coupon-Codes und Massenkaufanreize wahrscheinlich selbst identifizieren. Die Erklärung von GitHub Copilot sollte Ihre Beobachtungen unterstützen und zusätzliche Einblicke darüber liefern, wie diese Rabattpfade interagieren, sowie über die wichtigsten Geschäftsregeln, die die Preisberechnungen steuern.

    - Beachten Sie, wie Rabatte für die verschiedenen Mitgliedschaftsstufen (Premium, Gold, Silver) funktionieren und wie Personen, die zum ersten Mal etwas kaufen, behandelt werden.
    - Beachten Sie, wie die Coupon-Überprüfung ausgewertet und angewendet wird und wie Coupon-Rabatte mit Mitgliedschaftsrabatten interagieren.
    - Beachten Sie, wie volumenbasierte Rabatte basierend auf der Artikelanzahl angewendet werden.

    Geschäftsregeln werden über die verschachtelten Bedingungen erzwungen, um sicherzustellen, dass Rabatte basierend auf Benutzerstatus, Bestelldetails und Coupon-Codes korrekt angewendet werden. Diese Regeln müssen mit dem Umgestaltungsprozess voranschreiten.

1. Führen Sie das Projekt „ECommercePricingEngine“ aus und überprüfen Sie die Ausgabe.

    Die Ausgabe sollte die grundlegenden und ermäßigten Preise für verschiedene Kombinationen von Benutzenden, Bestellungen und Coupons anzeigen. Am Ende dieser Übung muss Ihr umgestalteter Code dieselben Ergebnisse wie der ursprüngliche Code generieren.

    Möglicherweise haben Sie bemerkt, dass die Ausgabe grundlegende Sicherheitstests für ungültige Eingaben und böswillige Versuche zur Manipulation der Preise enthält. Obwohl diese Tests nicht alle möglichen Angriffsvektoren oder die in einer Produktions-App erforderliche Testebene darstellen, dienen sie als Erinnerung, dass die Sicherstellung der Codequalität und -sicherheit eine Voraussetzung ist. Die Datei **SecurityTest.cs** ist Teil des Projekts „ECommercePricingEngine“.

    > [!NOTE]
    > Eine Kopie der Ausgabe finden Sie in der Datei **Output-ECommercePricingEngine.txt**, die im Ordner „ECommercePricingEngine“ enthalten ist. Sie können eine eigene Ausgabedatei erstellen, wenn Sie Ergebnisse vergleichen oder Beispieldaten ändern möchten. Wenn Sie das Ende dieser Übung erreichen, verwenden Sie die Ausgabedatei, um sicherzustellen, dass Ihr umgestalteter Code dieselben Ergebnisse wie der ursprüngliche Code generiert.

    So führen Sie das Projekt aus: Wenn die Datei „ECommercePricingDemo.cs“ im Editor von Visual Studio Code geöffnet ist, können Sie das Projekt ausführen, indem Sie die Schaltfläche „Ausführen“ (Projekt ausführen, das dieser Datei zugeordnet ist) auswählen, die sich in der oberen rechten Ecke des Editor-Bereichs befindet. Um das Projekt aus der PROJEKTMAPPEN-EXPLORER-Ansicht auszuführen, klicken Sie mit der rechten Maustaste auf **ECommercePricingEngine**, wählen Sie **Debuggen** aus und dann **Neue Instanz starten**.

### Identifizieren von Umgestaltungsmöglichkeiten im Code des E-Commerce-Preismoduls mithilfe von GitHub Copilot

GitHub Copilot ist ein hervorragendes Tool zum Analysieren von komplexem Code und zum Identifizieren von Codeumgestaltungsmöglichkeiten.

In dieser Aufgabe verwenden Sie GitHub Copilot, um bestimmte Umgestaltungsmöglichkeiten zu identifizieren und Hilfsmethoden vorzuschlagen, die die komplexen Bedingungen vereinfachen. Sie verwenden Beobachtungen aus der vorherigen Aufgabe, um Prompts für GitHub Copilot zu erstellen.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Stellen Sie sicher, dass die Chat-Ansicht von GitHub Copilot im **Fragemodus** geöffnet ist und das Modell **GPT-4.1** ausgewählt ist.

1. Fügen Sie die Datei **ECommercePricingDemo.cs** per Drag-and-Drop zum Chat-Kontext hinzu.

    Obwohl „ECommercePricingDemo.cs“ bereits im Editor von Visual Studio Code geöffnet ist, animiert das Hinzufügen zum Chat-Kontext GitHub Copilot, die gesamte Codedatei zu analysieren, was zu genaueren Vorschlägen führen kann. Das Hinzufügen relevanter Dateien zum Chat-Kontext ist eine bewährte Methode bei der Verwendung von GitHub Copilot, auch wenn Sie die Tags **@workspace** oder **#codebase** in Ihrem Prompt einschließen.

1. Senden Sie einen Prompt, der GitHub Copilot auffordert, Umgestaltungsmöglichkeiten zu identifizieren, die die Code-Modularität im Zusammenhang mit den wichtigsten Rabattpfaden verbessern.

    Berücksichtigen Sie beim Erstellen des Prompts die folgenden Elemente:

    - Weisen Sie GitHub Copilot an, sich auf die Methode **CalculateFinalPrice** und die verschachtelten Bedingungen zu konzentrieren.
    - Bitten Sie GitHub Copilot, Optionen vorzuschlagen, die komplexe Logik in besser verwaltbare Hilfsmethoden mit Einzelverantwortung zu verschieben.
    - Listen Sie die wichtigsten Rabattpfade auf, die für die Extraktion in Hilfsmethoden berücksichtigt werden sollten.
    - Heben Sie die Bedeutung der Aufrechterhaltung der Geschäftslogik hervor, während Sie die Codestruktur vereinfachen.

    Es ist häufig von Vorteil, wenn GitHub Copilot Codeinteraktionen bei der Analyse Ihres Codes in Betracht zieht. Sie können die Tags **@workspace** oder **#codebase** verwenden, um GitHub Copilot anzuweisen, Ihre gesamte Codebasis in die Analyse einzuschließen.

    Zum Beispiel:

    ```plaintext
    @workspace Analyze the CalculateFinalPrice method and suggest refactoring opportunities. Include options that move the nested conditional logic into more manageable, single-responsibility helper methods. Focus on the main discount paths: membership discounts, coupon discounts, and bulk discounts. Maintain the business logic while simplifying the code structure.
    ```

    GitHub Copilot analysiert die Methode, schlägt spezifische Umgestaltungsmöglichkeiten vor und identifiziert Muster in den verschachtelten Bedingungen, die in Hilfsmethoden extrahiert werden können.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Vorschläge von GitHub Copilot zu überprüfen.

    Die Antwort sollte Möglichkeiten identifizieren, die die Verwaltbarkeit und Modularität von Code verbessern, z. B. das Extrahieren der wichtigsten Rabattpfade in Hilfsmethoden und einen oder mehrere Ansätze zur Reduzierung der Schachtelung.

    Zum Beispiel:

    ```md
    Collecting workspace informationThe `ECommercePricing.PricingEngine.CalculateFinalPrice` method is functionally rich but contains deeply nested conditional logic, especially for membership, coupon, and bulk discounts. This makes the code harder to read, maintain, and test. Here are refactoring opportunities and suggestions:
    
    ## **Refactoring Opportunities**
    
    ### 1. **Extract Membership Discount Logic**
    Move the entire membership-based discount logic into a helper method, e.g., `ApplyMembershipDiscounts`. This method would encapsulate all the nested membership, event, and user-attribute checks, returning the updated discount and applied discounts.
    
    ### 2. **Extract Coupon Discount Logic**
    Move coupon handling into a method like `ApplyCouponDiscounts`. This would handle coupon validation, membership-based coupon boosts, and shipping coupon logic.
    
    ### 3. **Extract Bulk Discount Logic**
    Move the bulk purchase logic into a method such as `ApplyBulkDiscounts`.
    
    ### 4. **Reduce Nesting**
    Within each helper, use early returns or guard clauses where possible to reduce nesting.
    
    ### 5. **Encapsulate Discount State**
    Consider using a small struct or class (e.g., `DiscountContext`) to pass and update the discount percent and applied discounts list, reducing parameter clutter.
    ```

1. Übermitteln Sie einen Folge-Prompt, der GitHub Copilot fragt, wie komplexe bedingte Logik vereinfacht und Schachtelungsebenen in der Methode „CalculateFinalPrice“ reduziert werden.

    Folge-Prompts sind eine hervorragende Möglichkeit, Ihre Analyse zu verfeinern und spezifischere Vorschläge von GitHub Copilot zu erhalten. In diesem Fall möchten Sie zusätzliche Informationen zum Reduzieren von Schachtelungsebenen erhalten, die sich weiterhin im Kontext komplexer Bedingungen in der Methode „CalculateFinalPrice“ befinden. Sie können auch Folge-Prompts verwenden, um um bewährte Methoden zu bitten oder die Auswirkungen zu verstehen, die vorgeschlagene Änderungen möglicherweise auf den Code haben.

    Zum Beispiel:

    ```plaintext
    How can I simplify the complex conditional logic and reduce nesting levels in the CalculateFinalPrice method? For example, the method has multiple nested conditionals that apply different membership discounts based on user status and order details. What are some best practices for reducing nesting levels and improving readability? Explain the benefit of each approach when applied to the CalculateFinalPrice method.
    ```

1. Nehmen Sie sich eine Minute Zeit, um die Vorschläge von GitHub Copilot zum Vereinfachen der bedingten Logik und zum Reduzieren der Schachtelungsebenen zu überprüfen.

    GitHub Copilot sollte eine Liste mit Vorschlägen bereitstellen, um die bedingte Logik zu vereinfachen und Schachtelungsebenen zu reduzieren. Einige der Vorschläge sind möglicherweise Wiederholungen von vorherigen Vorschlägen. Das ist zu erwarten. Es sollten jedoch neue Vorschläge zum Reduzieren von Schachtelungsebenen und zur Verbesserung der Lesbarkeit angezeigt werden, z. B.:

    - Verwenden Sie frühzeitige Rückgabe- oder Wächter-Klauseln, um Logik zu vereinfachen, Einzüge zu reduzieren und Flow zu verdeutlichen.
    - Verwenden Sie lokale Hilfsfunktionen, um Duplizierung zu entfernen und die Absicht zu verdeutlichen.
    - Verwenden Sie Switch-Ausdrücke oder Musterabgleiche, um die Mitgliedschaftslogik explizit und verwaltbar zu machen.
    - Verwenden Sie kleinere Methoden pro Mitgliedschaft, um Logik zu modularisieren und das Testen und Aktualisieren zu vereinfachen.
    - Verwenden Sie boolesche Variablen für Bedingungen, um die Lesbarkeit komplexer Überprüfungen zu verbessern.

> [!NOTE]
> Sie verwenden die Ergebnisse Ihrer Analyse, um die Aufgabe zu erstellen, die GitHub Copilot-Agent im nächsten Abschnitt der Übung zugewiesen ist.

### Umgestalten des Codes des E-Commerce-Preismoduls mithilfe von GitHub Copilot-Agent

GitHub Copilot verfügt über drei Modi, **Frage**, **Bearbeitung**und **Agent**. Wenn GitHub Copilot im Agent-Modus ausgeführt wird, funktioniert GitHub Copilot als autonomer KI-Agent.

Im Agent-Modus:

- Ihr Prompt gibt die Aufgabe an, die GitHub Copilot-Agent zugewiesen ist.
- GitHub Copilot verwendet die Aufgabeninformationen und Ihre Codebasis, um die relevanten Codedateien zu identifizieren und den Kontext für die Aufgabe einzurichten.
- GitHub Copilot formuliert einen Prozess, den er zum Ausführen der Aufgabe verwenden kann. Der Agent verwendet einen iterativen Ansatz und Codeüberprüfungen, um sicherzustellen, dass die Aufgabe erfolgreich abgeschlossen wird.
- GitHub Copilot verwendet die Chat-Ansicht, um Sie auf dem Laufenden zu halten, während er an der zugewiesenen Aufgabe arbeitet. Er kann auch Erklärungen oder Begründungen für die vorgenommenen Änderungen bereitstellen.
- GitHub Copilot kann Tools aufrufen, um die Aufgabe zu erledigen oder zu überprüfen, ob Codeänderungen ordnungsgemäß funktionieren.
- GitHub Copilot kann während der Aufgabe anhalten und Sie um Unterstützung oder Klärung bitten. Es ist wichtig, den Chat zu überwachen und zu reagieren, wenn Sie aufgefordert werden, den autonomen Agenten zu unterstützen.
- GitHub Copilot aktualisiert Ihre Codedatei im Editor von Visual Studio Code. Sobald die Aufgabe abgeschlossen ist, sollten Sie die von GitHub Copilot vorgenommenen Änderungen überprüfen, bevor Sie sie auf Ihre Codebasis anwenden (einzeln oder gemeinsam).

In diesem Abschnitt der Übung verwenden Sie GitHub Copilot-Agent, um die Klasse „PricingEngine“ umzugestalten und die komplexe bedingte Logik in der Methode „CalculateFinalPrice“ zu vereinfachen. Die Aufgabe, die Sie GitHub Copilot-Agent zuweisen, basiert auf den Vorschlägen von GitHub Copilot, die während der Codeanalyse (der vorherigen Aufgabe) bereitgestellt wurden.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Stellen Sie sicher, dass die GitHub Copilot-Chatansicht in Visual Studio Code geöffnet ist.

1. Wählen Sie in der Chat-Ansicht den **Agent-Modus** aus.

    Das Dropdownmenü **Modus festlegen** befindet sich in der unteren linken Ecke der Chat-Ansicht. Wenn Sie **Agent** auswählen, wechselt GitHub Copilot in den Agent-Modus und arbeitet autonom an Aufgaben, die Sie zuweisen.

1. Nehmen Sie sich eine Minute Zeit, um die Anforderungen für die Aufgabe zu ermitteln, die Sie GitHub Copilot-Agent zuweisen.

    Sie müssen eine Aufgabe schreiben, die Ihr Ziel erläutert und die Schritte beschreibt, die GitHub Copilot-Agent verwenden kann, um dieses Ziel zu erreichen.

    In diesem Fall umfasst Ihr Ziel die folgenden Elemente:

    - Vereinfachen der komplexen bedingten Logik und reduzieren der Schachtelungsebenen.
    - Verbessern der Codeaufrechterhaltung und Lesbarkeit.
    - Bewahren der vorhandenen Funktionen auf und Sicherstellen, dass der umgestaltete Code dieselbe Ausgabe wie der ursprüngliche Code generiert.

    In der vorherigen Aufgabe haben Sie GitHub Copilot gebeten, den Code zu analysieren und Umgestaltungsmöglichkeiten zu identifizieren. Sie haben zwei Sätze von Vorschlägen generiert, einen zum Extrahieren komplexer Logik in Hilfsmethoden zur Verbesserung der Modularität und einen weiteren zur Reduzierung der Schachtelungsebenen und zur Verbesserung der Codelesbarkeit.

    Die im vorherigen Vorgang ermittelten Umgestaltungsmöglichkeiten können Folgendes umfassen:

    - Extrahieren Sie Rabattlogik auf Mitgliedschaftsebene in eine Hilfsmethode.
    - Extrahieren Sie Coupon-Validierung und Anwendungslogik in eine Hilfsmethode.
    - Extrahieren Sie volumenbasierte Rabattlogik in eine Hilfsmethode.
    - Verwenden Sie frühzeitige Rückgabe- oder Wächter-Klauseln, um Logik zu vereinfachen, Einzüge zu reduzieren und Flow zu verdeutlichen.
    - Verwenden Sie lokale Hilfsfunktionen, um Duplizierung zu entfernen und die Absicht zu verdeutlichen.
    - Verwenden Sie Switch-Ausdrücke oder Musterabgleiche, um die Mitgliedschaftslogik explizit und verwaltbar zu machen.
    - Verwenden Sie kleinere Methoden pro Mitgliedschaft, um Logik zu modularisieren und das Testen und Aktualisieren zu vereinfachen.
    - Verwenden Sie boolesche Variablen für Bedingungen, um die Lesbarkeit komplexer Überprüfungen zu verbessern.

    Die Aufgabe, die Sie für GitHub Copilot-Agent erstellen, sollte Ihre Zielanweisung und die von Ihnen identifizierten Umgestaltungsmöglichkeiten kombinieren.

    Die Aufgabe sollte die folgende Organisationsstruktur implementieren:

    1. Zielaussage: Erläutern des Gesamtziels des Vorgangs.
    1. Codestruktur-/Modularitäts-Updates: Identifizieren Sie alle großen Codeabschnitte, die extrahiert werden können, um die Modularität zu verbessern.
    1. Kleine oder detaillierte Codeverbesserungen: Beschreiben Sie die spezifischen Ansätze, um Schachtelungsebenen zu reduzieren und die Lesbarkeit zu verbessern.
    1. Ergebnis: Beschreiben Sie das erwartete Ergebnis des Umgestaltungsprozesses.

1. Erstellen Sie eine Aufgabe, die Ihren Anforderungen entspricht.

    Ihre Aufgabe sollte Ihr Ziel und die vorgeschlagenen Umgestaltungsmöglichkeiten enthalten, die anhand der vorgeschlagenen Organisationsstruktur angeordnet sind.

    Zum Beispiel:

    ```plaintext
    I need to simplify the complex conditional logic and reduce nesting levels in the CalculateFinalPrice method. The main areas of complexity are associated with membership discounts, coupon processing, and bulk discounts. Each of these areas could be moved into separate helper methods that are called from CalculateFinalPrice. There are several options to reduce nesting levels in the helper methods. Use early returns or guard clauses to flatten logic, reduce indentation, and clarify flow. Use local helper functions to remove duplication and clarify intent. Use switch expressions or pattern matching to make membership logic explicit and maintainable. Use smaller methods per membership to modularize logic and make it easier to test and update. Use Boolean variables for conditions to improve readability of complex checks. The goal is to improve code maintainability and readability while preserving the existing functionality and generated output.
    ```

    Diese Aufgabe verwendet Text in natürlicher Sprache, um das Ziel, wichtige Umstrukturierungsmöglichkeiten und spezifische Ansätze zur Reduzierung der Schachtelungsebenen und zur Verbesserung der Lesbarkeit zu beschreiben. Die Aufgabe beschreibt auch das erwartete Ergebnis des Umgestaltungsprozesses.

1. Verwenden Sie die Chat-Ansicht, um Ihre Aufgabe GitHub Copilot-Agent zuzuweisen.

    GitHub Copilot-Agent wertet die Aufgabe und die Codebasis aus, um einen Ansatz für die Umgestaltung von „CalculateFinalPrice“ zu entwickeln und die Mitgliedschaftsrabattlogik in eine neue Hilfsmethode zu extrahieren. Der Agent testet die Code-Updates in verschiedenen Phasen, um sicherzustellen, dass die Umgestaltung erfolgreich ist und die Geschäftslogik intakt bleibt.

    Nach der Übermittlung der Aufgabe beginnt GitHub Copilot-Agent mit der Arbeit an der Aufgabe. Sie können den Fortschritt in der Chat-Ansicht überwachen.

    > [!NOTE]
    > Wenn Sie Änderungen an der Aufgabe vornehmen müssen, können Sie den Text in der Chat-Ansicht bearbeiten und ihn erneut übermitteln. GitHub Copilot-Agent wertet die Aufgabe erneut aus und arbeitet weiter daran.

1. Überwachen Sie die Chat-Ansicht, während GitHub Copilot-Agent an der Aufgabe arbeitet.

    Der Agent stellt Updates über seinen Fortschritt bereit, einschließlich aller Herausforderungen, die auftreten und wie er plant, diese zu beheben. Er kann bei Bedarf auch nach Klarstellung oder zusätzlichen Informationen fragen. Stellen Sie bei Bedarf Unterstützung bereit, indem Sie in der Chat-Ansicht auf den Prompt des Agenten reagieren.

1. Überprüfen Sie nach Abschluss der Umgestaltungsaufgabe die vorgeschlagenen Updates im Editor von Visual Studio Code.

    Überprüfen Sie die von GitHub Copilot vorgeschlagenen Änderungen immer, bevor Sie sie akzeptieren. Stellen Sie sicher, dass die Updates mit Ihrer beabsichtigten Geschäftslogik, der App-Funktionalität und den Codierungsstandards übereinstimmen.

    Der umgestaltete Code sollte eine stark vereinfachte **CalculateFinalPrice**-Methode enthalten, die hauptsächlich aus Methodenaufrufen für Hilfsmethoden besteht, die Mitgliedschaftsrabatte, Coupon-Rabatte und Massenrabatte verwalten. Die Komplexität der ursprünglichen Methode sollte erheblich reduziert sein, wodurch sie einfacher zu lesen und verwalten ist.

    Die Hilfsmethode für Mitgliedschaftsrabatte sollte auch umgestaltet werden, um die komplexe Logik um Mitgliedschaftsebenen zu behandeln, mit einer zusätzlichen Hilfsmethode für jede Stufe (Premium, Gold, Silber und Personen, die zum ersten Mal einkaufen).

1. Wählen Sie in der Chat-Ansicht die Option **Beibehalten**aus, um alle Bearbeitungen zu akzeptieren.

    Sie können die vorgeschlagenen Änderungen ablehnen, wenn sie Ihre Erwartungen nicht erfüllen, oder Sie können einen Teil der Änderungen akzeptieren und andere ablehnen. Die Arbeit mit GitHub Copilot zum Umgestalten Ihres Codes ist häufig ein iterativer Prozess, der das Verfeinern Ihres Prompts zum Erzielen der beabsichtigten Ergebnisse umfasst.

    Wenn Sie die vorgeschlagenen Updates von GitHub Copilot akzeptieren und dann feststellen, dass die Vorschläge Probleme eingeführt haben, die möglicherweise schwierig zu lösen sind, können Sie die Änderungen rückgängig machen, indem Sie in der Chat-Ansicht die Option **Letzte Anforderung rückgängig machen** auswählen oder die Funktion zum Rückgängigmachen von Visual Studio Code verwenden.

1. Bitten Sie GitHub Copilot, die implementierten Codeumgestaltungs-Updates zu erläutern.

    Zum Beispiel:

    ```plaintext
    Explain the refactoring updates that you implemented to simplify the complex conditional logic, reduce nesting levels, and improve code maintainability and readability.
    ```

    GitHub Copilot stellt eine Erklärung der vorgenommenen Änderungen zur Verfügung, einschließlich wie die komplexe bedingte Logik vereinfacht wurde und wie die Codestruktur verbessert wurde.

    Zum Beispiel:

    ```md
    Here’s an explanation of the refactoring updates made to simplify the complex conditional logic, reduce nesting, and improve maintainability and readability in the `CalculateFinalPrice` method:
    
    ### 1. **Separation of Concerns with Helper Methods**
    - The main discount logic was split into three focused helper methods: `ApplyMembershipDiscounts`, `ApplyCouponDiscounts`, and `ApplyBulkDiscounts`.
    - Each helper method is responsible for a single aspect of the discount calculation, making the main method concise and easy to follow.
    
    ### 2. **Flattened Membership Discount Logic**
    - The deeply nested membership discount logic was moved into `ApplyMembershipDiscounts`, which uses a `switch` statement to dispatch to smaller, membership-specific methods (`ApplyPremiumDiscounts`, `ApplyGoldDiscounts`, `ApplySilverDiscounts`, `ApplyFirstTimeBuyerDiscounts`).
    - Each of these methods uses guard clauses (early returns) and Boolean variables to flatten the logic, reducing indentation and clarifying the flow.
    
    ### 3. **Guard Clauses and Early Returns**
    - Instead of multiple nested `if` statements, each helper method uses guard clauses to exit early when a condition is not met. This keeps the main logic path at the top level and reduces cognitive load.
    
    ### 4. **Switch Expressions and Pattern Matching**
    - The use of `switch` in `ApplyMembershipDiscounts` makes the membership logic explicit and easy to extend or modify.
    - This approach also makes it clear which logic applies to which membership type.
    
    ### 5. **Boolean Variables for Readability**
    - Boolean variables (e.g., `altPayment`, `premiumPayment`) are used to clarify complex conditions, making the code more self-documenting and easier to read.
    
    ### 6. **Local Helper Methods for Duplication and Intent**
    - Smaller, focused methods encapsulate repeated or complex logic, such as safe discount addition and category percentage calculation.
    - This reduces code duplication and clarifies the intent of each operation.
    
    ### 7. **Preserved Business Logic and Output**
    - All business rules, discount caps, and output formatting are preserved, ensuring that the refactoring does not change the program’s behavior.
    
    ## **Benefits**
    - **Readability:** The main method is now a clear sequence of high-level steps.
    - **Maintainability:** Each discount rule is isolated, making it easier to update or test.
    - **Extensibility:** Adding or modifying discount rules is straightforward.
    - **Testability:** Each helper method can be unit tested independently.
    
    This refactoring transforms a complex, deeply nested method into a modular, maintainable, and readable pricing engine, while preserving all business requirements and output.
    ```

1. Nehmen Sie sich eine Minute Zeit, um den umgestalteten Code in der Klasse „PricingEngine“ zu überprüfen.

1. Übermitteln Sie einen Folge-Prompt, der GitHub Copilot auffordert, bestimmte Teile des umgestalteten Codes zu erläutern oder die ursprünglichen und umgestalteten Versionen zu vergleichen.

    Zum Beispiel:

    ```plaintext
    Compare the original PricingEngine class with the new refactored version of the PricingEngine class. Explain the relationship between methods in the two versions. Explain the implementation of business rules in the two versions.
    ```

### Testen des umgestalteten Codes des E-Commerce-Preismoduls

Tests sind entscheidend, um sicherzustellen, dass ihre Umgestaltung das Verhalten der Geschäftslogik nicht verändert. Führen Sie den Code mit verschiedenen Szenarien aus, um sicherzustellen, dass die Berechnungen konsistent bleiben.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Erstellen Sie das Projekt, um sicherzustellen, dass keine Kompilierungsfehler auftreten.

    Klicken Sie beispielsweise in der PROJEKTMAPPEN-EXPLORER-Ansicht mit der rechten Maustaste auf **ECommercePricingEngine** und wählen Sie dann **Erstellen** aus.

    Wenn Kompilierungsfehler auftreten, überprüfen Sie den umgestalteten Code, und beheben Sie alle Probleme. GitHub Copilot kann bei Bedarf Kompilierungsfehler beheben.

1. Führen Sie die Anwendung aus, um die umgestaltete Preislogik zu testen.

    Wenn die Datei „ECommercePricingDemo.cs“ im Editor von Visual Studio Code geöffnet ist, können Sie das Projekt ausführen, indem Sie die Schaltfläche „Ausführen“ (Projekt ausführen, das dieser Datei zugeordnet ist) auswählen, die sich in der oberen rechten Ecke des Editor-Bereichs befindet. Um das Projekt aus der PROJEKTMAPPEN-EXPLORER-Ansicht auszuführen, klicken Sie mit der rechten Maustaste auf **ECommercePricingEngine**, wählen Sie **Debuggen** aus und dann **Neue Instanz starten**.

    Die Anwendung sollte ohne Fehler ausgeführt werden und Preisberechnungen für verschiedene Testszenarien anzeigen.

    > [!IMPORTANT]
    > Wenn der umgestaltete Code auf einen Laufzeitfehler stößt, überprüfen Sie die von GitHub Copilot-Agent vorgenommenen Änderungen und beheben Sie die Probleme mit GitHub Copilot. Bei Bedarf können Sie die Option **Letzte Anforderung rückgängig machen** in der Chat-Ansicht verwenden, um den letzten Satz von Änderungen rückgängig zu machen, und dann die Aufgabe aktualisieren, die GitHub Copilot-Agent zugewiesen ist. Das Durchlaufen von Prompts/Aufgaben zum Verfeinern der Ergebnisse ist bei der Arbeit mit KI-fähigen Tools die üblich.

1. Bitten Sie GitHub Copilot, die vom umgestalteten Code generierte Ausgabe mit der ursprünglichen Ausgabe zu vergleichen.

    Die ursprüngliche Ausgabe, **Output-ECommercePricingEngine.txt**, ist im Ordner „ECommercePricingEngine“ enthalten.

    Sie können eine zweite Ausgabedatei erstellen und GitHub Copilot bitten, alle Unterschiede zwischen den beiden Dateien zu ermitteln.

    Die Ausgabe sollte identisch sein, wobei bestätigt wird, dass die Geschäftslogik unverändert bleibt und gleichzeitig die Wartung und Lesbarkeit des Codes verbessert wird.

### (OPTIONAL) Vereinfachen komplexer Bedingungen in der Demo-App „LoanApprovalWorkflow“

Wenn die Zeit es zulässt, vereinfachen Sie komplexe Bedingungen in der Demo-App „LoanApprovalWorkflow“ mit demselben Prozess, mit dem Sie die Preislogik in der Beispiel-App für den Workflow von Genehmigungen für Kredite vereinfacht haben.

In dieser optionalen Aufgabe wenden Sie dieselben Techniken an, die Sie im E-Commerce-Preismodul verwendet haben, um die komplexe bedingte Logik in der Demo-App „LoanApprovalWorkflow“ umzugestalten. Sie analysieren den Kreditgenehmigungscode, identifizieren Umgestaltungsmöglichkeiten und verwenden dann GitHub Copilot-Agent, um komplexe Bedingungen in kleinere, fokussierte Hilfsmethoden zu extrahieren.

> [!IMPORTANT]
> Die Anweisungen für diese Aufgabe umfassen die allgemeinen Prozessschritte, enthalten jedoch keine vorgeschlagenen Prompts oder detaillierte Erklärungen. Sie können sich auf die vorherigen Aufgaben in dieser Übung beziehen, um Beispiele für das Erstellen von Prompts und die effektive Verwendung von GitHub Copilot zu erhalten.

Führen Sie die folgenden Schritte aus, um dies abzuschließen:

1. Erweitern Sie den Projektordner **LoanApprovalWorkflow**, öffnen Sie die Datei **LoanApprovalDemo.cs** und überprüfen Sie dann den Code.

1. Verwenden Sie GitHub Copilot, um den Code in **LoanApprovalDemo.cs** zu erläutern, einschließlich der komplexen bedingten Logik in der Methode „Evaluate“ der Klasse „LoanEvaluator“.

1. Führen Sie das Projekt „LoanApprovalWorkflow“ aus, um die erste Kreditgenehmigungslogik zu testen und einen Datensatz der Ausgabe zu erstellen.

1. Verwenden Sie GitHub Copilot, um Codeumgestaltungsmöglichkeiten zu identifizieren, die komplexe Bedingungen vereinfachen, Schachtelungsebenen reduzieren und die Lesbarkeit und Wartung in der Klasse „LoanEvaluator“ verbessern.

1. Weisen Sie GitHub Copilot-Agent eine Aufgabe zu, die komplexe bedingte Logik vereinfacht, Schachtelungsebenen reduziert und die Lesbarkeit und Wartung in der Klasse „LoanEvaluator“ verbessert (Umgestaltung der Methode „Evaluate“).

    Sie könnten beispielsweise GitHub Copilot-Agent bitten, Hilfsmethoden für die Kreditbewertung, Einkommens- und Beschäftigungsüberprüfung, Finanzkennzahlberechnungen, Berechtigungen für staatliche Hilfsprogramme und Kreditbedingungen zu erstellen.

1. Verwenden Sie GitHub Copilot-Agent, um komplexe bedingte Logik zu vereinfachen und Schachtelungsebenen in den Hilfsmethoden zu reduzieren.

1. Testen Sie Ihren umgestalteten Code, und stellen Sie sicher, dass die Demo-App für die Kreditgenehmigung dieselben Ergebnisse wie die ursprüngliche Implementierung erzeugt.

## Zusammenfassung

In dieser Übung haben Sie gelernt, wie Sie GitHub Copilot verwenden, um komplexe bedingte Logik in einer Codebasis zu vereinfachen. Sie haben die Demo-Apps für den E-Commerce-Preis und den Workflow zur Genehmigung von Krediten kennengelernt, Umgestaltungsmöglichkeiten identifiziert und den GitHub Copilot-Agent verwendet, um komplexe Bedingungen in kleinere, fokussierte Hilfsmethoden zu extrahieren. Außerdem haben Sie gelernt, wie Sie die Schachtelungsebenen im Code reduzieren, um die Lesbarkeit zu verbessern und dabei dieselbe Geschäftslogik beizubehalten.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich eine Minute Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder GitHub Copilot-Abonnement vorgenommen haben, das Sie nicht beibehalten möchten. Wenn Sie Änderungen vorgenommen haben, setzen Sie sie nach Bedarf zurück. Wenn Sie einen lokalen PC als Lab-Umgebung verwenden, können Sie den Beispielprojektordner archivieren oder löschen, den Sie für diese Übung erstellt haben.
