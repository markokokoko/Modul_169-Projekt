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

5. Moodle-Installation
- Installation durchführen

6. Migration auf neuste Version
- Moodle aktualisieren auf Version 4.4

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
[Anpassungen für die alte Moodle-Instanz](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Dokumentation/Anpassung_AltesMoodle.md)

## Container Umgebung erstellen
### Docker-Compose-File ausführen
Die alte Instanz läuft nun auf Port 8080. Daher ist der Port 80 nun nicht mehr besetzt. 
Nun kann man also das Docker-Compose-File ausführen und zwar wie folgt.

1. Darauf achten, dass das Dockerfile und das Docker-Compose-File im gleichen Verzeichniss liegt. (In dieser Anleitung liegen die Files Im home Verzeichnis )

2. Docke-Compose-File ausführen (Dies kann eher lange dauern: ```bash docker-compose up -d```

Nun werden die Container, Volumes, das Image und das Netzwerk erstellt. 

## Datenmigration
Am Anfang wurde bereits ein Backup (Dump) erstellt. 

1. Dump in den Datenbank-Container kopieren. Dies wird gemacht mit (Name des Dumps spielt keine Rolle):
```bash docker cp moodledata.sql <ContainerID>:/tmp/moodledata.sql```
![kopieren](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/dumkopieren.png)

2. Bash vom mariadb Container öffnen & anschliessen den Dump importieren:
```bash docker exec -it <containerID> /bin/bash```
```bash mariadb -u user -p moodle /tmp/moodledata.sql```
![importieren](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/importierendump.png)

3. Überprüfen der Moodleseite unter http://localhost:80/
![Startseite](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/startseite2.png)

## Moodle-Installation
Die Moodle-Seite konnte aufgerufen werden. Nun kann man der Installation Schritt-für-Schritt folgen:
1.
![Plugin](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/startseite2.png)

2.
 ![Einstellung](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Datenbankeinstellung.png)

3. Datenbank Angaben einfügen:
![Daten](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/datenbankeinstellungenuser.png)

4. Nun wird aufgefordert Moodle zu aktualisieren
![aktuell](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/aktualiseren1.png)

5. Nun kommen Server Überprüfungen, bei der man nach unten scrollen und auf "weiter" klicken kann.
![server](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/aktuellversininfomratin.png)
![weiter](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/weiterepf%C3%BCrung.png)

6. Jetzt werden die Plugins überprüft (Nach unten scrollen und auf "Aktualisieren der Datenbank starten" klicken:
![plugin](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Plungpruefung.png)
![starten](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/aktualisserendruecken.png)

7. Nun wird die Version aktualisiert (ebenfalls unten auf "weiter":
![aktualisieren](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/aktualsieren.png)

8. Es wird nun noch aufgefordert, eine Support-Contact-Email anzugeben:
![support](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/support.png)

9. Nach dem aktualisieren kann man sich nun mit dem Benutzer anmelden:
![anmelden](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/Login.png)

10. Nun ist man bei Moodle drin und man kann die Kurse etc. schon einsehen. Jedoch ist Moodle noch nicht auf der aktuellsten Version. Dafür muss man nun das Moodle auf die Version 4.4 aktualisieren.
![nachlogin](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/nachloginetc2.png)

## Moodle auf neuste Version aktualisieren












