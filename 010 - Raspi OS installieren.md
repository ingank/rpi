# Raspberry Pi OS installieren

Diese Kurzanleitung beschreibt die Installation von Raspberry Pi OS auf einem RaspberryPi.
An den RaspberryPi muss zur grundlegenden Netzwerk-Konfiguration weder Tastatur noch Bildschirm angeschlossen werden.
Der administrative Zugriff erfolgt im späteren Verlauf per LAN/IPv4/SSH.

## Betriebssystemdatenträger erstellen

Führe auf einem Ubuntu-Desktop-System nacheinander folgende Schritte aus:

* Lade das neueste Raspberry Pi OS herunter.
* Entpacke die .zip-Datei.
* Lege eine SD-Card ein.
* Starte 'Anwendungen anzeigen' -> 'Hilfsprogramme' -> 'Laufwerke'.
* Markiere das Laufwerk für die SD-Card.
* Gehe zu 'Drei waagerechte Striche' oben Links im Programmfenster.
* Klicke 'Laufwerksabbild wiederherstellen...'.
* Wähle im Dialog die entpackte .img-Datei.
* Klicke 'Wiederherstellung starten'.

Nach ca. 2 Minuten sollte das Image auf die SD-Card geschrieben sein.

## Konfiguration (out of the box)

* Markiere die nun vorhandene boot-Partition.
* Klicke Dreieck für 'Ausgewählte Partition einhängen'.
* Klicke auf den blau gefärbten Link hinter 'Eingehängt in'.

Im Dateimananger werden die Dateien der boot-Partition aufgelistet.

* Rechtsklick in freien Ordnerbereich -> 'In Terminal öffnen'.
* Im Terminal eingeben: `$ sudo touch ssh`
* Anfügen an Datei 'cmdline.txt': `ip=192.168.100.100:::255.255.255.0::eth0:off`
* Alle Dateien und Programme schließen, die auf die boot-Partition zugreifen.
* Klicke auf Quadrat im Programm 'Laufwerke' um die boot-Partition auszuhängen.
* Entnehme die SD-Card aus dem Ubuntu-Rechner.

Bemerkung:  
Das Netzwerksegment 192.168.100.0 wird in diesem Beispiel unabhängig vom meist genutzen 192.168.0.0 für administrative Aufgaben verwendet.
Da der die IPv4 192.168.100.100 direkt über einen Kernel-Boot-Paramter erzeugt wird,
ist eine missliche Konfiguration über die üblichen Systemwerkzeuge zumindest für diese Adresse (fast) ausgeschlossen.

Weiterführende Informationen zum Kernel-Paramter 'ip=':
* [Dokumentation auf kernel.org](https://www.kernel.org/doc/html/latest/admin-guide/nfs/nfsroot.html#kernel-command-line)
* [deutschsprachiges Dokument zum Thema](http://www.netzmafia.de/skripten/hardware/RasPi/RasPi_Install.html#initip)


## Erstes Booten des RaspberryPi und Zugriff mittels ssh

* Lege SD-Card in den RaspberryPi ein und versorge ihn mit Betriebsspannung.
* Richte auf dem Ubuntu-Rechner eine zweite IPv4 (beispielsweise 192.168.100.200) auf dem Ethernet-Interface ein.
* Öffne einen Terminal auf dem Ubuntu-Rechner.
* Im Terminal eingeben: `$ ssh pi@192.168.100.100`
* Das Standardpasswort lautet: **raspberry**

## Standardpasswort ändern

Direkt nach dem ersten Login **muss** das voreingestellte Passwort geändert werden:

```
pi@raspberrypi:~ $ passwd
Changing password for pi.
Current password: 
New password: 
Retype new password: 
passwd: password updated successfully
```