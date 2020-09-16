### Modul300 Dokumentation
<br>

# Allgemeine Bewertungskriterien
<br>

## K1 Umgebung wurde auf dem Notebook/VM in der TBZ cloud eingerichtet
<br>

## K2 Unsere Lernumgebung einrichten

- Ein Git-Client wird verwendet
- Dokumentation ist als Markdown vorhanden
- Markdowneditor wurde ausgewählt (Visual Studio Code)
- Markdwon ist Strukturiert
- Persönlicher Wissenstand wird dokummentiert und festgehalten
<br>

## K3
    
- Bestehende vm aus Vagrant-Cloud einrichten
  - Alle Vagrantfiles im Verzeichnis Modul300/LB2/server
- Kennt die Vagrant-Befehle  
- Eingerichtete Umgebung ist dokumentiert (Umgebungs-Variablen, Netzwerkplan    gezeichnet, Sicherheitsaspekte)
- Funktionsweise getestet inkl. Dokumentation der Testfälle- andere, vorgefertigte vm auf eigenem Notebook aufgesetzt
VM können mit Vagrantfile erfolreich erstellt werden. 
- Projekt mit Git und Mark Down dokumentiert
- Ein Git-Client wird verwendet   
<br>

## K4 Sicherheitsaspekte sind implementiert

- Firewall eingerichtet inkl. Rules
- Reverse-Proxy eingerichtet
- Benutzer- und Rechtevergabe ist eingerichtet
- Zugang mit SSH-Tunnel abgesichert
- Sicherheitsmassnahmen sind dokumentiert
- Projekt mit Git und Mark Down dokumentiert
<br>
<br>

# LB2

## Software

- Visual Studio Code
- BashGit
- Oracle VM VirtualBox
- Vagrant

## Unsere Lösung:

Wir haben uns dazu entschieden eine Umgebung mit insgesamt 5 Servern:

- Reverse Proxy (srv05-lx-proxy)
- Fileserver (srv03-lx-fileserver)
- Backupserver (srv04-lx_-fileserver)
- Webserver (srv01-lx-webserver)
- Datenbankserver (srv02-lx-databaseserver)

Siehe auch Netzwerkplan.

Alle Server werden aus einem Vagrantfile vollautomatisch erstellt und konfiguriert.

## Hardware

Die Hardware wird ebenfalls durch das Vagrantfile konfiguriert (Beispiel: Proxyserver): 

```Ruby
    config.vm.define "srv05-lx-proxy" do |subconfig|
        subconfig.vm.provider "virtualbox" do |vb|
            vb.name = "proxy"
            vb.memory = "512"
        end
```

## Netzwerkplan

Hier zeigen wir Ihnen unsere Umgebung auf die wir automatisch mit den Vagrantfile erstellen können.<br>

