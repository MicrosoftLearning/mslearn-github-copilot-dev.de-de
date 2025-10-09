---
lab:
  title: Übung – Einführung in das Stimmungs-Coding mit GitHub Copilot Agent
  description: 'Erfahren Sie, wie Sie mit Vibe Coding und dem GitHub Copilot Agent eine Prototyp-App erstellen.'
---

# Einführung in das Vibe Coding mit GitHub Copilot Agent

Vibe Coding ist ein Ansatz für das Programmieren mit KI-Tools, z. B. GitHub Copilot Agent, zum Generieren von Software. Anstatt Code manuell zu schreiben, liefert der Benutzer eine Beschreibung der beabsichtigten App in natürlicher Sprache bereit und die KI generiert den entsprechenden Code. Dadurch wandelt sich die Rolle des Programmierers vom traditionellen Programmieren hin zum Anleiten, Testen und Verfeinern der KI-generierten Ergebnisse.

In dieser Übung erstellen Sie mithilfe von Vibe Coding und dem GitHub Copilot Agent einen Prototyp einer Online-Shopping-App. Ihre Prototyp-App umfasst die folgenden Seiten: Produkte, Produktdetails, Warenkorb und Kasse. Die App umfasst eine grundlegende Navigation zwischen den Seiten sowie einen begrenzten Datensatz, um die Funktionen der App zu veranschaulichen. Der Prototyp umfasst keine Backend-Funktionalität, z. B. Benutzerauthentifizierung, Zahlungsverarbeitung oder Datenbankintegration.

Diese Übung dauert ca. **30** Minuten.

> **WICHTIG:** Um diese Übung abzuschließen, benötigen Sie ein eigenes GitHub-Konto und ein GitHub Copilot-Abonnement. Falls Sie kein GitHub-Konto haben, können Sie sich für ein kostenloses Einzelkonto <a href="https://github.com/" target="_blank">registrieren</a> und den GitHub Copilot Free-Plan verwenden, um die Übung abzuschließen. Wenn Sie in Ihrer Übungsumgebung Zugriff auf ein GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- oder GitHub Copilot Enterprise-Abonnement haben, können Sie Ihr vorhandenes GitHub Copilot-Abonnement für diese Übung verwenden.

## Vor der Installation

Ihre Übungsumgebung muss die folgenden Voraussetzungen erfüllen:

- Visual Studio Code.
- Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot.

Wenn Sie einen lokalen PC als Übungsumgebung für diese Übung verwenden, gilt Folgendes:

- Sie können die Visual Studio Code-Installer-Datei unter der folgenden URL herunterladen: <a href="https://code.visualstudio.com/download" target="_blank">Visual Studio Code herunterladen</a>.

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen Sie den folgenden Link in einem Browser: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

Wenn Sie eine gehostete Übungsumgebung verwenden, die diese Übung unterstützt:

- Wenn Sie Hilfe beim Aktivieren Ihres GitHub Copilot-Abonnements in Visual Studio Code benötigen, öffnen Sie einen Browser und fügen Sie die folgende URL in die Navigationsleiste ein: <a href="https://go.microsoft.com/fwlink/?linkid=2320158" target="_blank">Aktivieren von GitHub Copilot in Visual Studio Code</a>.

## Übungsszenario

Sie sind ein Unternehmer, der mittels Vibe Coding den Prototyp einer Shopping-App erstellen möchte. Ihr erster Prototyp muss die grundlegenden Funktionen aufzeigen, die Benutzer von einer Onlineshopping-App erwarten, sowie die spezifischen Funktionen, die Sie vorgesehen haben.

Die folgenden grundlegenden Spezifikationen bilden die Grundlage für den Beginn des Entwicklungsprozesses:

1. Verwenden Sie HTML, CSS und JavaScript, um eine clientseitige Web-App zu erstellen.
2. Fügen Sie die folgenden Webseiten hinzu: Products, ProductDetails, ShoppingCart und Checkout.
3. Ermöglichen Sie die Navigation zwischen den Seiten.

Diese Übung umfasst die folgenden Aufgaben:

1. **Definieren von Produktanforderungen**: Verwenden Sie GitHub Copilot, um Ihre grundlegenden Spezifikationen zu detaillierteren Produktanforderungen auszuarbeiten.

1. **Erstellen einer ersten Prototyp-App**: Verwenden Sie den GitHub Copilot Agent und Ihre Produktanforderungen, um eine erste Prototyp-App zu erstellen.

1. **Verfeinern Sie Ihre Prototyp-App**: Verwenden Sie den GitHub Copilot Agent um eine Reihe iterativer Aktualisierungen vorzunehmen, die das Benutzererlebnis verfeinern und sicherstellen, dass Ihre App die vorgesehenen Anforderungen erfüllt.

> **HINWEIS:** Eine Prototyp-App ist ein frühes, interaktives Modell einer Anwendung, das das visuelle Design und das Benutzererlebnis veranschaulicht. In dieser Übung soll Ihre Prototyp-App grundlegende Funktionen umsetzen und einige übergeordnete Anwendungsfälle abdecken.

## Definieren von Produktanforderungen

