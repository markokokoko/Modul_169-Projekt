# Inhalt
- Vorgehen
- Port ändern alter Moodle-Instanz
-
-
-

## Port ändern alte Moodle-Instanz
Die alte Moodle-Instanz läuft aktuell auf dem Port 80. Nach Anforderungen muss die alte Moodle-Instanz nach der Migration weiterhin erreichbar sein, jedoch über den Port 8080. 
Damit die Moodle-Instanz über den Port 8080 läuft, müssen folgende Config-Files angepasst werden:

1. ports.conf Datei anpassen:
Die Datei findet man unter "etc/apache2"
