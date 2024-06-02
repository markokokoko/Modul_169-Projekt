# Inhalt
1. Vorbereitung
- Backup der alten Moodle-Instanz (SQLDump)
- VM Updates durchführen & Benötigte Extension etc. installieren

2. Anpassung alte Moodle-Instanz
- Port ändern
- Als alte Instanz kennzeichnen

3. Container Umgebung erstellen
- Docker-Image erstellen
- Docker-Compose File ausführen

4. Datenmigration
- Dump in Container exportieren
- Dump importieren in die neue Datenbank

5. Überprüfen
- Lösungen & Tests

## 1. Vorbereitung
### Backup erstellen
Bevor auf der VM irgenwelche Änderungen vorgenommen werden, wird zuerst ein Backup erstellt.
Dafür führt man folgenden Befehl im Terminal aus: ```bash mysqldump -u root -p moodle > MoodleDump.sql```
![Dump](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Dump.png)

Das File wurde nun im aktuellen Verzeichnis abgepseichert. (/home/vmadmin).
![DumpFile](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/dumpFile.png)

### VM Updates & weitere benötigte Features
Da die VM nicht auf dem aktuellen Stand ist und recht veraltet ist, ist es wichtig vor der Migration die VM auf den neusten Stand zu bringen. Werden die Updates etc. nicht durchgeführt ist es nicht möglich die Container einwandfrei zu starten.

Folgende Schritte müssen durchgeführt werden (Befehle können 1zu1 kopiert werden):

- Paketlisten aktualisieren: ```bash sudo apt update```
- Upgrade aller installierten Pakete: ```bash sudo apt upgrade```

- Docker-Compose installieren: ```bash apt install docker-compose```
- Maschine neustarten: ```bash sudo reboot```



Nach diesen Schritten ist die VM nun ready für die weiteren Schritte.

## 2. Anpassungen alte Moodle-Instanz
### Port ändern
Die alte Moodle-Instanz läuft aktuell auf dem Port 80. Nach Anforderungen muss die alte Moodle-Instanz nach der Migration weiterhin erreichbar sein, jedoch über den Port 8080. 
Damit die Moodle-Instanz über den Port 8080 läuft, müssen folgende Config-Files angepasst werden:

1. ports.conf Datei anpassen:
Die Datei findet man unter "/etc/apache2". In der Datei passt man nun den Port 80 -> 8080 an:
![Ports.Conf](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/ports.conf.png)

2. 000-default.conf Datei anpassen:
Die Datei findet man unter "/etc/apache2/sites-enabled". In dieser Datei ändert man den Port in der ersten Zeile zu Port 8080:


![000-default-sites](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/000-default.conf.png)

4. config.php Datei anpassen:
Die letzte Datei welche angepasst werden muss, ist die config.php Datei. Da dies eine Read-Only Datei ist, kann man die Datei über das Terminal öffen und bearbeiten:
![config.php1](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/config.php.png)

In der Datei wird nun unter "$CFG->wwwroot" die Adresse angepasst, indem man nach localhost den Port hinzufügt:
![config.php](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/config.phpAendern.png)

4. Nachdem die drei Dateien angepasst wurden, kann man nun apache2 neustarten mit: "sudo systemctl restart apache2". 
Über den Link "http://localhost:8080/" gelangt man nun zu der alten Moodle-Instanz:
![altesMoodle](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/altes_moodle.png)

### Alte Moodle-Instanz erkennbar machen
Als Anforderung wurde eingebracht, dass die alte Moodle-instanz klar erkennbar sein soll.
Um dies direkt auf der Startseite zu kennzeichnen, kann man folgende Schritte beachten:

1. Einloggen als Administrator:
![einloogen](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Loginaltesmoodle.png)

2. Klicke nun auf "Website-Administration"
![WebsiteAdministration](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Website_Administration.png)

3. Scrolle nun bis zu "Startseite Einstellungen" und klicke auf "Einstellungen"
![Startseite Einstellungen](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Startseite_Einstellung.png)

4. Nun kann man den Namen etc. anch eigenen Vorstellungen anpassen:
![NamenAnpassen](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/namenaendern.png)

5. Ausloggen und Startseite überprüfen:
![neuestartseite](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/neuestartseite.png)


### Docker-Compose-File ausführen
Die alte Instanz läuft nun auf Port 8080. Daher ist der Port 80 nun nicht mehr besetzt. 
Nun kann man also das Docker-Compose-File ausführen und zwar wie folgt.

1. Darauf achten, dass das Dockerfile und das Docker-Compose-File im gleichen Verzeichniss liegt. (In dieser Anleitung liegen die Files Im home Verzeichnis )

2. Docke-Compose-File ausführen (Dies kann eher lange dauern: ```bash docker-compose up -d```

Nun werden die Container, Volumes, das Image und das Netzwerk erstellt. 





