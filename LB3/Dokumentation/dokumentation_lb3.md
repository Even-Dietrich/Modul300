# Modul300 Dokumentation für die LB3

Unsere Dokumentation zur Leistungsbeurteilung 3

## Inhaltsverzeichnis:
1 [Allgemeine Bewertungskriterien](#Allgemein)<br>
&nbsp;1.1 [K1: Umgebung auf dem Notebook eingerichtet](#K1)<br>
&nbsp;1.2 [K2: Eigene Lernumgebung eingerichtet](#K2)<br>
&nbsp;1.3 [K3: Docker](#K3)<br>
&nbsp;1.4 [K4: Sicherheitsaspekte](#K4)<br>
&nbsp;1.5 [K5: Allgemein](#K5)<br>
&nbsp;1.6 [K6: Systemtechnische Bewertungspunkte](#K6)<br>
2 [Unsere Idee](#Idee)<br>
3 [Unsere Arbeitsaufteilung](#Arbeitsaufteilung)<br>
4 [Verwendete Software](#Software)<br>
5 [Unsere Lösung](#Lösung)<br>
&nbsp;5.1 [Netzwerkplan](#Netzwerkplan)<br>
&nbsp;5.2 [Installation Minecraft Server](#MC-Server)<br>
&nbsp;5.3 [Installation Teamspeak Server](#TS-Server)<br>
6 [Wichtige Dockerbefehle](#Befehle)<br>
7 [Testprotokolle](#Testprotokolle)<br>
&nbsp;7.1 [Minecraftserver Testprotokoll](#MC-Test)<br>
&nbsp;7.2 [Teamspeakserver Testprotokoll](#TS-Test)<br>
&nbsp;7.3 [Proxyserver Testprotokoll](#Proxy-Test)<br>
&nbsp;7.4 [Webserver Testprotokoll](#Web-Test)<br>
&nbsp;7.5 [Fileserver Testprotokoll](#File-Test)<br>
8 [Kubernaters](#Kubes)<br>
9 [Persönlicher Wissensstand und Reflexion](#Wissensstand)<br>
&nbsp;9.1 [Adam](#Adam)<br>
&nbsp;9.2 [Alex](#Alex)<br>
&nbsp;9.3 [Even](#Even)<br>
&nbsp;9.4 [Jason](#Jason)<br>

## 1 Allgemeine Bewetungskriterien <a name="Allgemein"></a>

### 1.1 K1: Umbebung auf eigenem Notebook eingerichtet und funktionsfähig <a name="K1"></a>
- VirtualBox ist installiert und funktionstüchtig
- Vagrant ist installiert und funktionstüchtig
- Visualstudio-Code ist installiert und wird verwendet
- Git-Client ist installiert
- SSH-Key für Client erstellt und im GitHub Account hinterlegt

### 1.2 K2: Eigene Lernumgebung ist eingerichtet <a name="K2"></a>
- GitHub oder Gitlab-Account ist erstellt
- Git-Client wurde verwendet
- Dokumentation ist als Mark Down vorhanden
- Markdown-Editor ausgewählt und eingerichtet
- Markdown ist strukturiert
- Persönlicher Wissenstand im Bezug auf die wichtigsten Themen ist dokumentiert (Containerisierung / Docker, Microservices), siehe [Persönlicher Wissensstand](#Wissensstand)

### 1.3 K3: Docker <a name="K3"></a>
- Bestehende Docker-Container sind kombiniert
- Bestehnde Container als Backend, Desktop-App als Frontend sind eingesetzt
- Volumes zur persistenten Datenablage ist eingerichtet
- Eingerichte Umgebungen ist dokumentiert
- Funktionsweise ist getestet und Testfälle sind dokumentiert

### 1.4 K4: Sicherheitsaspekte <a name="K4"></a>
- Wird nicht bewertet.

### 1.5 K5: Allgemein <a name="K5"></a>
- Allgemein- 
  - Kreativität
  - Komplexität 
- UmfangUmsetzung eigener Ideen
  - Übungsdokumentation als Vorlage für Modul-Unterlagen erstellt
- Persönlicher Lernentwicklung 
  - Vergleich Vorwissen, Wissenszuwachs
  -  Reflexion

### 1.6 K6: Systemtechnische Bewertungspunkte<a name="K6"></a>
- Zusätzliche systemtechnische Bewertungspunkte
  - Umfangreiche Vernetzung der Container-Infrastruktur (Ansätze für reale Nutzungszenarien)
- Image-Bereitstellung
- Continuous Integration
- Cloud-Integration
- Elemente aus Kubernetesübung sind dokumentiert


# 2 Unsere Idee: <a name="Idee"></a>

Wir wollen folgende Server aufsetzten und konfigurieren:

  - Reverse Proxy Server
  - Teamspeakserver
  - Minecraft Server
  - Apache Webserver mit einem Communityforum
  - Fileserver als Backup für die Daten des Minecraftserver

# 3 Arbeitsaufteilung: <a name="Arbeitsaufteilung"></a>

Wir arbeiten alle gemeinsamm an der Dokumentation und individuell arbeiten wir an folgenden Servers:

  - Even, Reverse Proxy mit SSH-Tunnel
  - Alex, Teamspeakserver
  - Jason, Minecraft Server
  - Adam, Apache/Webserver mit Installation eines Open Source Forum
  - Fileserver je nach auslastung

# 4 Software: <a name="Software"></a>

Um unsere Lösung testen zu können brauchen wir zusätzliche Software:

- <a href="https://www.teamspeak.com/en/downloads/">TS3 Client, </a>damit wir auf den Teamspeakserver zugreiffen können
- <a href="https://www.minecraft.net/de-de/download">Minecraft Client, </a>damit wir auf den Server spielen können
- Browser

# 5 Unsere Lösung: <a name="Lösung"></a>

## 5.1 Netzwerkplan: <a name="Netzwerkplan"></a>

Da Docker die IP automatisch verteilt, kann man im Netzwerkplan die IP nicht einteilen.
![Netzwerkplan](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/Netzwerkplan.png)


## 5.2 Installation vom Minecraft-Server <a name="MC-Server"></a>

Den Minecraft Server ist einfach zum installieren man braucht nur den folgenden Befehl eingeben:
```
docker run -d -p 25565:25565 --name mc -e EULA=TRUE itzg/minecraft-server
```
Dannach kann man schon via den Minecraft Client mit der Server IP auf den Server zugreiffen.
![MC-Connecten](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/MC-Connecten.png)

Nachdem man die man sich verbunden hat kann man auch schon mit dem Spielen anfangen.
![MC-inGame](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/MC-inGame.png)

Beweisvideo das mehrere Personen mit auf den Server kommen (Das Video muss heruntergeladen werden, da es zu gross ist und Github unterstützt dies nicht)<br>
![MC-Screen](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/vid/MC-Screen.mov)

## 5.3 Installation vom Teamspeak-Server <a name="TS3-Server"></a>

Da wir Docker auf einer VM haben müssen wir zuerst die VM Starten.
Um die VM zu starten muss man zuerst in den Ordner mit dem Vagrantfile, auf diesem Vagrantfile sind die Konfigurationseinstellungen, wie auch die Installation von Docker.
 ```
    Vagrant up
    Vagrant ssh   
 ```
 Dann sind mir auf der VM! 
 Dannach müssen wir nur noch den Teamspeak Server starten und die Lizenz akzeptieren
 ```
 docker run -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -e TS3SERVER_LICENSE=accept teamspeak 
 ```
 Um auf den Server zu kommen braucht man nur noch die IP-Adresse des Teamspeak Servers, dannach kann man sich via den TS3-Client mit dem Server verbinden.
 
![TS3-Connecten](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/TS3-Connecten.png)

Wenn man sich verbindet kommt ein Feld und dieses Feld fordert auf den Admintoken einzugeben damit man die Adminrechte auf diesem Server bekommt.

![TS3-Admintoken](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/TS3-Admintoken.png)

Der Admintoken bekommt man, wenn man sich auf der VM via SSH zugreift und in der Konsole wird der Token angezeigt.

![TS3-Admintoken-CLI](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/TS3-Admintoken-CLI.png)

und schon ist man auf dem Server!

![TS3-aufServer](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/TS3-aufServer.png)

Um den Teamspeak 3 Server im Hintergrund laufen lassen damit man auf der VM mehrere Containers laufen lassen will kann man den Server mit folgendem Befehl starten:

```
docker run -d -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -e TS3SERVER_LICENSE=accept teamspeak 
```
## 5.4 Installation Fileserver

Um den Fileserver zu installieren muss  man folgenden Befehl ausführen:
```
docker run -d -p 80:80 owncloud:8.1
```

Wenn dies gemacht ist muss man noch folgende Konfiguration machen und die Installation abschliessen:

![owncloud](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/owncloud.jpeg)

via localhost:80 zugreifen setup fertig stellen login: mc-server pw: 1234
<br>


Wenn man mit dem Setup fertig ist kann man Owncloud öffnen können und sich anmelden:

![owncloud](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/owncloud2.jpeg)

## 5.5 Installation Webserver

Um den Webserver zu installieren muss man nur den folgenden Befehl ausführen:
```
  docker run -d -p 8080 bitnami/apache
```

Wenn die Installation fertig ist kann man auf die Testseite zugreifen:

![owncloud](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/testweb.jpeg)


## 6 Wichtige Dockerbefehle: <a name="Befehle"></a><br>

| Befehle | Auswirkung | 
|--------|----------|
|   `docker stop $(docker ps -a -q)`     |       Alle laufenden Container stoppen     |
|   `docker rm $(docker ps -a -q)`      |        Alle laufenden Container löschen   |
|   `docker start [OPTIONS] CONTAINER [CONTAINER...]`  |   Bestimmter Container starten   |
|   `docker ps (-a -q)`  |         Aktive Container anzeigen  (Attribute=Anzeigen der aktiven Container) |
|   `docker start [id]`     |       Container starten      |
|   `docker kill`    |     Stoppt den Container sofort       |
|   `docker log`     |      Zeigt die Logs der einzelnen Container an      |
|   `docker run --rm -d -p xxxx:xxxx Container`     |      Bestimmter Container an bestimmten Port weiterleiten      |

## 7 Testprotokolle: <a name="Testprotokolle"></a><br>

In diesem Abschnitt sind alle Testprotokolle festgehalten.

### 7.1 Testprotokoll für den Minecraftserver: <a name="MC-Test"></a><br>

Ist zustand:<br>
             - Der Minecraft Server wurde installiert und ist gestartet<br>
             - Die IP-Adresse des Servers ist bekannt<br>
             - Auf dem Testclient ist der Minecraft Client installiert<br>
             
Soll zustand:<br>
             - Man kann via den Minecraft-Client auf den Server zugreiffen<br>
             - Wenn man auf dem Server ist kann man das Spiel spielen<br>
             
Tatsächliches Ergebnis:<br>
             - Beide User kommen auf dem Server und können sich verständigen<br>
             
Analyse:<br>
             
### 7.2 Testprotokoll für den Teamspeakserver: <a name="TS-Test"></a><br>

Ist zustand:<br> 
             - Der Teamspeak Server wurde installiert und läuft auf der VM<br>
             - Die IP-Adresse des Servers ist bekannt<br>
             - Auf den Testclients sind Teamspeak3 Clients installiert<br>
             - Der Admintoken ist nur für einen User bekannt<br>
             - Die Tester sind im gleichen Netz<br>
             
Soll zustand:<br>
             - Beider User kommen auf den Server<br>
             - Beide User können miteinander reden und verstehen einander<br>
             - Der Adminuser kann den normalen User vom Server kicken<br>

Tatsächliches Ergebnis:<br>
             - Beide User kommen auf dem Server und können sich verständigen<br>
             - Der Adminuser kann den normalen User vom Server kicken<br>
             
Analyse:<br>

Der Teamspeak-Server ist voll funktionstüchtig und kann in einer Produktiven Umgebung eingesetzt werden. Die Benutzerberichtigung ist korrekt konfiguriert.



### 7.3 Testprotokoll für den Proxyserver: <a name="Proxy-Test"></a><br>

- Der Proxyserver wurde nicht umgesetzt.



### 7.4 Testprotokoll für den Webserver: <a name="Web-Test"></a><br>

Ist-Zustand:
- Webserver ist installiert und läuft auf der VM
- Client hat Zugriff auf die Webseite
- Browser ist installiert

Soll-Zustand:
- User hat Zugriff auf die Webseite
- Webseite kann geöffnet und bedient werden
  
Tatsächliches Ergebnis:
- User hat Zugriff
- Webseite kann bedient werden.

Analyse:

Der Webserver und die Webseite funktioniert einfwandfrei.

### 7.5 Testprotokoll für den Fileserver: <a name="File-Test"></a><br>

#### Fall 1

Ist zustand:
- Der File Server wurde installiert und läuft auf der VM
- Client hat Zugriff auf das Filesystem 
- Folder Test wurde auf dem Server erstellt 
- Browser ist auf dem TestClient installiert 
- User Account Testuser auf owncloud registiert 

Soll zustand:
- User hat Zugriff auf den Ordner Test 
- Ordner kann geöffnet werden 
- noch keine Dateien werden angezeigt 

Tatsächliches Ergebnis:
- User hat Zugriff auf den Ordner Test 
- Ordner kann geöffnet werden 
- noch keine Dateien werden angezeigt 

Analyse:

Der Bentuzer hat Zugriff auf den Fileserver und sieht die Ordner 

#### Fall 2

Ist zustand:
- Der File Server wurde installiert und läuft auf der VM
- Client hat Zugriff auf das Filesystem 
- Folder Test wurde auf dem Server erstellt 
- Browser ist auf dem TestClient installiert 
- User Account Testuser auf owncloud registiert 
- User erstellt txt datei mit dem Name test 

Soll zustand:
- User kann die Datei test.txt erstellen
- Datei txt ist im System sichtbar
- User kann Datei öffnen und wort test reinschreiben und abspeichern 

Tatsächliches Ergebnis:
- Datei test.txt kann erstellt werden 
- Datei kann geöffnet und bearbeitet werden

Analyse:

Das erstellen und bearbeitet von Dateien funktioniert auf dem Fileserver 

Ist zustand:
- Der File Server wurde installiert und läuft auf der VM
- Client hat Zugriff auf das Filesystem 
- Folder Test wurde auf dem Server erstellt 
- Browser ist auf dem TestClient installiert 
- User Account Testuser auf owncloud registiert 
- Datei text.txt wird gelöscht 

Soll zustand:
- Datei test.txt kann per delete gelöscht werden 
- Datei ist danach nicht mehr vorhanden 

Tatsächliches Ergebnis:
- Datei kann gelöscht werden

Analyse:

Das löschen einer Datei funktioniert und kann per Befehl umgesetz werden

# 8 Kubernetes: <a name="Kubes"></a><br>
Zum verstehen von Kubernetes gibt es einige Begriffe die wir Ihnen kurz erklären. 

Grundbegriffe zu Kubeernetes:

Service Discorvery

Ist der Prozess um einen Cleint mit Verbindungsinformationen zu versorgen. 
Da in dem meisten Umgebungen mehrer Services mit mehrer Server bestehen, nutzt man einfach einen eindeutigen Namen zum erkennen des angefragen Services. Bei unserem Fall handelt es sich um die Verneztung der einzelnen Container. 

Containervernetzung beginnt mit der Annahme, dass es eine Route zwischen Hosts gibt – egal, ob diese Route über das öffentliche Internet läuft oder nur über einen schnellen lokalen Switch.

Also ist der Service Discorvery dazu da um Instanzen zu finden und die Vernetzung kümmert sich darum, die Verbindung aufzubauen. 

Weiter Funktionen:
- Health Checking
- Failover
- Load Balancing
-  Verschlüsselung der übertragenen Daten
- Isolieren von Containergruppen.

Load Balancing 

Anfragen werden auf parrallel arbeitende Systeme verteilt. Somit stellt man sicher, dass kein System  überlastet wird. 

Cluster

Dabei handelt es sich um ein Rechnerverbund. Die in einem Cluster befindlichen Computer  werden auch oft als Serverfarm bezeichnet.


Kubernets

Kubernetes ist ein Open-Source-System zur Automatisierung der Bereitstellung, Skalierung und Verwaltung von Container-Anwendungen. Es zielt darauf eine Plattform zur verfügung zu stellen um mehrer Container auf verschieden Hotst zu verteieln. Dabei unstersützt es viele Container-Tools wie Docker. 

>![Kubernaters](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/kubernetic.JPG)


Merkmale

   Immutable (Unveränderlich) statt Mutable.
   Deklarative statt Imperative (Ausführen von Anweisungen) Konfiguration.
   Selbstheilende Systeme - Neustart bei Absturz.
   Entkoppelte APIs – LoadBalancer / Ingress (Reverse Proxy).
   Skalieren der Services durch Änderung der Deklaration.
   Anwendungsorientiertes statt Technik (z.B. Route 53 bis AWS) Denken.
   Abstraktion der Infrastruktur statt in Rechnern Denken.


# 9 Persönlicher Wissensstand und Reflexion: <a name="Wissensstand"></a><br>
  
## 9.1 Adam: <a name="Adam"></a><br>
In der LB3 werde ich versuchen mit meinem Vorwissen von der LB2 einen bessere und komplexere Arbeit abzuliefern. Da ich aber zuvor noch nie mit Docker gearbeitet habe muss ihc mich zuerst einarbeiten in.

Mein Ziel an der LB3 ist es einen Webserver mit Installation eines Open Source Forum auf der VM zu Installieren. Dank meines vorwissens von der LB2 kann ich mitlerweile so komplexe sachen verstehen jedoch muss ich mich aber noch mit Docker einarbeiten, es ist nämlich recht Kompliziert 
  
## 9.2 Alex: <a name="Alex"></a><br>

### Stand 16.09.2020:

Ich hoffe, dass ich mit der Erfahrung von der LB2 in der LB3 ein komplexeres System aufsetzten kann. Aber ich habe noch nie mit Docker gearbeitet also ist heute das Ziel sich ein bisschen einzuarbeiten.

>Was sind Container?

>Container machen Anwendungen unabhängiger von der Umgebung, in der sie ausgeführt werden. Sie agieren damit ähnlich einer virtuellen Maschine (VM). Während eine VM jedoch ein vollständiges Betriebssystem sowie Applikationen enthält, teilen sich mehrere Container einen Betriebssystemkern. Jede Anwendung erhält lediglich einen neuen User Space und damit eine komplett isolierte Umgebung.

>![Vergleich VM und Container](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/content-grafiken-vm-container.jpg)

>Container verbrauchen also im Vergleich zu VMs deutlich weniger Ressourcen wie
Rechenleistung, Hauptspeicher und Speicherplatz. Und es dreht sich hier um Megabytes bei Containern im Vergleich zu Gigabytes bei VMs. Daher passen auf einen Server sehr viel mehr Container als virtuelle Maschinen. Zudem sind Container schneller einsatzbereit: Während VMs manchmal mehrere Minuten zum Start benötigen, stehen Anwendungen hier beinahe sofort zur Verfügung.
>Quelle: <a href=https://www.cloud-mag.com/was-sind-container/#close>cloud-mag.com</a>

### Wissenstand vom 30.09.2020:

Ich habe mein Wissen über Docker deutlich verbessert, ich weiss wie man Docker in einem Produktiven Umfeld einsetzt. Der grosse Vorteil von Docker ist dass es viel weniger Ressourcen vom Host braucht als bei einer VM. Auf meinem Mac kann ich ohne Probleme mehrere Docker und Services am laufen haben, die von einander getrennt sind und noch ohne Probleme noch Frontend Programme für die Services verwenden. Das ist mit VMs nicht möglich, da eine VM mehr Ressourcen vom Host braucht.

### Reflexion

Durch Github konnten wir ohne Probleme unsere Arbeitaufteilen und gleichzeit an der LB3 arbeiten. Mit unserem Whatsapp-Chat konnten wir uns auch immer auf dem neusten Stand halten.
Durch die Arbeit an der LB2 hatte ich keine grosse Probleme, mich mit Docker ausseinander setzten.
  
## 9.3 Even: <a name="Even"></a><br>

### Stand 16.09.2020:

In der LB3 werde ich versuchen mit meinem Vorwissen von der LB2 einen bessere und komplexere Arbeit abzuliefern. Da ich aber zuvor noch nie mit Docker gearbeitet habe muss ihc mich zuerst einarbeiten in.

### Stand 30.09.2020

Ich lernte heute verschiede Befehle kennen:
| Befehl | Auswirkung |
|--------|------------|
| docker stop $(docker ps -a -q)     |       Alle laufenden Container stoppen     |
| docker rm $(docker ps -a -q)      |        Alle laufenden Container löschen   |
| docker run -p -d nginx            | Installiert den Container Nginx (Proxy) |
|docker container ps                 | Zeigt alle Container an |

Dazu lernte ich noch den Container Nginx kennen. Mit diesem Container wollten wir den Reverse Proxy realisieren. Dazu versuchte ich mit mehreren Anleitung durchzuführen was ich aber am Ende nicht machte. Da wir in der LB3 die Punkte von K4 nicht umsetzt müssen wurde der Reverse Proxy nicht umgesetzt. Trotzdem hätte ich mit mehr Zeit diesen mit dem Angesammelten Wissen realisieren.

### Reflexion:

Durch eine gute Plannung und das verwenden von Github kammen wir schnell mit der LB3 vorwärts. Wir konnten uns gegeseitig helfen und somit unser angesammelt Wissen auch einsetzten. 
Das Wissen von LB2 konnte ich sehr gut anwenden und es half mir in einigen Situationen weiter. 

  
##  9.4 Jason: <a name="Jason"></a><br>

### Vorwissen:

Ich habe bezogen auf Docker oder Kubernetes überhaupt kein Vorwissen und muss mir alles von Anfang an aneignen und nachlesen. Dies sollte aber kein Problem sein.

### Stand 16.09.2020:

Ich erhoffe mir das ich mit der Erfahrung von LB2 in der LB3 eine bessere und komplexere Arbeit abliefern kann. Ich habe jedoch noch nie mit Docker gearbeitet daher muss ich mich zuerst etwas einarbeiten.

Um mich über Docker zu informieren benutzte ich das GitHub von herr Bernet und Tutorials auf Youtube. Docker ist für mich ziemlich komplex und kompliziert, mir ist noch sehr vieles davon unklar aber das wird sich hoffentlich mit der Zeit bessern.

Wichtige Befehle für Docker:
- `docker start [OPTIONS] CONTAINER [CONTAINER...]` > Startet einen Container, dabei müssen noch Parameter und angaben mitgegeben werden.
- `docker stop $(docker ps -a -q)` > Stoppt alle laufenden Container.

Wichtiges für ein Dockerfile:
```Dockerfile
  # Paket von hub.docker
  FROM php:7.0-apache
  # kopiert ein File in den Container
  COPY src/ /var/www/html/
  # Gibt dem Container an das der Port 80 offen sein soll
  EXPOSE 80
```

### Stand 30.09.2020:

Heute habe ich mehr über Docker gelernt. Ich habe mit meinen Teamkollegen die Dockerfiles erstellt und die Umgebung weiter voran gebracht. Ebenfalls habe ich die Doku weitergeschrieben und das gemachte dokumentiert und beschrieben und mein gelerntes festgehalten. 

### Reflexion:

Die Arbeit in dieser LB haben wir im Team von anfang an sehr gut geplant und aufgeteilt. Wir haben die Dokumentation sehr früh und übersichtlich gestaltet und darin unsere Arbeitsaufteilung festgehalten. 

Ich finde wir haben in der LB3 sehr gut von der LB2 profitiert und unsere Arbeitsweise erfolgreich angepasst und umgesetzt. Ich bin sehr zufrieden mit unserer Arbeit.

