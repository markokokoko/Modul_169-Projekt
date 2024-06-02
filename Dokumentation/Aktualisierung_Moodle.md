## Moodle auf v4.4 Aktualisieren (neuster Stand)
Moodle ist nun auf der Version 4.1. Die Anforderungen von dem Projekt ist aber, das die neuste Moodle-Version verwendet wird.
Dafür müssen nun folgende Schritte erledigt / gemacht werden.

1. Im Terminal, in den Moodle-Container wechseln:
![wechseln](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/moodlecontainer.png)

2. Im Container muss man als erstes in folgendes Verzeichnis wechseln: ```bash cd /var/www/html/moodle```
![verzeichnis](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/verzeihcniss%20wechseln.png)

4. Nun wird das Verzeichnis zu den "sicheren" Verzeichnissen hinzugefügt. Dies ist notwenidg, wenn Git den Zugriff aufgrund der Sicherheit einschränken möchte.
```bash git config --global --add safe.directory /var/www/html/moodle```

5. Nun wird die E-Mail-Adresse gesetzt. Dies ist dafür da, das bei jedem Git-Commit der Autor authentifizert werden kann.
```bash git config --global user.email "ramsauerr2@gmail.com"```

6. HIer iwrd nun noch der Git-Benutzername gesetzt, welcher ebenfalls für die Authentifizierung benötigt wird.
```bash git config --global user.name "Roman"```
![bilder](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/configahpasse.png)

7. Dies ist der nächste Befehl, welcher ausgeführt werden muss. Der ist nützlich, um sicherzustellen, dass man die neusten Änderungen von allen Remote-Repositories erhält:
```bash git fetch --all```
![fetch](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/gitfetchall.png)

8. git stash wird nun ausgeführt das keine ungesicherten Änderungen im Verzeichnis sind und dieses sauber ist.
```bash git stash```
![stash](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/gitstash.png)

9. Nun wird ein Befehl verwendet um zum Branch "MOODLE_404_STABLE" wechselt.
```bash git checkout MOODLE_404_STABLE```
![stable](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/gitcheckout.png)

10. Mit diesem Befehl kann man nun die Branches überprüfen:
```bash git branch```
![gitbranch](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/gitbranch.png)

11. Nun kann man die Moodle-Seite reloaden und kommt nun auf folgende Seite. Nun wird angefordert ein Versions-Upgrade auf v4.4+ zu machen. Hier kann man nun die Updates etc. wieder durchklicken wie beim Abschnitt "Moodle-Installation erklärt"
![upgrade44](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/upgradeto44.png)

12. Auf folgender Seite ist noch anzumerken, dass man hier ein häckchen setzten kann und dadruch ebenfalls weiter machen kann.
![sms](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/smsmobnilphone.png)

13. Auf folgender Seite, müssen keine Änderungen vorgenommen werden. Man kann nach unten scrollen und auf weiter klicken:
![weiterklicken](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/moodlemodul169.png)


14. Wir man nun sehen kann, ist Moodle auf der aktuellsten Version:
![uptodate](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/moodleuptodate.png)


