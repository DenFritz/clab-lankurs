# Vorbereitungen für die Netzerksimulationen und Übungen

Die Übungen für den Netzwerk-Kurs werden über ein GitHub-Repository zur Verfügung gestellt. Mit Hilfe von virtualisierten _Cisco IOS Images_, welche in _Docker Containern_ ausgeführt werden, erfolgt die Simulation von Netzwerkgeräten (Router und Switches). Als Simulationsumgebung dient die Open Source Software [_Containerlab_](https://Github.com/hellt/containerlab) von Nokia, welche die Container orchestriert. Der Aufbau eines simulierten Netzwerkes wird in einer sogenannten Topology-Datei in YAML-Syntax beschrieben, welche _Containerlab_ beim Start eines Labs einliest.

Die Laborübungen ie Netzwerk-Simulationen laufen in sog. [Dev Containern](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers) auf [GitHub Codespaces](https://docs.github.com/en/codespaces). _GitHub Codespaces_ sind virtuelle Maschinen, die auf GitHub gehostet werden und angepasst an die benötigte Systemumgebung in einem _GitHub Repository_ angelegt werden können. Ein kostenloser GitHub Account enthält derzeit (Juni 2025) monatlich 60 CPU-Stunden für die Nutzung von Codespace.

Um dies zu ermöglichen, benötigt jeder Kursteilnehmer einen eigenen GitHub-Account und eine Kopie (Fork) des entsprechenden GitHub-Repositories mit den [Netzwerkübungen](https://github.com/tjbalzer/clab-lankurs).

### GitHub Sign-up

!!! info
    Bereits bestehende GitHub-Accounts der Teilnehmer können ebenfalls genutzt werden. In diesem Fall weiter im Abschnitt [Installation von Wireshark auf dem SmartClient](vorbereitungen.md#installation-von-wireshark-auf-dem-smartclient).

Ein GitHub Account wird wie folgt angelegt:

#### GitHub-Startseite in Webbrowser öffnen

[GitHub-Startseite](https://gigthub.com) in Webbrowser öffnen und Sign-up Button auswählen:

![GitHub aufrufen](img/github-profil-anlegen-1.png)

![GitHub Sign-up #1](img/github-profil-anlegen-2a.png)

#### Benutzername und Passwort anlegen

- E-Mail Adresse eintragen
- Passwort eintragen und merken 🙂
- Gewünschten Usernamen eingeben (GitHub prüft Verfügbarkeit, Usernamen ggf. anpassen)
- Country/Region _Germany_ auswählen
- Button _Continue_ auswählen

![GitHub Sign-up #2](img/github-profil-anlegen-2b.png)

#### GitHub Account verifizieren

Der neue GitHub Account wird nun verifziert (hier am Beispiel _Bilderrätsel_ dargestellt):

- Button _Bilderrätsel_ auswählen
- Im rechten Bild angezeigte Grafik über rechts/links-Pfeile solange ändern, bis sie den im Text dargestellten Vorgaben entspricht
- Auswahl über den Button _Absenden_ bestätigen
- Bestätigungsnachricht wird angezeigt, wenn die Auswahl korrekt war, ansonsten wird ein neues Bilderrätsel angezeigt

![GitHub Verification #1](img/github-profil-anlegen-3a.png)

![GitHub Verification #2](img/github-profil-anlegen-3c.png)

![GitHub Verification #3](img/github-profil-anlegen-3d.png)

#### E-Mail Adresse bestätigen

Nach den Account Verifikation wird die E-Mail Adresse überprüft:

- Posteingang auf Nachricht von GitHub mit Bestätigungscode prüfen
- Bestätigungscode in den Feldern unter _Enter Code_ eintragen
- Eingabe über den Button _Continue_ abschließen (dadurch werden auch die GitHub _Terms of Service_ angenommen)
- Es folgt die Anzeige der GitHub Sign-in Seite

![GitHub Verification #4](img/github-profil-anlegen-4.png)

![GitHub Verification #5](img/github-profil-anlegen-5.png)

### GitHub Sign-in

Anmelden mit den Benutzerdaten des neu angelegten GitHub-Profils:

![GitHub Sign-in](img/github-anmeldung-1.png)

![GitHub Sign-in](img/github-anmeldung-2.png)

## _Forken_ des GitHub-Repositories für die Netzwerkübungen

Die Übungen werden über das GitHub Repository [clab-lankurs](https://github.com/tjbalzer/clab-lankurs) des GitHub Users _tjbalzer_ zur Verfügung gestellt. GitHub Codespaces werden einem GitHub-Repository zugeordnet und können nur vom Eigentümer des Repositories ausgeführt werden, wenn dieser mit seiner GitHub-Userid angemeldet ist. Deshalb muss das _clab-lankurs_ GitHub-Repository von der GitHub-Seite des GitHub-Nutzers _tjbalzer_ in das jeweilige GitHub-Konto jedes Kursteilnehmers kopiert (_geforkt_) werden.

Dieser _Fork_ des Original GitHub-Repositories wird wie folgt erstellt:

- Öffnen der GitHub-Webseite des _clab-lankurs_ Repositories: [https://github.com/tjbalzer/clab-lankurs](https://github.com/tjbalzer/clab-lankurs)
- Button _Fork_ auswählen, um das _clab-lankurs_ Repository als eigenes Repository in die GitHub-Umgebung des Nutzers zu kopieren
- Fork durch Bestätigung der Eingabemaske _Create a new fork_ über den Button _Create fork_ erstellen

![Fork erstellen #1](img/create-lankurs-fork-1.png)
![Fork erstellen #2](img/create-lankurs-fork-2.png)
![Fork erstellen #3](img/create-lankurs-fork-3.png)
![Fork erstellen #4](img/create-lankurs-fork-4.png)

## Dev Container in GitHub Codespaces erstellen und starten

Die Netzwerk Labs sollen in einer virtuellen Maschine (VM) auf GitHub bereitgestellt werden. Die VM wird als _Dev Container_ (auf GitHub auch _Codespace_ genannt) definiert und erstellt. Der Dev Container ist im geforkten Repository in der Datei `.devcontainer/devocontainer.json` definiert und basiert auf einem Containerlab Dev Container der SRL Labs:

``` JSON
{
    "image": "ghcr.io/srl-labs/containerlab/devcontainer-dind-slim:0.68.0",
    "hostRequirements": {
        "cpus": 2, 
        "memory": "8gb",
        "storage": "32gb"
    }
}
```

Die Existenz der Datei `.devcontainer/devcontainer.json` im _clab-lankurs_ Repository wird von GitHub automatisch erkannt und wir können den Dev Container (Codespace) wie folgt erstellen:

- Auf der Hauptseite des geklonten Repositories _clab-lankurs_ den Button _<> Code_ auswählen
- Daraufin wird ein Dialog mit den Reitern _Local_ und _Codespaces_ angezeigt
- Auswahl des Reiters _Codespaces_ und Erstellung des Dev Containers über den Button _Create codespace on main_
- Die Erstellung des Codespaces dauert in der Regel 5-10 Minuten
- Über den Informationsdialog `Setting up remote connection` unten rechts kann durch klicken auf `Building codespace...` bei Bedarf das Log für den Aufbau im Bereich `TERMINAL` angezeigt und verfolgt werden
- Die Erstellung und der Start des Codepaces ist abgeschlossen, wenn unten links der Verbindungsstatus `>< Codespaces: <zufälliger Name des Codespaces>` angezeigt, im Hauptfenster die _Containerlab Willkommensnachricht_ erscheint und das Containerlab Symbol am linken Rand in der vertikalen Bedienleiste eingeblendet wird 

!!! warning
    Als _Default Idle Timeout_ für GitHub Codespaces sind 30 Minuten vorkonfiguriert. Nutzt man einen gestarteten Codespace für 30 Minuten nicht, wie der Codespace automatisch gestoppt.

!!! warning
    Als _Default Retention Time_ für GitHub Codespaces sind 30 Tage vorkonfiguriert. Codespaces werden maximal 30 Tage nach der letzten Nutzung gelöscht.

!!! info
    Die Codepace-Einstellungen für seinen GitHub-Account erreicht man unter dem folgenden Link, wenn man bereits mit seinem Nutzernamen auf GitHub angemeldet ist: [https://github.com/settings/codespaces](https://github.com/settings/codespaces)

![Codespace erstellen #1](img/create-codespace-1.png)
![Codespace erstellen #2](img/create-codespace-2.png)
![Codespace erstellen #3](img/create-codespace-3.png)
![Codespace erstellen #4](img/create-codespace-4.png)
![Codespace erstellen #5](img/create-codespace-5.png)
![Codespace erstellen #6](img/create-codespace-6.png)

## Installation von Wireshark auf dem SmartClient

Soll statt eines Schulungs-Notebooks der persönliche EnBW Smart Client genutzt werden, muss zusätzliche Software auf dem Smart Client installiert werden.

!!! info
    Vorraussetzung: Der Schulungsteilnehmer muss über Adminrechte auf dem Smart Client verfügen.




