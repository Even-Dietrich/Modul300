<h1>Allgemeine Bewertungskriterien</h1>
<br>
<p>K1 Umgebung wurde auf dem Notebook/VM in der TBZ cloud eingerichtet<br>
<p>K2 Unsere Lernumgebung einrichten</b>

<ul>
    <li>Ein Git-Client wird verwendet</li>
    <li>Dokumentation ist als Markdown vorhanden</li>
    <li>Markdowneditor wurde ausgewählt (Visual Studio Code)</li>
    <li>Markdwon ist Strukturiert</li>
    <li>Persönlicher Wissenstand wird dokummentiert und festgehalten</li>   
</ul>
</p>
<p>K3
    <ul>
       <li>Bestehende vm aus Vagrant-Cloud einrichten</li>
	   Alle Vagrantfiles im Verzeichnis Modul300/LB2/server<br>
       <li>Kennt die Vagrant-Befehle</li>   
       <li>Eingerichtete Umgebung ist dokumentiert (Umgebungs-Variablen, Netzwerkplan gezeichnet, Sicherheitsaspekte)</li>
       <li>Funktionsweise getestet inkl. Dokumentation der Testfälle- andere, vorgefertigte vm auf eigenem Notebook aufgesetzt</li>
	    VM können mit Vagrantfile erfolreich erstellt werden. <br>
       <li>Projekt mit Git und Mark Down dokumentiert</li>
       <li>Ein Git-Client wird verwendet</li>
       <li>Ein Git-Client wird verwendet</li
     </ul>
</p>
<p>K4 Sicherheitsaspekte sind implementiert-</b>
<ul>
   <li>Firewall eingerichtet inkl. Rules</li>
   <li>Reverse-Proxy eingerichtet</li>
   <li>Benutzer- und Rechtevergabe ist eingerichtet</li>
   <li>Zugang mit SSH-Tunnel abgesichert</li>
   <li>Sicherheitsmassnahmen sind dokumentiert</li>  
   <li>Projekt mit Git und Mark Down dokumentiert</li>  

	
</ul>
</p>

<br>
<br>

<h1>Netzwerkplan</h1>
Hier zeigen wir Ihnen unsere Umgebung auf die wir automatisch mit den Vagrantsfile erstellen können.<br>

<img src=Dokumentation/img/Netzwerkplan.jpg>

<h1>Persönlicher Wissenstand:</h1>
<br>
<h2>Adam:</h2>
<br>
<p>Stand vor Kursbeginn<br>
Ich habe vor dem Beginn des Kurses noch keine ahnung von GitHub und das Erstemal im Modul 300 damit gearbeitet. Ich kannte jedoch GitLab von meinem Geschäft, konnte aber bis jetzt noch nie damit in Kontakt gekommen.<br>

<h2>Alex:</h2>

<p>Stand 19.08.2020
Heute habe ich gelernt, wie man ein Github Repository mit meinem PC synchronisieren kann.<br>

Wichtige Befehl für den Git-Client:<br>
git add -A änderungen werden erkennt<br>
git commit -m "Kommentar" Die Änderungen werden auf dem Gerät gespeichert (lokal)<br>
git push Die Änderungen werden auf GitHub geladen.<br>

Desweiteren habe ich Vagrant kennen gerlernt. Damit kann man Konfigurationsdateien erstellen für VM, damit man nicht immer die VM manuell aufsetzten muss. </p>


<br>
<h2>Even:</h2>
<br>

<p>Stand vor Kurbeginn<br>
Eigentlich hatte ich kein richtig grossen Vorwissen zum Beginn dieses Kurses. Ich kannte zwar die wichtigsten Befehle von Windows hatte aber keine Erfahrung damit<br>
<p>Stand 19.08.2020<br>
Heute habe ich die zwei Tools Github und Vagrant kennengelernt. Bei Github konnte ich erfolgreich ein Repository erstellen und dieses per ssh mit dem Bash Terminal verküpfen. 
Vagrant ist dazu da um einfach automatisch VM zu installieren. Da wir ich die VM nutze war schon alles installiert und ich musste mich nur noch in die Anleitung reinslesen. Per Bash Terminal können wir nun darauf zugreigen und damit arbeiten<br>



<p>Stand 02.09.2020</p>
Heute habe ich viel Neues über den Fileshare Dienst samba gelernt. Ich habe erfolreich ein share erstellt und diesen per Vagrant automatisiert. <br>
Wichtige Befehle zu Samba:<br>
- sudo apt-get -y install samba-common samba, sudo apt-get -y install tdb-tools (installiert den Dienst und die Benutzerdatenbank von samba)<br>
- sudo echo "xxx" >> /etc/samba/smb.conf (Konfigurationsfile anpassen, zum erstellen des Shares/Freigaben)<br>
- sudo mkdir /home/sambashare (Ordner erstellen)<br>
- sudo service smbd restart (Samba Service neustarten)<br>
- sudo ufw allow samba (Firewall freischaltung für den Service Samba)<br>

Auch habe ich heute den Synchronistations Service gebraucht. <br>
Wichtige Befehle zu rsync:<br>
- sudo rsync -a /home/sambashare /srv04_lx_fileserver (rysnc [Option] [Daten] [Ziel], angeben des Backupziels und den zu sicherenden Daten)<br>
- 	sudo apt-get -y install rsync (Dienst installieren) <br>
<br>
<h2>Jason:</h2>
<br>
<p>Stand 19.08.2020<br>
Ich habe gelernt wie man mit GitHub umgeht und ein Repository erstellt und synchonisieren kann.<br>
 
Für den Git-Client gibt es diverse wichtige Befehle:<br>
- git add -A (Änderungen registrieren/erkennen)<br>
- git commit -m "Kommentar" (Änderungen werden auf dem lokalen Gerät gespeichert)<br>
- git push (Änderungen werden auf GitHub geladen)

Ausserdem habe ich VirtualBox und Vagrant kennengelernt. Durch die Anleitungen auf GitHub konnte ich die Aufgaben ziemlich einfach durcharbeiten und die Plattformen kennenlernen.<br>

VirtalBox ist eine Plattform um VMs zu erstellen und verwalten, ähnlich zu VMWare.<br>

Mit Vagrant kann man VMs ganz einfach und schnell automatisch erstellen und installieren. Vagrant wird lokal installiert und muss in den Umgebungsvariablen unter path<br>
eingetragen werden. Danach kann man im Terminal/Bash vagrant aufrufen<br>

Wichtige Befehle für Vagrant:<br>
- vagrant init ubuntu/xenial64 (init erstellt ein leeres vagrantfile, in diesem Beispiel wird eines mit ubuntu erstellt )<br>
- vagrant up (erzeugt und konfiguriert die VM anhand des vagrantfiles)<br>
- vagrant ssh (verbindet per ssh mit VM)<br>
- vagrant halt (beendet die VM)<br>
<br>
<p>Stand 02.09.2020<br>
Ich habe heute den Kapitel 25 Sicherheit durchgearbeitet. Ich habe dabei vagrant näher kennengelernt und gelernt wie man mit einem Vagrantfile einen Server mit ReverseProxy<br>
und Firewall einstellungen als VM erstellt. Ausserdem habe ich gelernt wie man ein vagrantfile richtig konfigueriert und damit eine VM erstellt.<br>