Damit ein KI-Agent die von Ihnen vorgesehene App entwickeln kann, muss er Ihre Produktanforderungen und das beabsichtigte Benutzererlebnis verstehen. Sie können Ihre Absichten mit einem der folgenden Prozesse an den GitHub Copilot Agent kommunizieren:

- **Zuerst Code schreiben und anschließend iterieren, um die Anforderungen zu definieren**: Bei diesem Ansatz beginnen Sie mit minimalen grundlegenden Spezifikationen und steigen direkt ins Programmieren ein. Im Verlauf der Entwicklung nimmt die App in iterativen Zyklen nach und nach Gestalt an, wobei die Funktionen und das Benutzererlebnis nach und nach herausgearbeitet werden. Bei diesem Ansatz besteht die Gefahr, dass Sie von Ihrer ursprünglichen Vision abweichen, wenn Sie sich mit den von der KI implementierten Funktionen auseinandersetzen, was sowohl Vor- als auch Nachteile haben kann. Ein KI-gestützter Prozess kann unerwartet zeitaufwändig werden und möglicherweise nicht zu den gewünschten Ergebnissen führen, insbesondere wenn die anfänglichen Spezifikationen vage oder offen formuliert sind.

- **Ausarbeiten der Anforderungen, bevor mit dem Programmieren begonnen wird**: Dieser Ansatz sorgt von Anfang an für Klarheit. Sie arbeiten mit der KI zusammen, um ein Dokument mit Produktanforderungen (PRD) zu entwerfen, bevor mit dem Programmieren beginnen. Das PRD umreißt den Zweck, die Zielgruppe, die wichtigsten Funktionen und die technischen Einschränkungen der App. Indem Sie von Anfang an eine klare Vision festlegen, geben Sie der KI eine solide Grundlage, um Code zu generieren, der sich an Ihren Zielen orientiert. So verringern Sie Unklarheiten und erhöhen die Wahrscheinlichkeit, dass die App entsteht, die Sie wirklich vorgesehen haben.

Bei dieser Aufgabe verwenden Sie GitHub Copilot, um Ihre grundlegenden Spezifikationen auszuwerten und Produktanforderungen für Ihre Prototyp-App zu entwickeln.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Öffnen Sie Visual Studio Code.

1. Wählen Sie im Menü „Datei“ die Option **Ordner zum Arbeitsbereich hinzufügen** aus.

1. Navigieren Sie im Dialogfeld **Ordner zum Arbeitsbereich hinzufügen** zu einem leicht auffindbaren Speicherort, erstellen Sie einen neuen Ordner namens **VibeCoding-PrototypeApp** und wählen Sie dann **Hinzufügen** aus.

    Der Speicherort sollte außerhalb eines vorhandenen Git-Repositorys liegen und leicht auffindbar sein. Wenn Sie beispielsweise einen Windows-PC verwenden, können Sie einen neuen Ordner namens **VibeCoding-PrototypeApp** auf Ihrem **Desktop** oder im Verzeichnis **Dokumente** erstellen.

    Nach Abschluss dieser Übung können Sie das Codeprojekt entweder archivieren oder löschen.

1. Öffnen Sie die Chat-Ansicht von GitHub Copilot.

    Sie können die die Chat-Ansicht öffnen, indem Sie das GitHub Copilot-Symbol oben in der Mitte des Visual Studio Code-Fensters rechts neben dem Suchtextfeld auswählen.

1. Stellen Sie sicher, dass der Chatmodus auf **Fragen** eingestellt und das Modell **GPT-4.1** ausgewählt ist.

    Die Dropdown-Menüs *Modus festlegen* und *Model auswählen* befinden sich in der unteren linken Ecke der Chat-Ansicht.

    **GitHub Copilot-Modi**: Auch wenn sich ihre Funktionen überschneiden, ist jeder der Chatmodi (Fragen, Bearbeiten und Agent) für einen bestimmten Zweck optimiert:

    - **Fragen**: Verwenden Sie diesen Modus, um GitHub Copilot Fragen zu Ihrer Codebasis zu stellen. Sie können den Modus „Fragen“ verwenden, um Code zu erläutern, Änderungen vorzuschlagen oder Informationen zur Codebasis bereitzustellen.
    - **Bearbeiten**: Verwenden Sie diesen Modus, um bestimmte Codedateien in Ihrem Arbeitsbereich zu bearbeiten. Sie können den Modus „Bearbeiten“ verwenden, um Code umzugestalten, Kommentare hinzuzufügen, Tests zu implementieren oder Ihren Apps neue Funktionen hinzuzufügen.
    - **Agent**: Verwenden Sie diesen Modus, um GitHub Copilot als Agent auszuführen. Sie können den Modus „Agent“ verwenden, um Programmieraufgaben autonom ausführen zu lassen.

    **Unterstützte Modelle**: GitHub Copilot unterstützt mehrere Modelle mit unterschiedlichen Stärken. Einige Modelle priorisieren Geschwindigkeit und Kosteneffizienz, während andere für Genauigkeit, Gründe oder das Arbeiten mit multimodalen Eingaben (z. B. Bilder und Code) optimiert sind. GitHub Copilots kostenloser Plan unterstützt derzeit GPT-4.1, GPT-4o, o3-mini, Claude Sonnet 3.5 und Gemini 2.0 Flash. Das Modell GPT-4.1 ist eine gute Wahl für diese Übung, da es schnelle, präzise Code-Vervollständigungen und Erklärungen generiert, visuelle Eingaben unterstützt und komplexe Aufgaben effektiv bewältigt.

    > **HINWEIS:** Die Auswahl eines anderen Modells wirkt sich auf die Antworten aus, die Sie von GitHub Copilot erhalten. Das Modell GPT-4.1 wird für diese Übung empfohlen, Sie können die Übung jedoch auch mit anderen Modellen wiederholen, um zu sehen, wie sie auf Ihre Prompts reagieren.

