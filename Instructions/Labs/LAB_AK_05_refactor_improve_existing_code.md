---
lab:
  title: Übung – Umgestalten von vorhandenem Code mithilfe von GitHub Copilot
  description: 'Erfahren Sie, wie Sie vorhandene Codeabschnitte mithilfe von GitHub Copilot in Visual Studio Code umgestalten und verbessern.'
---

# Umgestalten von vorhandenem Code mithilfe von GitHub Copilot

Mit GitHub Copilot können Sie Ihre gesamte Codebasis auswerten und Aktualisierungen vorschlagen, die Ihnen bei der Umgestaltung und Verbesserung Ihres Codes helfen. In dieser Übung verwenden Sie GitHub Copilot, um bestimmte Abschnitte einer C#-Anwendung umzugestalten, während Sie Verbesserungen an Codequalität, Zuverlässigkeit, Leistung und Sicherheit vornehmen.

Diese Übung dauert ca. **30** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, benötigen Sie ein eigenes GitHub-Konto und ein GitHub Copilot-Abonnement. Falls Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses Einzelkonto <a href="https://github.com/" target="_blank">registrieren</a> und den GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie in Ihrer Übungsumgebung Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement für diese Übung verwenden.

## Vor der Installation

Ihre Übungsumgebung muss die folgenden Voraussetzungen erfüllen: Git 2.48 oder höher, .NET SDK 9.0 oder höher, Visual Studio Code mit der C# -Dev-Kit-Erweiterung und Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

Wenn Sie einen lokalen PC als Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Wenn Sie Hilfe beim Konfigurieren Ihres lokalen PCs als Übungsumgebung benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320147" target="_blank">Konfigurieren Sie Ihre Ressourcen für die Übungsumgebung</a>.

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

Wenn Sie eine gehostete Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen einen Browser und fügen Sie die folgende URL in die Navigationsleiste ein: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

- Öffnen Sie die Eingabeaufforderung und führen Sie dann die folgenden Befehle aus:

    Um sicherzustellen, dass Visual Studio Code für die Verwendung der richtigen Version von .NET konfiguriert ist, führen Sie den folgenden Befehl aus:

    ```bash

    dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org

    ```

## Übungsszenario

Sie sind Entwicklerin bzw. Entwickler und arbeiten in der IT-Abteilung Ihrer lokalen Community. Die Back-End-Systeme, die die öffentliche Bibliothek unterstützen, wurden bei einem Brand zerstört. Ihr Team muss eine temporäre Lösung entwickeln, damit die Mitarbeitenden der Bibliothek ihre Vorgänge verwalten können, bis das System ersetzt werden kann. Ihr Team hat GitHub Copilot ausgewählt, um den Entwicklungsprozess zu beschleunigen.

Sie haben eine erste Version der Bibliotheksanwendung zur Überprüfung abgegeben. Das Überprüfungsteam hat Möglichkeiten zur Verbesserung der Codequalität, Leistung, Lesbarkeit, Wartung und Sicherheit identifiziert.

Ihnen werden die folgenden Updates zugewiesen:

1. Gestalten Sie die Klasse „EnumHelper“ so um, dass statische Wörterbücher anstelle von Reflexion verwendet werden.

    - Die Verwendung statischer Wörterbücher verbessert die Leistung (erspart den Aufwand der Reflexion).
    - Das Entfernen der Reflexion verbessert auch die Lesbarkeit, Wartungsfreundlichkeit und Sicherheit von Code.

1. Gestalten Sie die Datenzugriffsmethoden so um, dass LINQ (Language Integrated Query) anstelle von Foreach-Schleifen verwendet wird.

    - Das Verwenden von LINQ bietet eine präzisere und besser lesbare Möglichkeit zum Abfragen von Sammlungen, Datenbanken und XML-Dokumenten.
    - Außerdem kann dadurch die Lesbarkeit, Wartungsfreundlichkeit und Leistung von Code verbessert werden.

Diese Übung umfasst die folgenden Aufgaben:

1. Richten Sie die Bibliotheksanwendung in Visual Studio Code ein.
1. Analysieren Sie Code in der Chat-Ansicht und gestalten Sie ihn in den Modi „Fragen“ und „Bearbeiten“ um.
1. Gestalten Sie Code mithilfe von Inline-Chat und der Chat-Ansicht in den Modi „Bearbeiten“ und „Agent“ um.

## Einrichten der Bibliotheksanwendung in Visual Studio Code

Sie müssen die vorhandene Anwendung herunterladen, die Codedateien extrahieren und dann die Projektmappe in Visual Studio Code öffnen.

Gehen Sie folgendermaßen vor, um die Bibliotheksanwendung einzurichten:

1. Öffnen Sie ein Browserfenster in Ihrer Übungsumgebung.

