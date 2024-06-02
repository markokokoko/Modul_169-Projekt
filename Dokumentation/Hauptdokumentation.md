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



### Docker-Compose-File ausführen
Die alte Instanz läuft nun auf Port 8080. Daher ist der Port 80 nun nicht mehr besetzt. 
Nun kann man also das Docker-Compose-File ausführen und zwar wie folgt.

1. Darauf achten, dass das Dockerfile und das Docker-Compose-File im gleichen Verzeichniss liegt. (In dieser Anleitung liegen die Files Im home Verzeichnis )

2. Docke-Compose-File ausführen (Dies kann eher lange dauern: ```bash docker-compose up -d```

Nun werden die Container, Volumes, das Image und das Netzwerk erstellt. 