1. Geben Sie in der Chatansicht die folgende Eingabeaufforderung ein:

    ```plaintext
    I want to create a product requirements document (PRD) for an app that I'll develop using a vibe coding process. I want the PRD to include information about the app's purpose, target audience, features, and technical requirements. I've defined the following high-level parameters for my app: 1 - Use HTML, CSS, and JavaScript to create a client-side web app. 2 - Include the following web pages: Products, ProductDetails, ShoppingCart, and Checkout. 3 - Enable navigation between pages. I want the prototype app to implement basic features and satisfy a small number of high-level use cases. The prototype should implement the following: basic use case functionality, simple navigation, a sample dataset, and basic styling. I'll be adding the PRD to the chat context, then asking GitHub Copilot Agent to create the prototype app. What sections should I include in the PRD to enable GitHub Copilot Agent to create my envisioned prototype?
    ```

1. Überprüfen Sie die von GitHub Copilot generierte Antwort.

    Ihre Antwort könnte zum Beispiel dem folgenden Muster ähneln:

    ```md
    To enable GitHub Copilot Agent to create your envisioned prototype app, your Product Requirements Document (PRD) should include the following sections:
    
    1. App Overview / Purpose  
       - Briefly describe what the app does and its main goal.
    
    2. Target Audience  
       - Define who will use the app (e.g., general consumers, online shoppers, etc.).
    
    3. Core Features  
       - List and describe the main features (e.g., view products, view product details, add to cart, checkout).
    
    4. Page Descriptions  
       - Detail each required page (Products, ProductDetails, ShoppingCart, Checkout) and what should be displayed or possible on each.
    
    5. Navigation  
       - Explain how users move between pages (e.g., navigation bar, links, buttons).
    
    6. Sample Data  
       - Describe the sample dataset (e.g., a few example products with name, price, description, image).
    
    7. Technical Requirements  
       - Specify technologies to use (HTML, CSS, JavaScript, client-side only, no backend).
       - Mention any libraries or frameworks (if any) or state "vanilla JS".
    
    8. Styling  
       - Indicate the level of styling (e.g., basic, clean, minimal, responsive).
    
    9. Use Cases / User Flows  
       - List a few high-level use cases (e.g., browse products, view details, add to cart, proceed to checkout).
    
    10. Out of Scope  
        - Clarify what is not required (e.g., user authentication, payment processing, backend integration).
    
    Including these sections will give clear, actionable guidance for building your prototype app.
    ```

    > **HINWEIS:** Machen Sie sich keine Sorgen, wenn Ihre Antwort andere Abschnittstitel enthält oder die Abschnitte in einer anderen Reihenfolge angeordnet sind. Die Antworten, die KI-Tools generieren, unterscheiden sich oft leicht von Sitzung zu Sitzung. Das ausgewählte KI-Modell, Ihr Chatverlauf und der Kontext Ihrer Chatsitzung können die Antworten ebenfalls beeinflussen.

1. Nehmen Sie sich ein paar Minuten Zeit, um sich zu überlegen, welche Informationen für die einzelnen Abschnitte des PRD erforderlich sind.

    Ein gut definiertes PRD trägt dazu bei, dass der GitHub Copilot Agent Ihre Vision für die App klar versteht. Das PRD sollte ausreichend Details enthalten, damit der Agent eine Prototyp-App erstellen kann, die Ihren Anforderungen und dem beabsichtigten Benutzererlebnis entspricht. Ihr PRD sollte auf den grundlegenden Spezifikationen aufbauen, die weiter oben in dieser Übung aufgeführt sind.

    Wenn Sie unsicher sind, welche Informationen in einem bestimmten Abschnitt enthalten sein sollen, können Sie den GitHub Copilot Agent bitten, den Inhalt für diesen Abschnitt zu erstellen. Sie können GitHub Copilot beispielsweise nach Ideen fragen, was in den Abschnitten „Core Features“ oder „Use Cases“ enthalten sein sollte.

    > **Tipp**: Sie können einen Text in natürlicher Sprache eingeben, der die Anforderungen Ihrer App beschreibt, und GitHub Copilot formatiert diese Informationen dann als PRD. Sie können GitHub Copilot auch verwenden, um das PRD zu überprüfen und zu aktualisieren und sicherzustellen, dass es den für den GitHub Copilot Agent erforderlichen Detailgrad zum Erstellen des Prototyps enthält.