![Netzwerkplan](https://github.com/Even-Dietrich/Modul300/blob/master/Dokumentation/img/Netzwerkplan.jpg)

## Scripts

Im Vagrantfile wird der VM Shell Commands mitgegeben welche nach der Installation automatisch ausgeführt werden. Die Commands sind standard Commands aus dem Linux Terminal.

Beim ProxyServer werden folgende Commands ausgeführt. 

```Ruby
#Shell für den Proxy Server
config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    #Installation apache
    sudo apt-get -y install apache2 libxml2-dev
    #Reverse Proxy
    sudo a2enmod proxy
	sudo a2enmod proxy_html
	sudo a2enmod proxy_http
    #kopieren und verlinken der reverse proxy config datei
    sudo cp /vagrant/001-reverseproxy.conf /etc/apache2/sites-available/
    sudo ln -s /etc/apache2/sites-available/001-reverseproxy.conf /etc/apache2/sites-enabled/
    #Neustart der Dienste
    sudo service apache2 restart
    #Firewall regeln erstellen und Firewall aktivieren
    sudo ufw allow 80/tcp
    sudo ufw allow 22/tcp
    sudo ufw -f enable

SHELL
```

## Sicherheit

Mit den Shell Scripts welche im Vagrantfile hinterlegt sind werden Firewall Regeln erstellt und die Firewall aktiviert.

Folgende Firewall Regeln sind konfiguriert:
```Shell
    sudo ufw allow 22/tcp
    sudo ufw allow 80/tcp
    sudo ufw -f enable
```
<br>

# Persönlicher Wissenstand:

## Adam:

#### Stand vor Kursbeginn<br>
Ich habe vor dem Beginn des Kurses noch keine ahnung von GitHub und das Erstemal im Modul 300 damit gearbeitet. Ich kannte jedoch GitLab von meinem Geschäft, konnte aber bis jetzt noch nie damit in Kontakt gekommen.<br>

#### Stand 19.08.2020<br>
Heute habe ich 2 Tools kennengelernt GitHub und Varagnt. Vargant ist ein Tool um automatisch VM aufzusetzen. Mithilfe von dem Bash Terminal können wir nun drauf zugreifen und so damit Arbeiten.<br>

#### Stand 02.09.2020<br>
Ich habe heute von Zuhause aus gearbeitet weil es mir nicht sehr wohl war. Ich konnte Jedoch mit der Hilfe meiner Teamkollegen trozdem vorankommen. Ich habe den Fileshare-service Samba besser kennengelernt, zusammen mit Even haben wir einen Share erstellt per Vagant automatisiert.


## Alex:
### Stand vor dem Kurs<br>
Da ich bei der Arbeit zum Teil mit Linux/Unix befehle zu tun habe sind mir die geläufigsten Befehle bekannt. Aber sonst habe ich nicht viel mit VMs zu tun oder mit konfigurationen über die Shell zu tun

#### Stand 19.08.2020
Heute habe ich gelernt, wie man ein Github Repository mit meinem PC synchronisieren kann.<br>

Wichtige Befehl für den Git-Client:<br>
- `git add -A` änderungen werden erkennt<br>
- `git commit -m "Kommentar"` Die Änderungen werden auf dem Gerät gespeichert (lokal)<br>
- `git push` Die Änderungen werden auf GitHub geladen.<br>

Desweiteren habe ich Vagrant kennen gerlernt. Damit kann man Konfigurationsdateien erstellen für VM, damit man nicht immer die VM manuell aufsetzten muss.

### Stand 02.09.2020
Heute habe ich mehr über wie man Konfigurationseinstellung über die Shell macht und wie man das im Vagrant automatisch machen kann mit dem Befehl echo und mit der Abgabe vom Pfad der Konfigurationsdatei bzw. wenn keine Vorhanden ist muss man diese zuerst neu erstellen.
Dies kann man einfach via einen Texteditor Bsp: sudo nano /pfad/zur/datei/dateiname.conf

Bsp zum in der Konfigurationsdatei etwas am Schluss anschliessen zu können:
- `sudo su` //Als Root ausführen
- `sudo echo "set" >> /pfad/zur/datei/dateiname.conf`
echo wiedergibt String, welcher man definiert hat. Die Zwei >> geben an dass der vorherigen String ganz unten bei der Textdatei anfügen soll. Alles nachden beiden Einfügoperatoren ist der Pfad.

Bsp um in einer Konfiguration alles zu Überschreiben
- `sudo su` //Als Root ausführen
- `sudo echo "String"  > /pfad/zur/datei/dateiname.conf` 
echo wiedergibt String, welcher man definiert hat. Der einte > gibt dass das ganze File überschrieben wird und dannach ist nur noch der voherigen String vorhanden. Alles nachdem Einfügoperatoren ist der Pfad.<br>

Wichtige Befehle und Konfigurationsdatein für Mysql und Wordpress:

MySql:
- /etc/mysql/mysql.conf.d/mysqld.conf: Dort kann man eine IP-Festlegen, welche auf den Server remote zugriff hat oder alternativ 0.0.0.0 dann kann jede andere IP auch auf den Mysql Server zugreiffen.
- mysql -uBenutzername -pPasswort -e "Mysql Befehle"

Wordpress
- /var/www/html/wp-config.cnf: Dort werden die Hauptkonfigurationen von Wordpress gespeichert aber dieses File muss vor der Installation  erstellt werden, sonst muss man die WP-Konfiguration übers GUI machen mit dem Browser.

## Even:

#### Stand vor Kurbeginn<br>
Eigentlich hatte ich kein richtig grossen Vorwissen zum Beginn dieses Kurses. Ich kannte zwar die wichtigsten Befehle von Windows hatte aber keine Erfahrung damit<br>
#### Stand 19.08.2020
Heute habe ich die zwei Tools Github und Vagrant kennengelernt. Bei Github konnte ich erfolgreich ein Repository erstellen und dieses per ssh mit dem Bash Terminal verküpfen. 
Vagrant ist dazu da um einfach automatisch VM zu installieren. Da wir ich die VM nutze war schon alles installiert und ich musste mich nur noch in die Anleitung reinslesen. Per Bash Terminal können wir nun darauf zugreigen und damit arbeiten<br>


#### Stand 02.09.2020
Heute habe ich viel Neues über den Fileshare Dienst samba gelernt. Ich habe erfolreich ein share erstellt und diesen per Vagrant automatisiert. <br>
Wichtige Befehle zu Samba:<br>
- `sudo apt-get -y install samba-common samba, sudo apt-get -y install tdb-tools` (installiert den Dienst und die Benutzerdatenbank von samba)<br>
- `sudo echo "xxx" >> /etc/samba/smb.conf` (Konfigurationsfile anpassen, zum erstellen des Shares/Freigaben)<br>
- `sudo mkdir /home/sambashare` (Ordner erstellen)<br>
- `sudo service smbd restart` (Samba Service neustarten)<br>
- `sudo ufw allow samba` (Firewall freischaltung für den Service Samba)<br>

Auch habe ich heute den Synchronistations Service gebraucht. <br>
Wichtige Befehle zu rsync:<br>
- `sudo rsync -a /home/sambashare /srv04_lx_fileserver` (rysnc [Option] [Daten] [Ziel], angeben des Backupziels und den zu sicherenden Daten)<br>
- `sudo apt-get -y install rsync` (Dienst installieren)
File per Script bearbeiten <br>
- `sudo echo "Text" >> Pfad zum File`  
<br>

## Jason:

#### Stand 19.08.2020
Ich habe gelernt wie man mit GitHub umgeht und ein Repository erstellt und synchonisieren kann.<br>
 
Für den Git-Client gibt es diverse wichtige Befehle:<br>
- `git add -A` (Änderungen registrieren/erkennen)<br>
- `git commit -m "Kommentar"` (Änderungen werden auf dem lokalen Gerät gespeichert)<br>
- `git push` (Änderungen werden auf GitHub geladen)

Ausserdem habe ich VirtualBox und Vagrant kennengelernt. Durch die Anleitungen auf GitHub konnte ich die Aufgaben ziemlich einfach durcharbeiten und die Plattformen kennenlernen.<br>

VirtalBox ist eine Plattform um VMs zu erstellen und verwalten, ähnlich zu VMWare.<br>

Mit Vagrant kann man VMs ganz einfach und schnell automatisch erstellen und installieren. Vagrant wird lokal installiert und muss in den Umgebungsvariablen unter path<br>
eingetragen werden. Danach kann man im Terminal/Bash vagrant aufrufen<br>

Wichtige Befehle für Vagrant:<br>
- `vagrant init ubuntu/xenial64` (init erstellt ein leeres vagrantfile, in diesem Beispiel wird eines mit ubuntu erstellt )<br>
- `vagrant up` (erzeugt und konfiguriert die VM anhand des vagrantfiles)<br>
- `vagrant ssh` (verbindet per ssh mit VM)<br>
- `vagrant halt` (beendet die VM)<br>
<br>

## Stand 02.09.2020
Ich habe heute den Kapitel 25 Sicherheit durchgearbeitet. Ich habe dabei vagrant näher kennengelernt und gelernt wie man mit einem Vagrantfile einen Server mit ReverseProxy<br>
und Firewall einstellungen als VM erstellt. Ausserdem habe ich gelernt wie man ein vagrantfile richtig konfigueriert und damit eine VM erstellt.<br>

Ich habe heute ein Vagrantfile erstellt um einen Reverse Proxy zu installieren. Der Folgende Code ist die Grundkonfiguration einer VM:
<br>

```Ruby
    #Grundkonfiguration der VM
    config.vm.define "srv05-lx-proxy" do |subconfig|    #Name für Vagrant
        subconfig.vm.provider "virtualbox" do |vb|    #Provider der VM Engine  
            vb.name = "srv05-lx-proxy"
            vb.memory = "512"   #Arbeitsspeicher
        end

    subconfig.vm.box = "ubuntu/xenial64"    #Vagrant Box
	subconfig.vm.hostname = "srv05-lx-proxy"    #Hostname
	subconfig.vm.network :private_network, ip: "10.0.0.14"  #IP-Konfiguration
	subconfig.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true  #Port weiterleitung
```
Mit Vagrant kann man der VM mitgeben was Sie beim aufsetzen installieren soll. In diesem Fall wird hier apache2 installiert, proxy Funktionen aktiviert, konfigurations-Files importiert und Firewall einstellungen vorgenommen.
<br>

```Ruby
    #Shell für den Proxy Server
    config.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update
        #Installation apache
        sudo apt-get -y install apache2 libxml2-dev
        #Reverse Proxy
        sudo a2enmod proxy
	    sudo a2enmod proxy_html
	    sudo a2enmod proxy_http
        #kopieren und verlinken der reverse proxy config datei
        sudo cp /vagrant/001-reverseproxy.conf /etc/apache2/sites-available/
        sudo ln -s /etc/apache2/sites-available/001-reverseproxy.conf /etc/apache2/sites-enabled/
        #Neustart der Dienste
        sudo service apache2 restart
        #Firewall regeln erstellen und Firewall aktivieren
        sudo ufw allow 80/tcp
        sudo ufw allow 22/tcp
        sudo ufw -f enable

        SHELL
    end
```
