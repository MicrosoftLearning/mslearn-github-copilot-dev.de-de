---
lab:
  title: Vorbereiten – Konfigurieren Ihrer Labumgebung für GitHub Copilot-Übungen (Python)
  description: 'Überprüfen Sie die Lab-Anforderungen und konfigurieren Sie Ressourcen, bevor Sie GitHub Copilot-Übungen starten.'
---

# Konfigurieren Ihrer Labumgebung für GitHub Copilot-Übungen

Ihre Labumgebung muss für die Python-Entwicklung mit Visual Studio Code und GitHub Copilot konfiguriert werden. Der Zugriff auf ein GitHub-Konto mit aktiviertem GitHub Copilot ist erforderlich.

Führen Sie die folgenden Schritte aus, um zu überprüfen, ob Ihre Labumgebung ordnungsgemäß konfiguriert ist:

1. Stellen Sie sicher, dass Git, Version 2.48 oder höher, in Ihrer Labumgebung installiert ist.

    Führen Sie den folgenden Befehl in einem Terminalfenster aus, um die installierte Version von Git zu überprüfen:

    ```bash
    git --version
    ```

    Wenn Sie Windows ausführen und Git aktualisieren möchten, verwenden Sie den folgenden Befehl:

    ```bash
    git update-git-for-windows
    ```

    Bei Bedarf können Sie Git über folgende URL herunterladen: <a href="https://git-scm.com/downloads" target="_blank">Git herunterladen</a>

1. Stellen Sie sicher, dass die neueste Version von Python in Ihrer Labumgebung installiert ist.

    Führen Sie den folgenden Befehl in einem Terminalfenster aus, um die installierte Version von Python zu überprüfen:

    ```bash
    python3 --version
    ```

    Führen Sie bei Bedarf die Schritte zum Konfigurieren von Python in Visual Studio Code über die folgende URL aus: <a href="https://code.visualstudio.com/docs/python/python-tutorial" target="_blank">Erste Schritte mit Python in VS Code</a>

1. Stellen Sie sicher, dass Visual Studio Code und die Python-Erweiterung in Ihrer Labumgebung installiert sind.

    Bei Bedarf können Sie VS Code über folgende URL herunterladen: <a href="https://code.visualstudio.com/download" target="_blank">Visual Studio Code herunterladen</a>

    Sie können die Python-Erweiterung über die Ansicht „Erweiterungen“ in Visual Studio Code installieren.

1. Stellen Sie sicher, dass Sie Zugriff auf ein GitHub-Konto und ein GitHub Copilot-Abonnement haben.

    Melden Sie sich über folgende URL bei Ihrem GitHub-Konto an: <a href="https://github.com/login" target="_blank">GitHub-Anmeldung</a>

    Wenn Sie kein GitHub-Konto haben, können Sie ein eigenes Konto über die GitHub-Anmeldeseite erstellen. Wählen Sie auf der Anmeldeseite **Konto erstellen** aus.

    Öffnen Sie die Seite „Einstellungen/Profil“ Ihres GitHub-Kontos, und überprüfen Sie, ob Sie Zugriff auf ein GitHub Copilot-Abonnement haben. Wenn Sie über ein aktives Abonnement für GitHub Copilot Pro, GitHub Copilot Pro+, GitHub Copilot Business oder GitHub Copilot Enterprise verfügen, das Sie für Schulungen verwenden können, können Sie Ihr vorhandenes GitHub Copilot-Abonnement zum Durchführen der GitHub Copilot-Übungen verwenden.

    Wenn Sie über ein eigenes GitHub-Konto verfügen, aber kein GitHub Copilot-Abonnement haben, können Sie während einer Schulungsübung einen GitHub Copilot Free-Plan über Visual Studio Code einrichten.

    > **WICHTIG:** Der kostenlose Plan GitHub Copilot Free ist eine eingeschränkte Version von GitHub Copilot, mit dem bis zu 2.000 Codevervollständigungen und 50 Chats oder Premiumanforderungen pro Monat möglich sind. Wenn Sie einen GitHub Copilot Free-Plan außerhalb von Schulungsübungen verwenden, überschreiten Sie möglicherweise die Ressourcengrenzwerte des Plans, bevor Sie die Schulung abschließen. Der GitHub Copilot Free-Plan ist für GitHub Copilot Pro-, GitHub Copilot Pro+-, GitHub Copilot Business- bzw. GitHub Copilot Enterprise-Abonnements nicht verfügbar.