1. Geben Sie in der Chatansicht die folgende Eingabeaufforderung ein:

    ```plaintext
    The PRD sections that you suggested look good. Here's some information that should help you construct the PRD:

    My prototype app targets online shoppers interested in ordering my products. The prototype should include the following:

    - A dynamic user interface that scales automatically to appear correctly on large or small screens (desktop and phone devices).
    - A simple dataset that defines 10 fruit products. The dataset should include: product name, description, price per unit (where unit could be the number of items, ounces, pounds, etc.). If possible, I want to include a simple image (an emoji) that represents the product.
    - A navigation menu on the left side of the screen that allows users to navigate between the Products, ProductDetails, ShoppingCart, and Checkout pages.
    - Basic styling that makes the user interface visually appealing, but it doesn't need to be fully responsive or polished.

    The prototype app won't include any backend functionality, such as user authentication, payment processing, or database integration. It will be a static prototype that demonstrates the basic concepts.

    Here's a description of the user interface:

    - The Products page should display a list of products with basic information such as product name, price per unit, and an image (an emoji). The Products page should also provide a way to select a desired quantity of a product and an option to add selected items to the shopping cart.
    - The ProductDetails page should display detailed information about a product when the product is selected from the Products page. The ProductDetails page should display the product name, a description of the product, the price per unit, and an image (an emoji) representing the product. The ProductDetails page should also provide a way to navigate back to the Products page.
    - The ShoppingCart page should display the list of products added to the cart. The list should include the product name, quantity, and total price for that product. The ShoppingCart page should also provide a way to update the quantity of each product that's in the cart, and an option to remove products from the cart.
    - The Checkout page should display a summary of the products being purchased, including product name, quantity, and price. The total price should be clearly displayed along with the option to "Process Order".
    - The left-side navigation menu should provide basic navigation between pages. The navigation bar should collapse down to display a one or two letter abbreviation when the display width drops below 300 pixels. The navigation bar should allow users to navigate between the app pages.
    ```

    GitHub Copilot sollte eine Antwort erstellen, die ein vorgeschlagenes PRD auf Grundlage der von Ihnen bereitgestellten Informationen enthält. Die Antwort sollte die Abschnitte enthalten, die Sie zuvor durchgesehen haben, und für jeden Abschnitt Inhalte auf Grundlage der von Ihnen bereitgestellten Informationen bereitstellen.

1. Wählen Sie in der Chat-Ansicht den Modus **Agent** aus.

    Das Dropdown-Menü „Modus festlegen“ befindet sich in der unteren linken Ecke der Chat-Ansicht.

1. Geben Sie in der Chatansicht die folgende Eingabeaufforderung ein:

    ```md
    Create a markdown file named VibeCodingPRD.md using your suggested sections and the inputs that I've provided.
    ```

1. Um die vorgeschlagene Datei VibeCodingPRD.md in der Chat-Ansicht zu speichern, wählen Sie **Behalten** aus.

1. Nehmen Sie sich einige Minuten Zeit, um die PRD-Datei zu überprüfen.

    Die vorgeschlagene PRD-Datei sollte für diese Übung ausreichend sein. Wenn Sie jedoch Lücken oder Unstimmigkeiten feststellen oder weitere Informationen hinzufügen möchten, können Sie die Datei direkt in Visual Studio Code bearbeiten. Sie können GitHub Copilot auch bitten, das PRD durch das Generieren zusätzlicher Informationen oder das Implementieren von Präzisierungen zu verfeinern.

1. Öffnen Sie die EXPLORER-Ansicht in Visual Studio Code.

