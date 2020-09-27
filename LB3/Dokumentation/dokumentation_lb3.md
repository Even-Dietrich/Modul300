# Modul300 Dokumentation für die LB3

## Inhaltsverzeichnis:
1 [Allgemeine Bewertungskriterien](#Allgemein)<br>
&nbsp;1.1 [K1: Umgebung auf dem Notebook eingerichtet](#K1)<br>
&nbsp;1.2 [K2: Eigene Lernumgebung eingerichtet](#K2)<br>
&nbsp;1.3 [K3: Titel](#K3)<br>
&nbsp;1.4 [K4: Titel](#K4)<br>
&nbsp;1.5 [K5: Titel](#K5)<br>
&nbsp;1.6 [K4: Titel](#K6)<br>
2 [Unsere Idee](#Idee)<br>
3 [Unsere Arbeitsaufteilung](#Arbeitsaufteilung)<br>
4 [Verwendete Software](#Software)<br>
5 [Unsere Lösung](#Lösung)<br>
6 [Netzwerkplan](#Netzwerkplan)<br>
7 [Sicherheit](#Sicherheit)<br>
8 [Skript](#Skript)<br>
9 [Wichtige Dockerbefehle](#Befehle)<br>
10 [Testprotokolle](#Testprotokoll)<br>
&nbsp;10.1 [Minecraftserver Testprotokoll](#MC-Test)<br>
&nbsp;10.2 [Teamspeakserver Testprotokoll](#TS-Test)<br>
&nbsp;10.3 [Proxyserver Testprotokoll](#Proxy-Test)<br>
&nbsp;10.4 [Webserver Testprotokoll](#Web-Test)<br>
&nbsp;10.5 [Fileserver Testprotokoll](#File-Test)<br>
11 [Persönlicher Wissensstand und Reflexion](#Wissensstand)<br>
&nbsp;11.1 [Adam](#Adam)<br>
&nbsp;11.2 [Alex](#Alex)<br>
&nbsp;11.3 [Even](#Even)<br>
&nbsp;11.4 [Jason](#Jason)<br>

## Allgemeine Bewetungskriterien <a name="Allgemein"></a>

### K1: Umbebung auf eigenem Notebook eingerichtet und funktionsfähig <a name="K1"></a>
- VirtualBox ist installiert und funktionstüchtig
- Vagrant ist installiert und funktionstüchtig
- Visualstudio-Code ist installiert und wird verwendet
- Git-Client ist installiert
- SSH-Key für Client erstellt und im GitHub Account hinterlegt

### K2: Eigene Lernumgebung ist eingerichtet <a name="K2"></a>
- GitHub oder Gitlab-Account ist erstellt
- Git-Client wurde verwendet
- Dokumentation ist als Mark Down vorhanden
- Markdown-Editor ausgewählt und eingerichtet
- Markdown ist strukturiert
- Persönlicher Wissenstand im Bezug auf die wichtigsten Themen ist dokumentiert (Containerisierung / Docker, Microservices), siehe [Persönlicher Wissensstand](#Wissensstand)

### K3: <a name="K3"></a>
-

### K4: <a name="K4"></a>
-

### K5: <a name="K5"></a>
-

### K6: <a name="K6"></a>
-


## Unsere Idee: <a name="Idee"></a>

Wir wollen folgende Server aufsetzten und konfigurieren:

  - Reverse Proxy Server
  - Teamspeakserver
  - Minecraft Server
  - Apache Webserver mit einem Communityforum
  - Fileserver als Backup für die Daten des Minecraftserver

## Arbeitsaufteilung: <a name="Arbeitsaufteilung"></a>

Wir arbeiten alle gemeinsamm an der Dokumentation und individuell arbeiten wir an folgenden Servers:

  - Even, Reverse Proxy mit SSH-Tunnel
  - Alex, Teamspeakserver
  - Jason, Minecraft Server
  - Adam, Apache/Webserver mit Installation eines Open Source Forum
  - Fileserver je nach auslastung

## Software: <a name="Software"></a>

Um unsere Lösung testen zu können brauchen wir zusätzliche Software:

- <a href="https://www.teamspeak.com/en/downloads/">TS3 Client, </a>damit wir auf den Teamspeakserver zugreiffen können
- <a href="https://www.minecraft.net/de-de/download">Minecraft Client, </a>damit wir auf den Server spielen können

## Unsere Lösung: <a name="Lösung"></a>

### Installation vom Teamspeak-Server <a name="TS3-Server></a>

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


## Netzwerkplan: <a name="Netzwerkplan"></a>

Der Netzwerkplan muss noch mit den Servernamen ergänzt werden!

![Netzwerkplan](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/Netzwerkplan_nichtfertig.jpg)

## Sicherheit: <a name="Sicherheit"></a>

Mit den Shell Scripts welche im Vagrantfile hinterlegt sind werden Firewall Regeln erstellt und die Firewall aktiviert.

Folgende Firewall Regeln sind konfiguriert:
```Shell
    sudo ufw allow 22/tcp
    sudo ufw allow 80/tcp
    sudo ufw -f enable
```

## Skript: <a name="Skript"></a>

## Wichtige Dockerbefehle: <a name="Befehle"></a><br>

| Befehle | Auswirkung | 
|--------|----------|
|   docker stop $(docker ps -a -q)     |       Alle laufenden Container stoppen     |
|   docker rm $(docker ps -a -q)      |        Alle laufenden Container löschen   |
|   docker start [OPTIONS] CONTAINER [CONTAINER...]  |   Bestimmter Container starten   |
|        |            |
|        |            |
|        |            |
|        |            |
|        |            |
|        |            |

## Testprotokolle: <a name="Testprotokolle"></a><br>

In diesem Abschnitt sind alle Testprotokolle festgehalten.

### Testprotokoll für den Minecraftserver: <a name="MC-Test"></a><br>
-
### Testprotokoll für den Teamspeakserver: <a name="TS-Test"></a><br>
-
### Testprotokoll für den Proxyserver: <a name="Proxy-Test"></a><br>
-
### Testprotokoll für den Webserver: <a name="Web-Test"></a><br>
-
### Testprotokoll für den Fileserver: <a name="File-Test"></a><br>
-

## Persönlicher Wissensstand und Reflexion: <a name="Wissensstand"></a><br>
  
### Adam: <a name="Adam"></a><br>

  
### Alex: <a name="Alex"></a><br>

Stand 16.09.2020:

Ich hoffe, dass ich mit der Erfahrung von der LB2 in der LB3 ein komplexeres System aufsetzten kann. Aber ich habe noch nie mit Docker gearbeitet also ist heute das Ziel sich ein bisschen einzuarbeiten.

>Was sind Container?

>Container machen Anwendungen unabhängiger von der Umgebung, in der sie ausgeführt werden. Sie agieren damit ähnlich einer virtuellen Maschine (VM). Während eine VM jedoch ein vollständiges Betriebssystem sowie Applikationen enthält, teilen sich mehrere Container einen Betriebssystemkern. Jede Anwendung erhält lediglich einen neuen User Space und damit eine komplett isolierte Umgebung.

>![Vergleich VM und Container](https://github.com/Even-Dietrich/Modul300/blob/master/LB3/img/content-grafiken-vm-container.jpg)

>Container verbrauchen also im Vergleich zu VMs deutlich weniger Ressourcen wie
Rechenleistung, Hauptspeicher und Speicherplatz. Und es dreht sich hier um Megabytes bei Containern im Vergleich zu Gigabytes bei VMs. Daher passen auf einen Server sehr viel mehr Container als virtuelle Maschinen. Zudem sind Container schneller einsatzbereit: Während VMs manchmal mehrere Minuten zum Start benötigen, stehen Anwendungen hier beinahe sofort zur Verfügung.
>Quelle: <a href=https://www.cloud-mag.com/was-sind-container/#close>cloud-mag.com</a>
  
### Even: <a name="Even"></a><br>
Stand 16.09.2020:

In der LB3 werde ich versuchen mit meinem Vorwissen von der LB2 einen bessere und komplexere Arbeit abzuliefern. Da ich aber zuvor noch nie mit Docker gearbeitet habe muss ihc mich zuerst einarbeiten in. 
  
### Jason: <a name="Jason"></a><br>

Stand 16.09.2020:

Ich erhoffe mir das ich mit der Erfahrung von LB2 in der LB3 eine bessere und komplexere Arbeit abliefern kann. Ich habe jedoch noch nie mit Docker gearbeitet daher muss ich mich zuerst etwas einarbeiten.
