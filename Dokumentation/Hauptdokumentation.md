# Inhalt
- Vorgehen
- Port ändern alter Moodle-Instanz
-
-
-

## Anpassungen alte Moodle-Instanz

### Port ändern
Die alte Moodle-Instanz läuft aktuell auf dem Port 80. Nach Anforderungen muss die alte Moodle-Instanz nach der Migration weiterhin erreichbar sein, jedoch über den Port 8080. 
Damit die Moodle-Instanz über den Port 8080 läuft, müssen folgende Config-Files angepasst werden:

1. ports.conf Datei anpassen:
Die Datei findet man unter "/etc/apache2". In der Datei passt man nun den Port 80 -> 8080 an:
![Ports.Conf](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/ports.conf.png)

2. 000-default.conf Datei anpassen:
Die Datei findet man unter "/etc/apache2/sites-enabled". In dieser Datei ändert man den Port in der ersten Zeile zu Port 8080:
![000-default-sites](https://github.com/markokokoko/Modul_169-Projekt/blob/main/Bilder/000-default.conf.png)

3. config.php Datei anpassen:
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