1. Geben Sie in der Chatansicht die folgende Eingabeaufforderung ein:

    ```md
    Can you create low-fidelity wireframe diagrams (or text-based layouts) that represent the web pages and navigation bar (expanded and collapsed) for my prototype app? Use the PRD that I've provided as a reference.
    ```

    Der GitHub Copilot Agent sollte textbasierte Low-Fidelity-Layouts erstellen, die die Benutzeroberfläche Ihrer Prototyp-App darstellen. Diese „Wireframe-Diagramme“ sollten dabei helfen, die Benutzeroberfläche sowie die Interaktion der Benutzer mit der App zu definieren.

    Die Antwort kann z. B. wie folgt aussehen:

    ```md
    Certainly! Here are text-based, low-fidelity wireframe layouts for each main page of your prototype app, based on your PRD:

    ---

    ### 1. Products Page
    

    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | 🍎 Apple         $1.00/each   [Qty: - 1 +] [Add]     |
    | 🍌 Banana        $0.50/each   [Qty: - 1 +] [Add]     |
    | 🍊 Orange        $0.80/each   [Qty: - 1 +] [Add]     |
    | ... (other fruits)                                  |
    +------------------------------------------------------+
    
    ---
    
    ### 2. ProductDetails Page
    
    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | 🍎 Apple                                         |
    | Fresh, crisp apples                              |
    | Price: $1.00/each                               |
    | [Qty: - 1 +] [Add to Cart]                      |
    | [Back to Products]                              |
    +------------------------------------------------------+
    
    ---
    
    ### 3. ShoppingCart Page
    
    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | Cart Items:                                       |
    | 🍎 Apple   Qty: [ - 2 + ]  $2.00   [Remove]        |
    | 🍌 Banana  Qty: [ - 1 + ]  $0.50   [Remove]        |
    | -------------------------------------------------- |
    | [Update Cart]                                     |
    | [Proceed to Checkout]                             |
    +------------------------------------------------------+
    
    ---
    
    ### 4. Checkout Page
    
    +------------------------------------------------------+
    | [Nav] Products | ProductDetails | Cart | Checkout    |
    +----------------+-------------------------------------+
    | Order Summary:                                     |
    | 🍎 Apple   x2   $2.00                              |
    | 🍌 Banana  x1   $0.50                              |
    | -------------------------------------------------- |
    | Total: $2.50                                      |
    | [Process Order]                                   |
    +------------------------------------------------------+
    
    ---
    
    ### 5. Navigation Bar (Left Side, Collapsible)
    
    +-------------------+      +-----+
    | Products          |      | P   |
    | ProductDetails    |      | D   |
    | Cart              |      | C   |
    | Checkout          |      | CO  |
    +-------------------+      +-----+
    (Full width)             (Collapsed <300px)
    
    ---
    
    These wireframes provide a clear, simple structure for each page and the navigation menu, matching your requirements. If you want these added to your PRD or as a separate markdown file, let me know!
    ```

    > **HINWEIS:** Es gibt viele andere Möglichkeiten zum Erstellen von Wireframe-Diagrammen. Für einen KI-basierten Ansatz, der zu Ihrem Vibe-Coding-Prozess passt, können Sie Microsofts M365 Copilot verwenden. Geben Sie M365 Copilot einfach eine Beschreibung Ihrer App (den Inhalt Ihres PRD) und bitten Sie die KI, Low-Fidelity-Wireframes als Bilder zu erstellen. Für manuell erstellte High-Fidelity-Wireframes können Sie ein UI/UX-Design-Tool wie Figma verwenden.

1. Geben Sie in der Chatansicht die folgende Eingabeaufforderung ein:

    ```md
    Save the low-fidelity wireframe diagrams as text files, one file for each web page and one for navigation.
    ```

1. Überwachen Sie die Chat-Ansicht, um sicherzustellen, dass alle Dateien gespeichert werden, und wählen Sie anschließend **Behalten** aus.

1. Nehmen Sie sich ein paar Minuten Zeit, um die Wireframe-Diagramme zu überprüfen.

    Wenn Sie offensichtliche Probleme feststellen, die Sie korrigieren möchten, können Sie die Wireframe-Diagramme direkt in Visual Studio Code bearbeiten. Sie können GitHub Copilot auch bitten, die Wireframe-Diagramme zu verfeinern.

    Für diese Übung müssen Ihre Wireframes (Text-Layouts) nicht exakt sein und die vorgeschlagenen Wireframes sollten ohne Änderungen ausreichen. Wenn Sie jedoch später während der Übung auf Probleme stoßen, die Sie auf die Wireframe-Diagramme zurückführen, können Sie den GitHub Copilot Agent bitten, die Wireframe-Diagramme zu verfeinern.

    > **Tipp**: Wenn Sie unsicher sind, wie Sie ein Wireframe-Diagramm interpretieren können, oder ob eines der Wireframe-Diagramme möglicherweise fehlerhaft ist, bitten Sie GitHub Copilot, das/die Wireframe-Diagramm(e) zu erläutern. Beispielsweise können Sie den GitHub Copilot Agent bitten, "die Wireframe-Diagramme zu überprüfen und sie zu nutzen, um das Layout der Benutzeroberfläche sowie die Interaktion des Benutzers mit der App zu erläutern." Wenn die Erklärung von GitHub Copilot nicht Ihren Erwartungen entspricht, können Sie den GitHub Copilot Agent bitten, die Wireframe-Diagramme zu aktualisieren, damit sie besser mit dem beabsichtigten Benutzererlebnis übereinstimmen.

## Erstellen einer ersten Prototyp-App

GitHub Copilot Agent kann Produktanforderungen und Wireframe-Diagramme verwenden, um eine Prototyp-Anwendung zu entwickeln. Wenn Sie ausreichend detaillierte Produktanforderungen und Wireframe-Diagramme bereitstellen, hilft das dem Agenten, das Benutzererlebnis, die App-Funktionen und die Designziele zu verstehen, die Sie für Ihre App vorgesehen haben.

- Das PRD enthält detaillierte Informationen über den Zweck, die Zielgruppe, die Funktionen und die technischen Anforderungen der App.
- Die Wireframe-Diagramme zeigen die beabsichtigte Benutzeroberfläche und dienen dazu, die Benutzerinteraktionen zu beschreiben.