1. Um eine ZIP-Datei mit der Bibliotheksanwendung herunterzuladen, fügen Sie die folgende URL in die Adressleiste Ihres Browsers ein: [GitHub Copilot-Übung – Umgestalten von vorhandenem Code](https://github.com/MicrosoftLearning/mslearn-github-copilot-dev/raw/refs/heads/main/DownloadableCodeProjects/Downloads/AZ2007LabAppM5.zip)

    Die ZIP-Datei heißt **AZ2007LabAppM5.zip**.

1. Extrahieren Sie die Dateien aus der Datei **AZ2007LabAppM5.zip**.

    Zum Beispiel:

    1. Navigieren Sie zu dem Ordner mit Downloads in Ihrer Übungsumgebung.

    1. Klicken Sie mit der rechten Maustaste auf **AZ2007LabAppM5.zip** und wählen Sie dann **Alle extrahieren** aus.

    1. Wählen Sie **Dateien nach Extrahierung anzeigen** und dann **Extrahieren** aus.

1. Öffnen Sie den Ordner mit den extrahierten Dateien und kopieren Sie dann den Ordner **AccelerateDevGHCopilot** an einen Speicherort, auf den Sie einfach zugreifen können, z. B. Ihren Windows-Desktop-Ordner.

1. Öffnen Sie den Ordner **AccelerateDevGHCopilot** in Visual Studio Code.

    Zum Beispiel:

    1. Öffnen Sie Visual Studio Code in Ihrer Übungsumgebung.

    1. Wählen Sie in Visual Studio Code im Menü **Datei** die Option **Ordner öffnen** aus.

    1. Navigieren Sie zum Windows-Desktop-Ordner und wählen Sie **AccelerateDevGHCopilot** und dann **Ordner auswählen** aus.

1. Überprüfen Sie in der Visual Studio Code-Ansicht „PROJEKTMAPPEN-EXPLORER“ die folgende Projektmappenstruktur:

    - AccelerateDevGHCopilot\
        - src\
            - Library.ApplicationCore\
            - Library.Console\
            - Library.Infrastructure\
        - tests\
            - UnitTests\

1. Stellen Sie sicher, dass die Lösung erfolgreich erstellt wird.

    Um beispielsweise die Projektmappe in der PROJEKTMAPPEN-EXPLORER-Ansicht zu erstellen, klicken Sie mit der rechten Maustaste auf **AccelerateDevGHCopilot** und wählen Sie anschließend **Erstellen** aus.

    Es werden einige Warnungen angezeigt, es sollten aber keine Fehler auftreten.

## Analysieren von Code in der Chat-Ansicht und Umgestaltung in den Modi „Fragen“ und „Bearbeiten“

Reflexion ist ein leistungsfähiges Feature, mit dem Sie Objekte während der Runtime untersuchen und bearbeiten können. Reflexion kann jedoch langsam sein, und es gibt dabei potenzielle Sicherheitsrisiken, die berücksichtigt werden sollten.

Sie müssen folgende Schritte durchführen:

1. Analysieren Sie Ihren Arbeitsbereich und untersuchen Sie, wie Sie Ihre zugewiesene Aufgabe angehen sollten.
1. Gestalten Sie die Klasse „EnumHelper“ so um, dass statische Wörterbücher anstelle von Reflexion verwendet werden.

### Analysieren der Klasse „EnumHelper“ mithilfe der Chat-Ansicht im Modus „Fragen“

Die Chat-Ansicht von GitHub Copilot verfügt über drei Modi: **Fragen**, **Bearbeiten** und **Agent**. Jeder Modus wurde für verschiedene Arten von Interaktionen mit GitHub Copilot entwickelt.

- **Fragen**: Verwenden Sie diesen Modus, um GitHub Copilot Fragen zu Ihrer Codebasis zu stellen. Sie können GitHub Copilot bitten, Code zu erklären, Änderungen vorzuschlagen oder Informationen zur Codebasis bereitzustellen.
- **Bearbeiten**: Verwenden Sie diesen Modus, um ausgewählte Codedateien zu bearbeiten. Sie können GitHub Copilot verwenden, um Code umzugestalten, Kommentare hinzuzufügen oder andere Änderungen an Ihrem Code vorzunehmen.
- **Agent**: Verwenden Sie diesen Modus, um GitHub Copilot als Agent auszuführen. Sie können GitHub Copilot verwenden, um Befehle auszuführen, Code auszuführen oder andere Aufgaben in Ihrem Arbeitsbereich auszuführen.

In diesem Abschnitt der Übung verwenden Sie die Chat-Ansicht im Modus „Fragen“, um Ihre Programmieraufgabe zu analysieren.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie in der PROJEKTMAPPEN-EXPLORER-Ansicht den Ordner **Library.ApplicationCore** und anschließend den Ordner **Enums**.

1. Öffnen Sie die Datei EnumHelper.cs und überprüfen Sie den vorhandenen Code.

    ```csharp
    using System.ComponentModel;
    using System.Reflection;
    
    namespace Library.ApplicationCore.Enums;
    
    public static class EnumHelper
    {
        public static string GetDescription(Enum value)
        {
            if (value == null)
                return string.Empty;
    
            FieldInfo fieldInfo = value.GetType().GetField(value.ToString())!;
    
            DescriptionAttribute[] attributes =
                (DescriptionAttribute[])fieldInfo.GetCustomAttributes(typeof(DescriptionAttribute), false);
    
            if (attributes != null && attributes.Length > 0)
            {
                return attributes[0].Description;
            }
            else
            {
                return value.ToString();
            }
        }
    }
    ```

1. Öffnen Sie die Chat-Ansicht von GitHub Copilot.

    Die Chat-Ansicht bietet eine verwaltete Chatoberfläche zur Interaktion mit GitHub Copilot.

    Sie können die Chat-Ansicht über die Schaltfläche **Toggle Chat** ein- und ausblenden. Diese befindet sich oben im Visual-Studio-Code-Fenster, rechts neben dem Suchtextfeld.

    ![Screenshot der Copilot-Schaltfläche „Chat umschalten“.](./Media/m01-github-copilot-toggle-chat.png)

    Sie können auch die Tastenkombination **Strg+Alt+I** verwenden, um die Chat-Ansicht umzuschalten.

1. Beachten Sie, dass die Chat-Ansicht standardmäßig im Modus **Fragen** geöffnet wird.

    Der aktuelle Chatmodus wird in der unteren rechten Ecke der Chat-Ansicht angezeigt. Chat-Antworten werden in der Chat-Ansicht angezeigt, wenn Sie im Modus **Fragen** arbeiten.

1. Wählen Sie den Code in der Datei EnumHelper.cs aus.

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext
    @workspace Explain how the GetDescription method uses reflection to assign the return value.
    ```

1. Nehmen Sie sich kurz Zeit, um die Antwort zu überprüfen.

    Die Methode **GetDescription** verwendet Reflexion, um das Beschreibungsattribut eines Enumerations-Parameters namens **value** abzurufen.

    Die Methode überprüft, ob der Parameter **value** null ist. Ist dies der Fall, gibt die Methode eine leere Zeichenfolge zurück. Andernfalls wird Reflexion verwendet, um die Feldinformationen für den Enumerationswert und die Attribute des Typs **DescriptionAttribute** abzurufen. Wenn Attribute gefunden werden, wird die Beschreibung zurückgegeben, andernfalls die Zeichenfolgendarstellung des Enumerations-Werts.

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext
    @workspace Which files in this workspace are used to store the enum values passed to the GetDescription method?
    ```

    Die Antwort sollte Sie auffordern, den Ordner „Enums“ zu überprüfen. Die Enumerationswerte werden in den Dateien **LoanExtensionStatus**, **LoanReturnStatus** und **MembershipRenewalStatus** definiert.

1. Fügen Sie die folgenden Dateien zum Chat-Kontext hinzu:

    - EnumHelper.cs
    - LoanExtensionStatus.cs
    - LoanReturnStatus.cs
    - MembershipRenewalStatus.cs

    Sie können die Dateien aus der EXPLORER-Ansicht von Visual Studio Code per Drag-and-Drop in die Chat-Ansicht ziehen. Sie können auch die Schaltfläche **Kontext hinzufügen** in der Chat-Ansicht verwenden, um Dateien und andere Ressourcen hinzuzufügen.

    > **HINWEIS:** Durch das Hinzufügen von Dateien zum Chat-Kontext wird sichergestellt, dass GitHub Copilot diese Dateien beim Generieren einer Antwort berücksichtigt. Die Relevanz und die Genauigkeit der Antworten erhöhen sich, wenn GitHub Copilot den Kontext Ihrer Prompts versteht.

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext

    @workspace I need to refactor the `EnumHelper` class and remove any code that uses reflection. Use static dictionaries to supply enum description attributes. Use a separate dictionary for each enum. The dictionaries should use values from the `LoanExtensionStatus.cs`, `LoanReturnStatus.cs`, and `MembershipRenewalStatus.cs` files. Explain how to update the EnumHelper class using dictionaries and show me the updated code.

    ```

    Beim Schreiben von Prompts sind Klarheit und Kontext wichtig. Mithilfe von Chat-Teilnehmern, Slash-Befehlen und Chat-Variablen können Sie den Kontext so definieren, dass GitHub Copilot ihn versteht.

    Wenn Sie einen Prompt schreiben, der GitHub Copilot auffordert, ein Problem zu lösen, beginnen Sie mit dem Problem, das Sie lösen möchten. Verwenden Sie prägnante Sätze, um Details zu beschreiben, Einschränkungen festzulegen und Ressourcen zu identifizieren. Stellen Sie abschließend sicher, dass Sie GitHub Copilot mitteilen, was in die Antwort eingeschlossen werden soll.

    In diesem Fall beginnt Ihr Prompt mit einer Beschreibung Ihres Problems/Ziels. Sie teilen GitHub Copilot mit, dass Sie die Klasse **EnumHelper** umgestalten und sämtlichen Code entfernen müssen, der Reflexionen verwendet. Sie teilen GitHub Copilot mit, dass Sie Wörterbücher verwenden möchten, um die Beschreibungsattribute von Enumerationen bereitzustellen. Sie geben an, dass für jede Enumeration ein separates Wörterbuch verwendet werden soll, und teilen GitHub Copilot mit, dass die Enumerationswerte aus den von Ihnen genannten Dateien stammen sollen. Sie müssen GitHub Copilot bitten, zu erläutern, wie die Klasse **EnumHelper** aktualisiert wird, und nach einem Codebeispiel fragen, das den aktualisierten Code enthält.

1. Nehmen Sie sich kurz Zeit, um die von GitHub Copilot generierte Antwort zu überprüfen.

    Die Antwort sollte den folgenden Markdown- und Codebeispielen ähneln:

    ```markdown

    To refactor the EnumHelper class and remove reflection, you can create static dictionaries for each enum type. These dictionaries will map each enum value to its description. The dictionaries will be initialized with the descriptions defined in the Description attributes of the enums.

    Here's how to update the **EnumHelper** class:

    1. Create a static dictionary for each enum (LoanExtensionStatus, LoanReturnStatus, and MembershipRenewalStatus).
    2. Populate these dictionaries with the enum values as keys and their descriptions as values.
    3. Update the GetDescription method to retrieve the description from the appropriate dictionary based on the enum type.

    Here’s the updated code:

    ```

    ```csharp

    using System.Collections.Generic;
    
    namespace Library.ApplicationCore.Enums;
    
    public static class EnumHelper
    {
        private static readonly Dictionary<LoanExtensionStatus, string> LoanExtensionStatusDescriptions = new()
        {
            { LoanExtensionStatus.Success, "Book loan extension was successful." },
            { LoanExtensionStatus.LoanNotFound, "Loan not found." },
            { LoanExtensionStatus.LoanExpired, "Cannot extend book loan as it already has expired. Return the book instead." },
            { LoanExtensionStatus.MembershipExpired, "Cannot extend book loan due to expired patron's membership." },
            { LoanExtensionStatus.LoanReturned, "Cannot extend book loan as the book is already returned." },
            { LoanExtensionStatus.Error, "Cannot extend book loan due to an error." }
        };
    
        private static readonly Dictionary<LoanReturnStatus, string> LoanReturnStatusDescriptions = new()
        {
            { LoanReturnStatus.Success, "Book was successfully returned." },
            { LoanReturnStatus.LoanNotFound, "Loan not found." },
            { LoanReturnStatus.AlreadyReturned, "Cannot return book as the book is already returned." },
            { LoanReturnStatus.Error, "Cannot return book due to an error." }
        };
    
        private static readonly Dictionary<MembershipRenewalStatus, string> MembershipRenewalStatusDescriptions = new()
        {
            { MembershipRenewalStatus.Success, "Membership renewal was successful." },
            { MembershipRenewalStatus.PatronNotFound, "Patron not found." },
            { MembershipRenewalStatus.TooEarlyToRenew, "It is too early to renew the membership." },
            { MembershipRenewalStatus.LoanNotReturned, "Cannot renew membership due to an outstanding loan." },
            { MembershipRenewalStatus.Error, "Cannot renew membership due to an error." }
        };
    
        public static string GetDescription<TEnum>(TEnum value) where TEnum : Enum
        {
            return value switch
            {
                LoanExtensionStatus loanExtensionStatus => LoanExtensionStatusDescriptions[loanExtensionStatus],
                LoanReturnStatus loanReturnStatus => LoanReturnStatusDescriptions[loanReturnStatus],
                MembershipRenewalStatus membershipRenewalStatus => MembershipRenewalStatusDescriptions[membershipRenewalStatus],
                _ => value.ToString()
            };
        }
    }

    ```

    ```markdown

    Explanation:
    
    1. Static Dictionaries: Each dictionary is specific to an enum type and maps enum values to their descriptions.
    2. Generic Method: The GetDescription method is now generic and uses a switch expression to determine which dictionary to use based on the enum type.
    3. No Reflection: The use of reflection is completely removed, improving performance and type safety.
    
    This approach ensures that the descriptions are statically defined and avoids the runtime overhead of reflection.

    ```

1. Zeigen Sie mit dem Mauszeiger in der Chat-Ansicht auf das Codebeispiel, das in der Antwort enthalten ist.

1. Beachten Sie die drei Schaltflächen, die in der oberen rechten Ecke des Codeausschnitts angezeigt werden.

1. Zeigen Sie mit dem Mauszeiger auf die einzelnen Schaltflächen, um eine QuickInfo anzuzeigen, die die Aktion beschreibt.

    Die ersten beiden Schaltflächen kopieren Code in den Editor. Die dritte Schaltfläche kopiert Code in die Zwischenablage.

> **HINWEIS:** Sie könnten den Modus „Fragen“ verwenden, um die Klasse **EnumHelper** zu aktualisieren. Der Modus „Bearbeiten“ gestaltet Ihren Code jedoch direkt im Code-Editor um und bietet weitere Optionen zum Akzeptieren von Updates.

### Umgestalten der Klasse „EnumHelper“ mithilfe der Chat-Ansicht im Modus „Bearbeiten“

Der Modus „Bearbeiten“ der Chat-Ansicht wurde für die Bearbeitung von Code in Ihrem Arbeitsbereich entwickelt. Sie können den Modus „Bearbeiten“ verwenden, um Code umzugestalten, Kommentare hinzuzufügen oder andere Änderungen an Ihrem Code vorzunehmen.

1. Wählen Sie in der Chat-Ansicht **Modus festlegen** und dann **Bearbeiten** aus.

    Wenn Sie gefragt werden, ob Sie eine neue Sitzung im Modus „Bearbeiten“ starten möchten, wählen Sie **Ja** aus.

    Im Modus **Bearbeiten** zeigt GitHub Copilot Antworten als Vorschläge zum Aktualisieren des Codes im Code-Editor an. Der Modus „Bearbeiten“ wird in der Regel verwendet, wenn ein neues Feature implementiert, ein Fehler behoben oder Code umgestaltet wird.

1. Fügen Sie die folgenden Dateien zum Chat-Kontext hinzu:

    - EnumHelper.cs
    - LoanExtensionStatus.cs
    - LoanReturnStatus.cs
    - MembershipRenewalStatus.cs

1. Überprüfen Sie ihn und geben Sie dann den folgenden Prompt ein:

    ```plaintext

    #codebase I need to refactor the `EnumHelper` class and remove any code that uses reflection. Use static dictionaries to supply enum description attributes. Use a separate dictionary for each enum. The dictionaries should use values from the `LoanExtensionStatus.cs`, `LoanReturnStatus.cs`, and `MembershipRenewalStatus.cs` files.

    ```

    Dieser Prompt weist GitHub Copilot an, die Klasse **EnumHelper** mithilfe von Wörterbüchern statt Reflexion umzugestalten, um die Beschreibungsattribute von Enumerationen zuzuweisen. Er legt fest, dass für jede Enumeration ein separates Wörterbuch verwendet werden soll und dass die Enumerationswerte aus bestimmten Dateien stammen sollen.

1. Nehmen Sie sich kurz Zeit, um die vorgeschlagenen Code-Updates zu überprüfen.

    Überprüfen Sie die vorgeschlagenen Updates, um sicherzustellen, dass die Enumerationswerte aus den Dateien **LoanExtensionStatus.cs**, **LoanReturnStatus.cs** und **MembershipRenewalStatus.cs** stammen.

    Öffnen Sie die einzelnen Enumerationsdateien und stellen Sie sicher, dass die Enumerationswerte in den Wörterbüchern korrekt sind. Wenn Diskrepanzen vorliegen, fordern Sie GitHub Copilot dazu auf, die Wörterbücher für jede Enumeration einzeln zu aktualisieren. Beispielsweise können Sie den folgenden Prompt für die Enumeration **LoanExtensionStatus** verwenden:

    ```plaintext

    #codebase Use the description values in LoanExtensionStatus.cs to update the LoanExtensionStatus dictionary in the EnumHelper class. Provide the updated code for the LoanExtensionStatus dictionary in the EnumHelper class.

    ```

1. Wählen Sie in der Chat-Ansicht die Option **Behalten**aus, um alle Updates zu akzeptieren.

    Sie können auch die Symbolleiste „Chat-Bearbeitungen“ am unteren Rand der Registerkarte „Code-Editor“ verwenden, um Code-Updates anzunehmen oder abzulehnen.

1. Nehmen Sie sich kurz Zeit, um die Methode **GetDescription** zu überprüfen.

    GitHub Copilot sollte die Methode **GetDescription** aktualisiert haben, um Musterabgleich und statische Wörterbücher anstelle von Reflexion zu verwenden. Die aktualisierte Methode sollte einem der folgenden Beispiele ähneln:

    ```csharp

    public static string GetDescription(Enum value)
    {
        if (value == null)
            return string.Empty;

        // Use type checks to select the correct dictionary
        if (value is LoanExtensionStatus les && LoanExtensionStatusDescriptions.TryGetValue(les, out var lesDesc))
            return lesDesc;
        if (value is LoanReturnStatus lrs && LoanReturnStatusDescriptions.TryGetValue(lrs, out var lrsDesc))
            return lrsDesc;
        if (value is MembershipRenewalStatus mrs && MembershipRenewalStatusDescriptions.TryGetValue(mrs, out var mrsDesc))
            return mrsDesc;

        return value.ToString();
    }

    ```

    oder

    ```csharp

    public static string GetDescription<TEnum>(TEnum value) where TEnum : Enum
    {
        return value switch
        {
            MembershipRenewalStatus status => MembershipRenewalDescriptions.TryGetValue(status, out var description) ? description : status.ToString(),
            LoanReturnStatus status => LoanReturnDescriptions.TryGetValue(status, out var description) ? description : status.ToString(),
            LoanExtensionStatus status => LoanExtensionDescriptions.TryGetValue(status, out var description) ? description : status.ToString(),
            _ => value.ToString()
        };
    }

    ```

    Dieser Code verwendet den Musterabgleich, um den Typ der Enumeration zu bestimmen und die Beschreibung aus dem entsprechenden Wörterbuch abzurufen. Die **switch**-Anweisung überprüft den Typ des Enumerationswerts und gibt die entsprechende Beschreibung aus dem Wörterbuch zurück. Wenn der Enumerationswert im Wörterbuch nicht gefunden wird, greift die Methode auf den Aufruf von ToString() für den Enumerationswert zurück, der den Namen des Enumerationselements als Zeichenfolge zurückgibt.

    Wenn Sie GitHub Copilot die Methode GetDescription umgestalten lassen, um die Lambda-Ausdrücke zu entfernen, ist die zugrunde liegende Logik leichter nachzuvollziehen:

    ```csharp

    public static string GetDescription<TEnum>(TEnum value) where TEnum : Enum
    {
        switch (value)
        {
            case MembershipRenewalStatus status:
                string membershipDescription;
                if (MembershipRenewalDescriptions.TryGetValue(status, out membershipDescription))
                {
                    return membershipDescription;
                }
                return status.ToString();

            case LoanReturnStatus status:
                string loanReturnDescription;
                if (LoanReturnDescriptions.TryGetValue(status, out loanReturnDescription))
                {
                    return loanReturnDescription;
                }
                return status.ToString();

            case LoanExtensionStatus status:
                string loanExtensionDescription;
                if (LoanExtensionDescriptions.TryGetValue(status, out loanExtensionDescription))
                {
                    return loanExtensionDescription;
                }
                return status.ToString();

            default:
                return value.ToString();
        }
    }

    ```

1. Erstellen Sie Ihre Lösung, um sicherzustellen, dass dabei keine Fehler entstanden sind.

    Es werden dieselben Warnungen angezeigt, die Sie am Anfang dieser Übung gesehen haben, aber es sollten keine Fehlermeldungen vorhanden sein.

## Umgestalten von Code mithilfe von Inline-Chat und der Chat-Ansicht in den Modi „Bearbeiten“ und „Agent“

LINQ ist ein leistungsfähiges Feature in C#, mit dem Sie Sammlungen, Datenbanken und XML-Dokumente einheitlich abfragen können. LINQ bietet im Vergleich zu herkömmlichen foreach-Schleifen eine präzisere und besser lesbare Möglichkeit zum Abfragen von Daten.

Dieser Abschnitt der Übung umfasst die folgenden Aufgaben:

- Gestalten Sie die Klasse „JsonData“ mithilfe von Inline-Chat um.
- Gestalten Sie die Klasse „JsonLoanRepository“ mithilfe der Chat-Ansicht im Modus „Bearbeiten“ um.
- Gestalten Sie die Klasse „JsonPatronRepository“ mithilfe der Chat-Ansicht im Modus „Agent“ um.

### Umgestalten der Klasse „JsonData“ mithilfe von Inline-Chat

Die JsonData-Klasse enthält die folgenden Datenzugriffsmethoden: GetPopulatedPatron, GetPopulatedLoan, GetPopulatedBookItem und GetPopulatedBook. Diese Methoden verwenden foreach-Schleifen, um Sammlungen zu durchlaufen und Objekte aufzufüllen. Sie können diese Methoden zum Verwenden von LINQ umgestalten, um die Lesbarkeit und Wartungsfreundlichkeit von Code zu verbessern.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie in der PROJEKTMAPPEN-EXPLORER-Ansicht das Projekt **Library.Infrastructure** und dann den Ordner **Daten**.

1. Öffnen Sie die Datei „JsonData.cs“.

1. Scrollen Sie nach unten, um die Methode**GetPopulatedPatron** zu finden.

    Die Methode **GetPopulatedPatron** ist dafür vorgesehen, ein vollständig gefülltes **Patron**-Objekt der Bibliothek zu erstellen. Sie kopiert die grundlegenden Eigenschaften des Kunden und füllt dessen Ausleih-Sammlung mit detaillierten Ausleih-Objekten.

1. Wählen Sie die **GetPopulatedPatron**-Methode aus.

    ```csharp

    public Patron GetPopulatedPatron(Patron p)
    {
        Patron populated = new Patron
        {
            Id = p.Id,
            Name = p.Name,
            ImageName = p.ImageName,
            MembershipStart = p.MembershipStart,
            MembershipEnd = p.MembershipEnd,
            Loans = new List<Loan>()
        };

        foreach (Loan loan in Loans!)
        {
            if (loan.PatronId == p.Id)
            {
                populated.Loans.Add(GetPopulatedLoan(loan));
            }
        }

        return populated;
    }

    ```

1. Öffnen Sie einen Inline-Chat, und geben Sie dann einen Prompt ein, durch den die Methode mit LINQ umgestaltet wird.

    ```plaintext
    #selection refactor selection to `return new Patron` using LINQ
    ```

1. Nehmen Sie sich einen Moment Zeit, um das vorgeschlagene Update zu überprüfen.

    Das vorgeschlagene Update sollte dem folgenden Code ähneln:

    ```csharp
    public Patron GetPopulatedPatron(Patron p)
    {
        return new Patron
        {
            Id = p.Id,
            Name = p.Name,
            ImageName = p.ImageName,
            MembershipStart = p.MembershipStart,
            MembershipEnd = p.MembershipEnd,
            Loans = Loans!
                .Where(loan => loan.PatronId == p.Id)
                .Select(GetPopulatedLoan)
                .ToList()
        };
    }
    ```

    Beachten Sie, dass eine LINQ-Abfrage verwendet wird, um die Foreach-Schleife zu ersetzen.

    Der LINQ-Code verwendet den Objektinitialisierer, um dem neuen **Patron**-Objekt Objekteigenschaften zuzuweisen. Dadurch entfällt die Notwendigkeit einer separaten **gefüllten** Instanz des **Patron**-Objekts. Insgesamt ist der aktualisierte Code kürzer und besser lesbar.

    Der Code verwendet den Kunden**p**, um dem neuen **Patron**-Objekt einige grundlegende Eigenschaften zuzuweisen. Anschließend wird die **Loans**-Sammlung mit den Ausleih-Elementen gefüllt, die dem Kunden-Parameter **p** zugeordnet sind, wobei jedes Ausleih-Element mithilfe der Methode **GetPopulatedLoan** aufbereitet wird.

    Sie können die LINQ-Codezeile aufschlüsseln, die die**Loans**-Sammlung füllt:

    - **Loans!**: Der Ausdruck **Loans!** greift auf die **Loans**-Sammlung zu. Der **!** Der Operator ist ein Null-Forgiving-Operator, der angibt, dass der Entwickler sicher ist, dass **Loans** nicht null ist. Sie sollten sicherstellen, dass **Loans** ordnungsgemäß initialisiert ist, bevor Sie die Methode **GetPopulatedPatron** aufrufen.

    - **.Where(loan => loan.PatronId == p.Id)**: Dieser Code filtert die Loan-Elemente, um nur diejenigen einzuschließen, die zum Kunden-Eingabeelement **p** gehören.

    - **.Select(GetPopulatedLoan)**: Dieser Code transformiert jedes gefilterte Loan-Element mithilfe der Methode **GetPopulatedLoan**.

    - **.ToList()**: Konvertiert das Ergebnis in eine **Liste\<Loan\>**.

1. Um das vorgeschlagene Update zu akzeptieren, wählen Sie **Annehmen** aus.

    Sie werden denselben Ansatz verwenden, um drei andere Methoden umzugestalten.

1. Überarbeiten Sie die Methoden **GetPopulatedLoan**, **GetPopulatedBookItem** und **GetPopulatedBook** nach demselben Ansatz.

    Verwenden Sie beispielsweise die folgenden Prompts, um die drei Methoden umzugestalten:

    Für die **GetPopulatedLoan**-Methode:

    ```plaintext

    #selection refactor selection to `return new Loan` using LINQ. Use `GetPopulatedBookItem` for the `BookItem` property. Use `Single` for BookItem and Patron properties.

    ```

    Für die **GetPopulatedBookItem**-Methode:

    ```plaintext

    #selection refactor selection to `return new BookItem` using LINQ. Use `GetPopulatedBook` and `Single` for the `BookItem` property.

    ```

    Für die **GetPopulatedBook**-Methode:

    ```plaintext

    #selection refactor selection to `return new Book` using LINQ. Use `Where` and `Select` for `Author` property. Use `First` author.

    ```

1. Nachdem Sie die vorgeschlagenen Updates akzeptiert haben, nehmen Sie sich einen Moment Zeit, um Ihre Codeänderungen zu überprüfen.

    Ihr aktualisierter Code sollte dem folgenden Code ähneln:

    ```csharp
    public Loan GetPopulatedLoan(Loan l)
    {
        return new Loan
        {
            Id = l.Id,
            BookItemId = l.BookItemId,
            PatronId = l.PatronId,
            LoanDate = l.LoanDate,
            DueDate = l.DueDate,
            ReturnDate = l.ReturnDate,
            BookItem = GetPopulatedBookItem(BookItems!.Single(bi => bi.Id == l.BookItemId)),
            Patron = Patrons!.Single(p => p.Id == l.PatronId)
        };
    }

    public BookItem GetPopulatedBookItem(BookItem bi)
    {
        return new BookItem
        {
            Id = bi.Id,
            BookId = bi.BookId,
            AcquisitionDate = bi.AcquisitionDate,
            Condition = bi.Condition,
            Book = GetPopulatedBook(Books!.Single(b => b.Id == bi.BookId))
        };
    }

    public Book GetPopulatedBook(Book b)
    {
        return new Book
        {
            Id = b.Id,
            Title = b.Title,
            AuthorId = b.AuthorId,
            Genre = b.Genre,
            ISBN = b.ISBN,
            ImageName = b.ImageName,
            Author = Authors!.Where(a => a.Id == b.AuthorId).Select(a => new Author {
                Id = a.Id,
                Name = a.Name
            }).First()
        };
    }
    ```

1. Verwenden Sie die intelligente Aktion **Erklären**, um eine Erklärung der LINQ-Abfragen anzuzeigen.

    Klicken Sie zur Auswahl der intelligenten Aktion **Erklären** mit der rechten Maustaste auf die ausgewählten Codezeilen und wählen Sie Copilot und dann im Kontextmenü **Erklären** aus. Die intelligente Aktion **Erklären** liefert eine detaillierte Erklärung des ausgewählten Codes. In diesem Fall werden die LINQ-Abfragen im Code verwendet.

    Sie können beispielsweise die intelligente Aktion **Erklären** auf die Methode **GetPopulatedBook** anwenden, um eine Erklärung der LINQ-Abfrage zu erhalten, die zum Auffüllen der Eigenschaft **Author** des Objekts **Book** verwendet wird.

    ```csharp
    Author = Authors!.Where(a => a.Id == b.AuthorId).Select(a => new Author {
        Id = a.Id,
        Name = a.Name
    }).First()
    ```

    Die intelligente Aktion **Erklären** liefert eine detaillierte Erklärung der LINQ-Abfrage, die zum Auffüllen der Eigenschaft **Author** des Objekts **Book** verwendet wird.

    Die Erklärung könnte z. B. wie folgt aussehen:

    ```plaintext

    The active selection is a C# code snippet that assigns a value to the Author property. This value is derived from a collection of Author objects named Authors. The code uses LINQ to filter and transform the data within this collection.
    
    First, the Authors! expression uses the null-forgiving operator (!) to indicate that Authors is not null, even if the compiler might think otherwise. This is a way to suppress nullable warnings. The Where method is then called on the Authors collection to filter the elements. The lambda expression a => a.Id == b.AuthorId is used to find all Author objects where the Id matches the AuthorId property of another object b.
    
    After filtering, the Select method is used to project each filtered Author object into a new Author object. This is done by creating a new instance of the Author class and copying the Id and Name properties from the original Author object.
    
    Finally, the First method is called to retrieve the first element from the resulting sequence. This means that the Author property will be assigned the first Author object that matches the filter criteria and has been projected into a new Author instance.
    
    This approach ensures that the Author property is set to a new Author object with the same Id and Name as the first matching Author in the Authors collection.

    ```

1. Erstellen Sie Ihre Lösung, um sicherzustellen, dass keine Fehler vorhanden sind.

### Umgestalten der Klasse „JsonLoanRepository“ mithilfe der Chat-Ansicht im Modus „Bearbeiten“

Die Klasse „JsonLoanRepository“ enthält die Datenzugriffsmethoden **GetLoan** und **UpdateLoan**. Sie gestalten diese beiden Methoden um, indem Sie foreach-Schleifen durch LINQ ersetzen, um die Lesbarkeit und Wartungsfreundlichkeit von Code zu verbessern.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie die Datei **JsonLoanRepository.cs**.

1. Wählen Sie die **GetLoan**-Methode aus.

    Die Methode **GetLoan** dient dazu, einen Loan anhand seiner ID abzurufen.

    ```csharp
    public async Task<Loan?> GetLoan(int id)
    {
        await _jsonData.EnsureDataLoaded();

        foreach (Loan loan in _jsonData.Loans!)
        {
            if (loan.Id == id)
            {
                Loan populated = _jsonData.GetPopulatedLoan(loan);
                return populated;
            }
        }

        return null;
    }
    ```

1. Stellen Sie sicher, dass die Chat-Ansicht im Modus **Bearbeiten** geöffnet ist.

    Wenn die Chat-Ansicht nicht geöffnet ist, wählen Sie **Chat umschalten** aus, um den Modus **Bearbeiten** einzustellen.

1. Geben Sie einen Prompt ein, die die Methode mithilfe von LINQ umgestaltet.

    Geben Sie beispielsweise die folgende Eingabeaufforderung ein:

    ```plaintext
    refactor the foreach using LINQ. Use Where, Select, and GetPopulatedLoan return the first matching loan.
    ```

1. Nehmen Sie sich einen Moment Zeit, um das vorgeschlagene Update zu überprüfen.

    Das vorgeschlagene Update sollte dem folgenden Code ähneln:

    ```csharp
    public async Task<Loan?> GetLoan(int id)
    {
        await _jsonData.EnsureDataLoaded();

        return _jsonData.Loans!
            .Where(l => l.Id == id)
            .Select(l => _jsonData.GetPopulatedLoan(l))
            .FirstOrDefault();

    }
    ```

    Der aktualisierte Code verwendet LINQ, um die Loan-Sammlung so zu filtern, dass nur das Loan-Element mit der angegebenen ID enthalten ist. Beachten Sie, dass **loan** als Nullwerte zulassend deklariert werden sollte (**Loan? loan**). Anschließend wird das Loan mithilfe der Methode **GetPopulatedLoan** umgewandelt und das erste Ergebnis wird zurückgegeben. Wenn kein passender Loan gefunden wird, gibt **FirstOrDefault** **null** zurück. Die Methode gibt dann dieses Loan-Objekt zurück, das null sein kann, wenn kein Loan mit der angegebenen **ID** existiert. Mit diesem Ansatz wird sichergestellt, dass das zurückgegebene Loan-Element vollständig mit allen erforderlichen dazugehörigen Daten aufgefüllt wird und einen umfassenden Überblick über den Loan-Datensatz bietet.

    GitHub Copilot könnte auch den folgenden Code vorschlagen, der funktionell gleichwertig ist:

    ```csharp
    public async Task<Loan?> GetLoan(int id)
    {
        await _jsonData.EnsureDataLoaded();

        Loan? loan = _jsonData.Loans!
            .Where(l => l.Id == id)
            .Select(l => _jsonData.GetPopulatedLoan(l))
            .FirstOrDefault();

        return loan;
    }
    ```

1. Um die aktualisierte Methode „GetLoan“ zu akzeptieren, klicken Sie auf **Behalten**.

1. Wählen Sie die **UpdateLoan**-Methode aus.

    ```csharp
    public async Task UpdateLoan(Loan loan)
    {
        Loan? existingLoan = null;
        foreach (Loan l in _jsonData.Loans!)
        {
            if (l.Id == loan.Id)
            {
                existingLoan = l;
                break;
            }
        }

        if (existingLoan != null)
        {
            existingLoan.BookItemId = loan.BookItemId;
            existingLoan.PatronId = loan.PatronId;
            existingLoan.LoanDate = loan.LoanDate;
            existingLoan.DueDate = loan.DueDate;
            existingLoan.ReturnDate = loan.ReturnDate;

            await _jsonData.SaveLoans(_jsonData.Loans!);

            await _jsonData.LoadData();
        }
    }
    ```

1. Geben Sie einen Prompt ein, die die Methode mithilfe von LINQ umgestaltet.

    Geben Sie beispielsweise die folgende Eingabeaufforderung ein:

    ```plaintext

    refactor selection using LINQ. find existing loan in `_jsonData.Loans!. replace existing loan.

    ```

1. Nehmen Sie sich einen Moment Zeit, um das vorgeschlagene Update zu überprüfen.

    Das vorgeschlagene Update sollte einem der folgenden Beispiele ähneln:

    ```csharp

    public async Task UpdateLoan(Loan loan)
    {
        var loans = _jsonData.Loans!;
        var index = loans.FindIndex(l => l.Id == loan.Id);

        if (index >= 0)
        {
            loans[index] = loan;
            await _jsonData.SaveLoans(loans);
            await _jsonData.LoadData();
        }
    }

    ```

    oder

    ```csharp

    public async Task UpdateLoan(Loan loan)
    {
        Loan? existingLoan = _jsonData.Loans!.FirstOrDefault(l => l.Id == loan.Id);

        if (existingLoan != null)
        {
            existingLoan.BookItemId = loan.BookItemId;
            existingLoan.PatronId = loan.PatronId;
            existingLoan.LoanDate = loan.LoanDate;
            existingLoan.DueDate = loan.DueDate;
            existingLoan.ReturnDate = loan.ReturnDate;

            await _jsonData.SaveLoans(_jsonData.Loans!);

            await _jsonData.LoadData();
        }
    }

    ```

    Der aktualisierte Code verwendet LINQ, um das vorhandene Loan-Element in der Loan-Sammlung zu finden. Anschließend wird das vorhandene Loan-Element mit den neuen Loan-Daten aktualisiert. Dann wird die aktualisierte Loan-Sammlung mit der Methode gespeichert, und die Daten werden neu geladen. Mit diesem Ansatz wird sichergestellt, dass die Loan-Daten korrekt aktualisiert werden und dass die Änderungen am Datenspeicher beibehalten werden.

    Sie können den Code auch hinzufügen, um sicherzustellen, dass die Daten geladen werden, bevor die Methode ausgeführt wird:

    ```csharp

    public async Task UpdateLoan(Loan loan)
    {
        await _jsonData.EnsureDataLoaded();

        Loan? existingLoan = _jsonData.Loans!.FirstOrDefault(l => l.Id == loan.Id);

        if (existingLoan != null)
        {
            existingLoan.BookItemId = loan.BookItemId;
            existingLoan.PatronId = loan.PatronId;
            existingLoan.LoanDate = loan.LoanDate;
            existingLoan.DueDate = loan.DueDate;
            existingLoan.ReturnDate = loan.ReturnDate;

            await _jsonData.SaveLoans(_jsonData.Loans!);

            await _jsonData.LoadData();
        }
    }

    ```

1. Um die aktualisierte Methode „UpdateLoan“ zu akzeptieren, wählen Sie **Behalten** aus.

1. Erstellen Sie Ihre Lösung, um sicherzustellen, dass dabei keine Fehler entstanden sind.

    Es werden Warnungen angezeigt. Sie können sie vorerst ignorieren.

### Umgestalten der Klasse „JsonPatronRepository“ mithilfe der Chat-Ansicht im Modus „Agent

Die Klasse **JsonPatronRepository** enthält die folgenden drei Methoden:

- SearchPatrons: Die Methode „SearchPatrons“ dient der Suche nach Patrons anhand ihres Namens. Diese Methode gibt eine sortierte Liste von Kunden zurück.
- GetPatron: Die Methode „GetPatron“ wird verwendet, um einen Kunden anhand seiner ID abzurufen. Diese Methode gibt ein aufgefülltes Kunden-Objekt zurück.
- UpdatePatron: Die Methode „UpdatePatron“ wird verwendet, um die Informationen eines Kunden zu aktualisieren. Diese Methode aktualisiert den vorhandenen Kunden mit den neuen Daten und speichert die aktualisierte Kundensammlung.

Jede der drei Methoden verwendet eine Foreach-Schleife, um die Kunden zu durchlaufen und Übereinstimmungen basierend auf der Sucheingabe oder ID zu finden.

Verwenden Sie die Chat-Ansicht im Modus Agent- um die Methoden umzugestalten und Foreach-Schleifen durch LINQ-Abfragen zu ersetzen – genauso wie bei den Klassen **JsonData** und **JsonLoanRepository**.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie die **JsonPatronRepository.cs**-Datei.

    Die Klasse **JsonPatronRepository** wurde entwickelt, um Bibliothekskunden zu verwalten.

1. Nehmen Sie sich kurz Zeit, um sich die drei Methoden in der Klasse **JsonPatronRepository** enthalten Methoden genauer anzusehen.

    Die Methode **SearchPatrons** dient der Suche nach Kunden anhand ihres Namens.

    ```csharp

    public async Task<List<Patron>> SearchPatrons(string searchInput)
    {
        await _jsonData.EnsureDataLoaded();

        List<Patron> searchResults = new List<Patron>();
        foreach (Patron patron in _jsonData.Patrons)
        {
            if (patron.Name.Contains(searchInput))
            {
                searchResults.Add(patron);
            }
        }
        searchResults.Sort((p1, p2) => String.Compare(p1.Name, p2.Name));

        searchResults = _jsonData.GetPopulatedPatrons(searchResults);

        return searchResults;
    }

    ```

    Beachten Sie, dass die Methode **SearchPatrons** eine Foreach-Schleife verwendet, um die Kunden zu durchlaufen und Übereinstimmungen basierend auf der Zeichenfolge **searchInput** zu finden. Die Methode sortiert die Ergebnisse dann nach Namen und gibt eine Liste mit aufgefüllten Kunden zurück.

    Die Methode **GetPatron** ist so konzipiert, dass das Kunden-Element zurückgegeben wird, das der angegebenen **ID** entspricht.

    ```csharp

    public async Task<Patron?> GetPatron(int id)
    {
        await _jsonData.EnsureDataLoaded();

        foreach (Patron patron in _jsonData.Patrons!)
        {
            if (patron.Id == id)
            {
                Patron populated = _jsonData.GetPopulatedPatron(patron);
                return populated;
            }
        }
        return null;
    }

    ```

    Beachten Sie, dass die Methode **GetPatron** eine Foreach-Schleife verwendet, um die Kunden zu durchlaufen und eine Übereinstimmung basierend auf dem Parameter **ID** zu finden. Die Methode gibt dann das aufgefüllte Kunden-Objekt zurück.

    Die Methode **UpdatePatron** dient dazu, den Benutzer mit der angegebenen **ID** zu aktualisieren.

    ```csharp

    public async Task UpdatePatron(Patron patron)
    {
        await _jsonData.EnsureDataLoaded();
        var patrons = _jsonData.Patrons!;
        Patron existingPatron = null;
        foreach (var p in patrons)
        {
            if (p.Id == patron.Id)
            {
                existingPatron = p;
                break;
            }
        }
        if (existingPatron != null)
        {
            existingPatron.Name = patron.Name;
            existingPatron.ImageName = patron.ImageName;
            existingPatron.MembershipStart = patron.MembershipStart;
            existingPatron.MembershipEnd = patron.MembershipEnd;
            existingPatron.Loans = patron.Loans;
            await _jsonData.SavePatrons(patrons);
            await _jsonData.LoadData();
        }
    }

    ```

    Beachten Sie, dass die Methode **UpdatePatron** eine Foreach-Schleife verwendet, um die Kunden zu durchlaufen und eine Übereinstimmung basierend auf dem Parameter **ID** zu finden. Die Methode aktualisiert dann den vorhandenen Kunden mit den neuen Daten und speichert die aktualisierte Kundensammlung.

1. Ändern Sie in der Chat-Ansicht den Modus zu **Agent**

    Der Modus „Agent“ wurde für die Ausführung von GitHub Copilot als Agent entwickelt. Sie können natürliche Sprache verwenden, um eine Aufgabe auf hoher Ebene zu erteilen. Der Agent wertet die zugewiesene Aufgabe aus, plant die erforderliche Arbeit und wendet die Änderungen auf Ihre Codebasis an.

    Der Modus „Agent“ verwendet eine Kombination aus Codebearbeitung und dem Aufruf von Tools, um die von Ihnen angegebene Aufgabe auszuführen. Während Ihre Anforderung verarbeitet wird, werden die Ergebnisse von Bearbeitungen und Tool-Aufrufen überwacht und es wird iterativ an der Behebung aller auftretenden Probleme gearbeitet. Wenn der Agent ein Problem nicht beheben kann, wird er Sie bitten, einzugreifen. Wenn der Agent beispielsweise mehrere Iterationen benötigt, um dasselbe Problem zu beheben, wird der Prozess angehalten und Sie werden aufgefordert, zusätzlichen Kontext bereitzustellen, um Ihre Anfrage zu klären oder den Vorgang abzubrechen.

    > **WICHTIG:** Wenn Sie die Chat-Ansicht im Modus „Agent“ verwenden, kann GitHub Copilot mehrere Premium-Anfragen stellen, um eine einzelne Aufgabe abzuschließen. Premium-Anfragen können durch benutzerinitiierte Eingabeaufforderungen und Folgeaktionen verwendet werden, die Copilot in Ihrem Auftrag ausführt. Die Gesamtzahl der verwendeten Premium-Anfragen hängt von der Komplexität des Vorgangs, der Anzahl der beteiligten Schritte und dem ausgewählten Modell ab.

1. Nehmen Sie sich kurz Zeit, um sich Gedanken über die Aufgabe zu machen, die Sie dem Agenten zuweisen möchten.

    Die Aufgabe besteht darin, die Klasse **JsonPatronRepository** umzugestalten. Ziel ist es, die Foreach-Schleifen durch LINQ-Abfragen zu ersetzen, die dasselbe Ergebnis wie der ursprüngliche Foreach-Code erzeugen.

    Sie können Ihre Erfahrung mit den Klassen **JsonData** und **JsonLoanRepository** nutzen, um die Aufgabe für den Agenten zu formulieren. Die LINQ-Abfragen sollten **Where**, **Select** und **FirstOrDefault** verwenden, um passende Kunden zu finden. Die LINQ-Abfragen sollten auch **OrderBy** verwenden, um die Sortierung des ursprünglichen Foreach-Codes beizubehalten.

1. Geben Sie den folgenden Prompt ein, um dem Agenten die Aufgabe zuzuweisen:

    ```plaintext

    Review the LINQ code used in the JsonData and JsonLoanRepository classes. Notice how Where, Select, and FirstOrDefault are used. Refactor the methods in the JsonPatronRepository class, replacing foreach loops with LINQ queries that produce the same result as the original foreach code. Use OrderBy to preserve sorting in original foreach code. Use ! to suppress nullability warnings when accessing collections.

    ```

    Dieser Prompt weist den Agenten an, die Klasse **JsonPatronRepository** umzugestalten. Er gibt an, dass die Foreach-Schleifen durch LINQ-Abfragen ersetzt werden sollen, die dasselbe Ergebnis wie der ursprüngliche Foreach-Code erzeugen. Er gibt auch an, dass **OrderBy** verwendet werden sollte, um die Sortierung des ursprünglichen Foreach-Codes beizubehalten, und das **!** verwendet werden sollte, um Warnungen zur NULL-Zulässigkeit beim Zugriff auf Sammlungen zu unterdrücken.

1. Überwachen Sie den Fortschritt des Agenten, während er den Code umgestaltet.

    Beachten Sie, dass der Agent die Aufgabe in mehreren Iterationen abschließt. Auf jeden Codebearbeitungsdurchlauf folgt ein Überprüfungsdurchlauf, bei dem der Code auf Probleme überprüft wird. Wenn ein Problem auftritt, wird der Code umgestaltet, um das Problem zu beheben. Wenn der Agent ein Problem nicht beheben kann, wird er Sie bitten, einzugreifen.

1. Nachdem der Agent seine Aufgabe beende hat, nehmen Sie sich kurz Zeit, um die vorgeschlagenen Updates zu überprüfen.

    Das vorgeschlagene Update sollte dem folgenden Code ähneln:

    ```csharp

    public async Task<List<Patron>> SearchPatrons(string searchInput)
    {
        await _jsonData.EnsureDataLoaded();

        var searchResults = _jsonData.Patrons!
            .Where(patron => patron.Name.Contains(searchInput))
            .OrderBy(patron => patron.Name)
            .ToList();

        return _jsonData.GetPopulatedPatrons(searchResults);
    }

    public async Task<Patron?> GetPatron(int id)
    {
        await _jsonData.EnsureDataLoaded();

        return _jsonData.Patrons!
            .Where(patron => patron.Id == id)
            .Select(patron => _jsonData.GetPopulatedPatron(patron))
            .FirstOrDefault();
    }

    public async Task UpdatePatron(Patron patron)
    {
        await _jsonData.EnsureDataLoaded();

        var existingPatron = _jsonData.Patrons!.FirstOrDefault(p => p.Id == patron.Id);
        if (existingPatron != null)
        {
            existingPatron.Name = patron.Name;
            existingPatron.ImageName = patron.ImageName;
            existingPatron.MembershipStart = patron.MembershipStart;
            existingPatron.MembershipEnd = patron.MembershipEnd;
            existingPatron.Loans = patron.Loans;

            if (_jsonData.Patrons != null)
            {
                await _jsonData.SavePatrons(_jsonData.Patrons);
                await _jsonData.LoadData();
            }
        }
    }

    ```

1. Wählen Sie **Behalten** aus, um alle Updates zu akzeptieren.

### Erstellen und Ausführen der Anwendung

Nachdem Sie den Code umgestaltet haben, ist es an der Zeit, die Anwendung zu erstellen und auszuführen, um sicherzustellen, dass alles ordnungsgemäß funktioniert. Außerdem müssen Sie die Anwendung testen, um sicherzustellen, dass der umgestaltete Code wie erwartet funktioniert.

1. Um die Lösung zu bereinigen, klicken Sie mit der rechten Maustaste auf **AccelerateAppDevGitHubCopilot** und wählen Sie dann **Bereinigen** aus.

    Mit dieser Aktion werden alle Buildartefakte des vorherigen Build entfernt. Durch das Bereinigen der Lösung werden die Dateien mit den JSON-Daten währenddessen (im Ausgabeverzeichnis) effektiv auf ihre ursprünglichen Werte zurückgesetzt.

1. Stellen Sie sicher, dass die Projektmappe erfolgreich erstellt wird.

    Um beispielsweise die Projektmappe in der PROJEKTMAPPEN-EXPLORER-Ansicht zu erstellen, klicken Sie mit der rechten Maustaste auf **AccelerateDevGHCopilot** und wählen Sie anschließend **Erstellen** aus.

    Es werden einige Warnungen angezeigt, es sollten aber keine Fehler auftreten.

1. Klicken Sie zum Ausführen der Anwendung mit der rechten Maustaste auf **Library.Console**, wählen Sie **Debuggen** aus, und wählen Sie anschließend **Neue Instanz starten** aus.

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

In dieser Übung haben Sie gelernt, wie Sie Code mithilfe von GitHub Copilot umgestalten. Sie haben die Chat-Ansicht im Modus „Bearbeiten“ verwendet, um die Klasse **EnumHelper** umzugestalten und die Reflexion durch statische Wörterbücher zu ersetzen. Sie haben auch den Inline-Chat- und Modus „Bearbeiten“ verwendet, um die Klassen **JsonData** und **JsonLoanRepository** umzugestalten und Foreach-Schleifen durch LINQ-Abfragen zu ersetzen. Schließlich haben Sie den Modus „Agent“ verwendet, um die Klasse **JsonPatronRepository** umzugestalten und Foreach-Schleifen durch LINQ-Abfragen zu ersetzen.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich kurz Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder Ihrem GitHub Copilot-Abonnement vorgenommen haben, die Sie nicht beibehalten möchten. Falls Sie Änderungen vorgenommen haben, machen Sie diese jetzt wieder rückgängig.
