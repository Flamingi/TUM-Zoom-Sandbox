
# TUM-Zoom-Sandbox
# Nutzung des Zoom-Clients in Windows Sandbox
Durch die aktuelle Lage ist an der TUM kein Präsenzbetrieb möglich, weshalb alle Vorlesungen und Übungen digital abgehalten werden müssen. Zwar existieren verschiedene Tools, mit welchen digitale Lehrveranstaltungen live gehalten werden können, doch nur wenige erfüllen alle Funktionsanforderungen und sind mit einer hohen Zahl an Teilnehmern stabil. Eines dieser Programme ist Zoom, welches von verschiedenen Lehrenden eingesetzt wird. Leider ist Zoom in der Vergangenheit mehrfach durch schlechten Datenschutz und Sicherheitslücken negativ aufgefallen. Als Lehrender besteht die Möglichkeit sich für andere Lösungen zu entscheiden, doch als Student ist man gezwungen Zoom zu nutzen, wenn die Vorlesung diesen Dienst nutzt. Es ist möglich an der Zoom-Veranstaltung im Browser teilzunehmen, aber dies ist nur mit eingeschränktem Funktionsumfang und einer oft schlechten Stabilität möglich, weshalb für eine störungsfreie Nutzererfahrung die Installation des Desktopclients empfohlen wird. Wie man dies tun kann, ohne seine Daten zu gefährden oder seinen Computer für Hacker angreifbar zu machen, wird in dieser Anleitung beschrieben.
## Was ist die Windows Sandbox?
Die Windows Sandbox ist eine ins Betriebssystem integrierte virtuelle Maschine, welche parallel und abgeschottet zur eigentlichen Windows-Installation läuft. Am Ende läuft also Windows in Windows, ohne Zugriff auf persönliche sensible Daten und Zoom kann ohne Bedenken installiert werden. Wer bereits Erfahrung mit VMs hat, der wird hier nichts bahnbrechend Neues lernen, alle Funktionen, die von Windows Sandbox zur Verfügung gestellt werden, können schon seit Jahren von anderen Tools übernommen werden. Neu ist allerdings die sehr einfache Bedienung und [effiziente Implementierung](https://techcommunity.microsoft.com/t5/windows-kernel-internals/windows-sandbox/ba-p/301849) des Parallel-Systems, sowohl in Anbetracht des benötigten Speicherplatzes (unter 100MB) als auch in der Nutzung der Hardware. 
## Voraussetzungen
Um die Sandbox zu nutzen müssen einige Anforderungen erfüllt werden, diese sind nicht sehr speziell und jeder halbwegs moderne PC oder Laptop sollte ausreichen:
* 1 GB freier Speicherplatz
* 4 GB RAM (empfohlen werden 8GB RAM)
* 2 CPU-Kerne (empfohlen werden 4 CPU-Kerne)
* CPU-Support für Virtualisierung (muss evtl. im BIOS aktiviert werden)
* Windows 10 Version 1903 oder neuer
* Windows Pro, Enterprise, Edu, Server (keine Sorge, falls Windows 10 Home installiert ist. Als TUM Student(in) kann man sich einen kostenfreien Windows 10 Edu Key besorgen)
## Aktivierung der Sandbox
Im Folgenden wird nun Schritt für Schritt die Aktivierung der Sandbox erläutert. 
### Korrekte Windows Version nutzen
Um zu überprüfen, welche Windows Version installiert ist, gibt man in das Windows-Suchfeld `winver` ein und führt den Befehl aus. Ist die Version eine der oben in den Voraussetzungen genannten, so kann man jetzt einfach zum nächsten Punkt springen, ansonsten ist jetzt beschrieben, wie man sich als TUM-Student(in) einen Edu Key besorgt.
![Anzeigen der Windows Version](https://i.imgur.com/jwVjffu.png)
* Als erstes muss auf Studisoft Office 365 (kostenfrei) bestellt werden. Wer dies bereits getan hat und einen `forstudents.onmicrosoft`-Account hat, kann diesen Schritt überspringen
  * Die [Studisoft-Seite](https://www.studisoft.de/studisoft/StudiSoft_Overview) aufrufen
  * Aus der List die TUM auswählen und sich wie gewohnt durch SSO anmelden
  * Bei den verfügbaren Artikeln Office 365 auswählen und bestellen
  * Der Download ist ein pdf mit einer Anleitung zur Erstellung eines Microsoft-Accounts, diese Anleitung befolgen
  * Am Ende sollte man einen Microsoft-Account der Form `TUM-Kennung@forstudents.onmicrosoft.com` haben
  * (Wer möchte kann sich im Anschluss die aktuellen Office 365 Programme im [Portal](https://portal.microsoftonline.com) herunterladen)
* Mit diesem Account kann man sich nun einen Windows 10 Edu Key holen und aktivieren
  * Zum Microsoft Azure [Portal](https://portal.azure.com/#blade/Microsoft_Azure_Education/EducationMenuBlade/software) navigieren und mit dem neuen Account anmelden
  * Nach `Windows 10 Education` suchen, sich den Key anzeigen lassen und kopieren (und am besten speichern)![Generieren des Windows 10 Edu Keys](https://i.imgur.com/mkT6GRX.png)
  * Die Windows-Einstellungen öffnen und zu `Update und Sicherheit > Aktivierung > Product Key ändern` navigieren
  * Hier den Key eingeben und das System aktualisieren
  * Nach einem Neustart sollte nun beim erneuten Aufruf von `winver` auch Windows 10 Edu aktiviert sein
### Sandbox-Feature aktivieren
Mit der richtigen Windows-Version, kann man nun die Sandbox aktivieren:
* In die Windows-Suche `Windows-Features aktivieren oder deaktivieren` eingeben und öffnen
* Im neuen Fenster nach unten scrollen und den Haken bei `Windows-Sandbox` aktivieren![Aktivieren des Windows-Sandbox Features](https://i.imgur.com/0ba8UdL.png)
* Nach einem weiteren Neustart ist nun die Windows Sandbox verfügbar
## Nutzen der Sandbox
Die Sandbox kann man jetzt einfach nutzen, indem man nach `Windows Sandbox` sucht. Der erste Start kann wenige Minuten in Anspruch nehmen, da das Betriebssystem konfiguriert werden muss, spätere Starts dauern nur noch einige Sekunden. Man startet in ein komplett leeres Windows-System hinein, bei dem keine Programme installiert sind. Man hat zunächst auch keinen Zugriff auf Dateien des Host-Systems und kann auch keine neuen Dateien speichern. Dieses System eignet sich dann auch, um zum Beispiel zwielichtige Webseiten aufzurufen, unbekannte Programme zu untersuchen oder Malware zu installieren (z. B. Zoom) ohne sensible Daten preiszugeben oder sich durch Sicherheitslücken angreifbar zu machen. Ein weiteres Merkmal der Sandbox ist, dass der Zustand nicht gespeichert wird, d. h. bei jedem Start hat man ein frisches unmodifiziertes System und muss alle Programme neu installieren. Ein entsprechender Workaround, der das Leben einfacher macht ist im nächsten Punkt beschrieben.
## Konfigurieren der Sandbox
Wie bereits geschrieben läuft die Sandbox zunächst komplett abgeschottet und ohne Zugriff auf Dateien des Host-Systems. Damit man auch auf Vorlesungs-PDFs oder ähnliches Zugreifen kann (wobei man die auch einfach auf dem gleichzeitig nutzbaren Host-Sytem öffnen kann), ist es möglich einen Shared Folder einzurichten. Ich habe z. B. in so einem Shared Folder ein Skript, welches automatisch den Zoom Desktop-Client herunterlädt und installiert.
* Zunächst erstellt man sich einen Ordner, der geshared werden soll. Ich habe unter `C:` einfach einen Ordner `C:\Sandbox` erstellt und dort den Zoominstaller abgelegt
* Durch `Rechtsklick > Neu > Textdokument` dann eine Konfigurationsdatei anlegen, z. B. `Zoom Sandbox.txt`
* Diese Konfigurationsdatei ist eine XML-Datei und kann dann mit einem Editor der Wahl modifiziert werden
* Alle Einstellungen müssen zwischen dem `Configuration`-Parameter stehen
```XML
<Configuration>
...
</Configuration>
```
* Jetzt kann man den Parameter `MappedFolders` hinzufügen, unter welchem man wiederum einen `MappedFolder` mit dem Pfad zum Shared Folder angibt. Zusätzlich ist noch der Parameter `ReadOnly` angegeben, welcher die Sandbox nur lesen, aber nicht schreiben lässt. Möchte man auch aus der Sandbox Dateien speichern können, so muss dieser Parameter von `true` auf `false` gesetzt werden. Man muss sich dabei aber im klaren sein, dass man eine Verbindung zwischen der Sandbox und dem Host-System herstellt und so das System angreifbar macht. 
```XML
<Configuration>
    <MappedFolders>
        <MappedFolder>
            <HostFolder>C:\Sandbox</HostFolder>
            <ReadOnly>true</ReadOnly>
        </MappedFolder>
    </MappedFolders>
</Configuration>
```
* Im Shared Folder kann man nun noch ein Skript anlegen, welches den Zoom-Installer herunterlädt und installiert. Ich habe die Datei `InstallZoom.cmd` genannt
```bash
REM Download latest Zoom Installer

curl -L "https://zoom.us/client/latest/ZoomInstaller.exe" --output C:\Users\WDAGUtilityAccount\Desktop\ZoomInstaller.exe

REM Install and run Zoom
start C:\Users\WDAGUtilityAccount\Desktop\ZoomInstaller.exe

exit
```
* Nun kann man die vorhandene Konfigurationsdatei erweitern, sodass das Skript beim Start ausgeführt wird
```XML
<Configuration>
    <MappedFolders>
        <MappedFolder>
            <HostFolder>C:\Sandbox</HostFolder>
            <ReadOnly>true</ReadOnly>
        </MappedFolder>
    </MappedFolders>

	<LogonCommand>
		<Command>C:\Users\WDAGUtilityAccount\Desktop\Sandbox\InstallZoom.cmd</Command>
	</LogonCommand>
</Configuration>
```
* Nach dem Speichern der Konfigurationsdatei, muss die Dateiendung von `.txt` in `.wsb` geändert werden. Zum Starten der Sandbox muss in Zukunft nur diese Datei geöffnet werden.
* Nach dem Starten der modifizierten Sandbox ist der Ordner auf dem Desktop und man hat Zugriff auf alle dort gespeicherten Dateien. Auch läuft das geschriebene Skript automatisch ab, lädt Zoom und installiert das Programm.![Sandbox mit Shared Folder](https://i.imgur.com/KHiM1j0.png)
* Wer noch mehr Informationen zu den Config Files möchte, der findet sie [hier](https://techcommunity.microsoft.com/t5/windows-kernel-internals/windows-sandbox-config-files/ba-p/354902) in einem entsprechenden Post von Microsoft
* Die beiden erstellten Beispieldateien stehen zum Download bereit