Bei dieser Aufgabe verwenden Sie den GitHub Copilot Agent, um auf Grundlage des von Ihnen erstellten PRD und der von Ihnen erstellten Wireframe-Diagramme eine erste Prototyp-App zu entwickeln.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Erstellen Sie in Visual Studio Code einen neuen Ordner namens **ShoppingApp** im Ordner „VibeCoding-PrototypeApp“.

    Der GitHub Copilot Agent benötigt einen leeren Ordner, der als Arbeitsbereich für die neuen App-Dateien dient.

    Die EXPLORER-Ansicht in Visual Studio Code sollte etwa wie folgt aussehen:

    ```plaintext
    UNTITLED (WORKSPACE)
    └── VibeCoding-PrototypeApp
        ├── ShoppingApp
        ├── VibeCodingPRD.md
        ├── wireframe-checkout.txt
        ├── wireframe-navigation.txt
        ├── wireframe-product-details.txt
        ├── wireframe-products.txt
            ```└── wireframe-shopping-cart.txt
    ```

1. Fügen Sie dem Chat-Kontext das PRD und die Wireframe-Diagramme hinzu.

    Durch das Hinzufügen dieser Dateien zum Chat-Kontext wird der GitHub Copilot Agent angewiesen, die Dateien beim Generieren einer Antwort als Referenz zu verwenden.

    Sie können dem Chat-Kontext Dateien hinzufügen, indem Sie sie aus der EXPLORER-Ansicht per Drag-and-Drop in die Chat-Ansicht ziehen oder indem Sie die Schaltfläche **Kontext hinzufügen** unten links in der Chat-Ansicht auswählen.

1. Wählen Sie in der EXPLORER-Ansicht den Ordner **ShoppingApp** aus.

1. Geben Sie in der Chatansicht die folgende Eingabeaufforderung ein:

    ```md
    I want you to create a prototype shopping app using the information in my PRD and wireframe diagrams. Create the prototype app in the selected 'ShoppingApp' folder. The prototype should implement the following: basic use case functionality, simple navigation, a sample dataset, and basic styling. After creating the prototype app, add a '.github/copilot-instructions.md' file to the workspace. Add the contents of the PRD and wireframe files to the 'copilot-instructions.md' file.
    ```

    Der GitHub Copilot Agent verwendet diesen Prompt, um eine erste Prototyp-App basierend auf den von Ihnen definierten Anforderungen zu generieren.

    - Der Agent überprüft den Ordner **ShoppingApp**, um sicherzustellen, dass er leer ist und als Arbeitsbereich verwendet werden kann
    - Der Agent verwendet das PRD und die Wireframe-Diagramme, um die Dateien für die Prototyp-App zu erstellen. Die folgenden Dateien werden im Ordner **ShoppingApp** erstellt:

        - **app.js**: Enthält den JavaScript-Code, der die Funktionen der App umsetzt, z. B. die Verwaltung des Produktkatalogs, des Warenkorbs und der Navigation.
        - **index.html**: Dient als Einstiegspunkt für die Webanwendung, indem sie die Grundstruktur einrichtet und Stylesheets sowie Skripts verknüpft.
        - **styles.css**: Liefert das visuelle Layout und das dynamische Design für die Prototyp-Web-App.

    - Der Agent fügt dem Arbeitsbereich die Datei **.github/copilot-instructions.md** hinzu und ergänzt die Datei **copilot-instructions.md** anschließend um den Inhalt des PRD und der Wireframe-Diagrammdateien.

    > **TIPP**: Sie können benutzerdefinierte Anweisungen im Arbeitsbereich oder Repository in der Datei .github/copilot-instructions.md speichern. Mit benutzerdefinierten Anweisungen können Sie allgemeine Richtlinien oder Regeln festlegen, damit die Antworten Ihren spezifischen Coding-Praktiken und Ihrem Tech-Stack entsprechen. Statt diesen Kontext manuell in jede Chat-Anfrage einzufügen, fügen benutzerdefinierte Anweisungen diese Informationen automatisch in jede Chat-Anfrage ein. Diese Anweisungen gelten nur für den Arbeitsbereich, in dem sich die Datei befindet.

1. Überwachen Sie die Chat-Ansicht, um den Fortschritt des Agents nachzuverfolgen, während er an Ihrer Prototyp-App arbeitet.

    > **HINWEIS:** Obwohl GitHub Copilot Agent Aufgaben als autonomer Agent ausführt, kann er beim Ausführen bestimmter Aufgaben um Unterstützung bitten. Um den Agenten zu unterstützen, antworten Sie auf alle Eingabeaufforderungen, die in der Chat-Ansicht erscheinen. Wenn der Agent beispielsweise die Berechtigung zum Ausführen eines Befehls im Terminal anfragt, wählen Sie **Ausführen** aus, damit der Agent den Befehl ausführen kann. Wenn der Agent um Klarstellung zu Ihren Anforderungen bittet, geben Sie eine Antwort, die dem Agenten hilft, Ihre Anforderungen zu verstehen.

1. Wählen Sie in der Chat-Ansicht die Option **Behalten** aus, um die Dateien der Prototyp-App zu speichern.

1. Öffnen Sie den Ordner **ShoppingApp**.

    Der Ordner sollte folgende Dateien enthalten:

    ```plaintext
    ShoppingApp
    ├── .github
    │   └── copilot-instructions.md
    ├── app.js
    ├── index.html
    ├── styles.css
    ```

1. Nehmen Sie sich ein paar Minuten Zeit, um die einzelnen Code-Dateien durchzusehen.

    - Die Datei **index.html** dient als Einstiegspunkt für eine Webanwendung. Sie richtet die Grundstruktur der App ein und verknüpft die Stylesheet- und Skriptdateien.
    - Die Datei **styles.css** stellt das visuelle Layout und das dynamische Design für Ihre Prototyp-Web-App bereit.
    - Die Datei **app.js** enthält den JavaScript-Code, der den Produktkatalog, den Warenkorb, die Navigation und das Rendern der Benutzeroberfläche verwaltet.

    Wenn es zeitlich möglich ist, bitten Sie den GitHub Copilot, für jede Datei eine detaillierte Erläuterung zu erstellen.

1. Öffnen Sie die Datei **index.html** im Editor von Visual Studio Code.

1. Wählen Sie im Menü **Ausführen** die Option **Ohne Debuggen ausführen** aus.

    Wenn Sie dazu aufgefordert werden, wählen Sie den Browser Ihrer Wahl aus, um die App auszuführen.

1. Testen Sie bei geöffneter Prototyp-App im Browser die Anwendungsfälle, die Sie in Ihrem PRD aufgeführt haben, und überprüfen Sie, ob Ihre Prototyp-App die erwartete Funktionalität bereitstellt.

    Die Anwendungsfälle beschreiben die grundlegenden Funktionen, die Ihre Prototyp-App umsetzen sollte. Zum Beispiel:

    - Als Benutzer kann ich eine Liste mit Obstprodukten durchsuchen.
    - Als Benutzer kann ich detaillierte Informationen zu einem ausgewählten Produkt anzeigen lassen.
    - Als Benutzer kann ich Produkte zu meinem Warenkorb hinzufügen und Mengen anpassen.
    - Als Benutzer kann ich meinen Warenkorb vor dem Gang zur Kasse überprüfen und aktualisieren.
    - Als Benutzer kann ich eine Zusammenfassung meiner Bestellung anzeigen und sie „verarbeiten“ lassen (keine echte Transaktion).
    - Als Benutzer kann ich zwischen den Seiten „Products“, „ProductDetails“, „ShoppingCart“ und „Checkout“ navigieren.

1. Testen Sie nach der Überprüfung der Anwendungsfälle das dynamische Verhalten der App, indem Sie die Größe des Browserfensters ändern.

    Die Prototyp-App sollte über eine dynamische Benutzeroberfläche verfügen, die automatisch skaliert wird, um die korrekte Anzeige auf PCs und Smartphones zu ermöglichen.

1. Versuchen Sie, die eingeklappte Navigationsleiste zu testen.

    Sie haben festgelegt, dass die Navigationsleiste eingeklappt werden soll, wenn die Seitenbreite unter 300 Pixel fällt. Bei eingeklappter Navigationsleiste sollten ein oder zwei Buchstaben angezeigt werden, die jeweils eine der Webseiten der App darstellen.

    > **HINWEIS:** Die meisten Desktopbrowser (einschließlich Microsoft Edge) erzwingen eine Mindestfensterbreite von mehr als 300 px (häufig etwa 320–400 px). Das bedeutet, dass Sie das Browserfenster möglicherweise nicht manuell so weit verkleinern können, dass die Navigationsleiste eingeklappt wird.

1. (Optional) Führen Sie zusätzliche Tests durch, um sicherzustellen, dass die Prototyp-App Ihre Erwartungen erfüllt.

    Während dem Testen können Sie sich gerne Notizen machen. Sie können Ihre Notizen bei der nächsten Aufgabe verwenden, um Ihre Prototyp-App zu verfeinern.

1. Schließen Sie das Browserfenster oder beenden Sie die App in Visual Studio Code.

## Verfeinern Ihrer Prototyp-App

Ihre Prototyp-App sollte die Produktanforderungen bereits grundlegend umsetzen. Sie kann jedoch wahrscheinlich noch verfeinert und verbessert werden und erreicht das beabsichtigte Benutzererlebnis möglicherweise noch nicht vollständig.

Bei dieser Aufgabe verwenden Sie GitHub Copilot Agent, um die Funktionen und das Verhalten Ihrer Prototyp-App zu verfeinern.

Führen Sie die folgenden Schritte aus, um diesen Abschnitt der Übung zu absolvieren:

1. Geben Sie in der Chat-Ansicht den folgenden Prompt ein, um den Breakpoint für die eingeklappte Navigationsleiste anzupassen:

    ```md
    #codebase Refactor the prototype app to use a higher breakpoint for the collapsed navigation bar. Change from 300 to 600px. Update the copilot-instructions.md file to explain the updated 600px requirement.
    ```

    Wenn der Agent eine Navigationsleiste erstellt hat, die ihre Ausrichtung ändert, wenn der Bildschirm schmaler wird (von vertikal auf horizontal wechselt), verwenden Sie den folgenden Befehl, um das Verhalten der Navigationsleiste zu aktualisieren:

    ```md
    #codebase Refactor the code to ensure that the navigation bar stays on the left-side of the app for all devices types and sizes. The navigation bar should be responsive and maintain its position, in either an expanded or collapsed mode.
    ```

1. Nehmen Sie sich kurz Zeit, um die Code-Updates zu überprüfen, die der GitHub Copilot Agent als Reaktion auf Ihren Prompt erstellt.

1. Wählen Sie in der Chat-Ansicht **Behalten** aus, um die aktualisierten Dateien der Prototyp-App zu speichern.

1. Führen Sie die Anwendung erneut aus und stellen Sie sicher, dass die Navigationsleiste eingeklappt wird, wenn die Breite unter 600 Pixel beträgt.

1. Schließen Sie das Browserfenster oder beenden Sie die App in Visual Studio Code.

1. Geben Sie in der Chat-Ansicht den folgenden Prompt ein und überwachen Sie dann den Fortschritt des Agenten:

    ```md
    #codebase Update the prototype app to display an emoji in the nav bar for each of the web pages. Ensure that the emoji is centered horizontally in the nav bar when the nav bar is collapsed. Update the copilot-instructions.md file to include this product requirement.
    ```

1. Nehmen Sie sich kurz Zeit, um die Code-Updates zu überprüfen.

1. Um die aktualisierten Dateien der Prototyp-App in der Chat-Ansicht zu speichern, wählen Sie **Behalten**aus.

1. Führen Sie die Anwendung erneut aus und stellen Sie sicher, dass Emojis in der Navigationsleiste korrekt angezeigt werden.

    Die Navigationsleiste sollte Emojis anzeigen, die die einzelnen Webseiten darstellen. Das jeweilige Emoji sollte horizontal in der Navigationsleiste zentriert werden, wenn diese eingeklappt ist.

    Wenn Sie zusätzliche Probleme mit der Navigationsleiste feststellen, können Sie den GitHub Copilot Agent bitten, das Verhalten der Navigationsleiste zu verfeinern. Beispielsweise können Sie den Agenten auffordern: „#codebase Gestalte den Code so um, dass die Navigationsleiste immer sichtbar ist und nur zwei Zustände hat: ausgeklappt oder eingeklappt.“

1. Schließen Sie das Browserfenster oder beenden Sie die App in Visual Studio Code.

1. Geben Sie in der Chat-Ansicht den folgenden Prompt ein, um weitere Verbesserungsmöglichkeiten zu identifizieren:

    ```md
    #codebase Review the product requirements and wireframe diagrams in the copilot-instructions.md file. Are there any features or requirements that are missing from the implementation? Are there obvious opportunities to improve the user experience?
    ```

1. Überprüfen Sie die Antwort des GitHub Copilot Agents.

    Identifizieren Sie drei oder mehr vorgeschlagene Verbesserungen, die Sie implementieren möchten.

1. Erstellen Sie einen Prompt, die die Verbesserungen beschreibt, die Sie implementieren möchten.

    Verwenden Sie die Vorschläge von GitHub Copilot und alle von Ihnen beim Testen gemachten Notizen, um Verbesserungen zu implementieren. Sie können den GitHub Copilot Agent beispielsweise bitten, die folgenden Änderungen zu implementieren:

    ```md
    #codebase Implement the following improvements to the prototype app:

    - Replace alert() popups with in-app notification banners or toasts.
    - Add a confirmation/thank you message after processing an order.
    - Add a visual indicator (badge) for the number of items in the cart on the nav bar.

    Ensure that the copilot-instructions.md file is updated to reflect any changes to the product features, technical requirements, user experience, or other measurable characteristics.
    ```

    > **TIPP**: Sie können Informationen aus der Antwort von GitHub Copilot kopieren, um Ihren neuen Prompt zu erstellen. Sie können auch auf Abschnitte der vorherigen Antwort in Ihrem Prompt verweisen.

1. Wenn es zeitlich möglich ist, verfeinern Sie Ihre App mit den Vorschlägen von GitHub Copilot und Ihren eigenen Ideen.

1. Wählen Sie im Menü „Datei“ die Option **Arbeitsbereich speichern unter …** aus.

1. Um die Arbeitsbereichs-Konfigurationsdatei (VibeCoding-PrototypeApp.code-workspace) im Ordner **VibeCoding-PrototypeApp** zu speichern, wählen Sie **Speichern** aus.

    Mit dieser Datei können Sie Ihren Arbeitsbereich speichern und mit derselben Ordnerstruktur sowie denselben Einstellungen erneut öffnen.

## Zusammenfassung

In dieser Übung haben Sie gelernt, wie Sie den GitHub Copilot Agent mittels Vibe Coding zum Erstellen einer Prototyp-App verwenden. Sie haben Produktanforderungen definiert, eine erste Prototyp-App erstellt und sie anschließend optimiert, um das beabsichtigte Benutzererlebnis und die geplanten Funktionen besser zu erfüllen.

## Bereinigen

Nachdem Sie die Übung abgeschlossen haben, nehmen Sie sich kurz Zeit, um sicherzustellen, dass Sie keine Änderungen an Ihrem GitHub-Konto oder Ihrem GitHub Copilot-Abonnement vorgenommen haben, die Sie nicht beibehalten möchten. Falls Sie Änderungen vorgenommen haben, setzen Sie diese nach Bedarf zurück. Wenn Sie einen lokalen PC als Übungsumgebung verwenden, können Sie den Ordner der Prototyp-App, den Sie für diese Übung erstellt haben, archivieren oder löschen.
