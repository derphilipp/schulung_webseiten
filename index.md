name: inverse
layout: true
class: left, middle, inverse
---

# Wordpress und Alternativen

## Statische und dynamische Webseiten für die eigene Homepage ##

Philipp Weißmann und Jürgen Krauß

* [mail@philipp-weissmann.de](mailto:mail@philipp-weissmann.de)
* [oh-mein-gott@es-ist-ein-krauss.de](mailto:oh-mein-gott@es-ist-ein-krauss.de)

---

# Agenda

* Übersicht
* Motivation
* Statische Webseiten
    * Hostingmöglichkeiten
    * Arbeiten mit Hugo
    * Aufsetzen einer Seite mit Hugo
* Dynamische Webseiten mit Wordpress
    * Hostingmöglichkeiten
    * Aufsetzen von Wordpress
    * Plugins & Best Practices
* Fragen und Antworten

---

# Begriffe 1

* Fontend
  * "Alles was im Browser passiert"
* Backend
  * "Alles, was auf dem/den Server(n) passiert

---

# Begriffe 2

* Application-Server
  * Programm auf Server
  * Liefert HTML/JSON/Datenströme etc.
* Webserver
  * "Öffentlich" erreichbarer Dienst, "Anlaufstelle" für Browser
* Reverse-Proxy
  * Spezialisierter Webserver
  * Leitet Anfragen zu Application-Server um/durch

---

# Begriffe 3

* Dynamische Webseiten
  * Seiten mit Application-Server oder Skripten auf der Serverseite
  * "Der Server kann unterschiedliche Inhalte ausliefern"
* Statische Webseiten
  * Seiten mit fixem HTML/Daten auf der Serverseite
  * "Der Server liefert stets die gleichen Daten/Seite aus"

**Achtung:** Die Frontend-Repräsentation (z.B. mittels Javascript) mit interaktiven Webseiten hat damit nichts zu tun!

---

# Application-Server

* In Beliebiger Sprache geschriebenes Programm
* Läuft i.d.R. als dauerhaft laufender Dienst auf einem Server
* Bietet oft HTTP an
* Keine Härtungen oder Caching
* i.d.R. nicht "direkt" öffentlich zugänglich
* Beispiel: *flask* (python), *nodejs* (javascript)

---

# Webserver

* Manche Webserver können Module laden
* Skripte (z.B. cgi) oder mit Modulen können Skripte ausgeführt werden
* Skripte o.ä. laufen nur "on demand"
* Kann Datenstrom verschlüsseln (HTTPS)
* Kann Cachen
* Sehr Sicherheitsrelevant (Härten etc.)
* Beispiele: Apache, nginx, lighttpd

---

# Reverse-Proxy

* Wird "vor" eine (oder mehrere) Application-Server geschaltet
* Öffentlich erreichbar
* Leitet vor/an die jeweiligen Application-Server Daten
* Beispiele: nginx, træfik

---


# Architektur Beispiel 1: Synchronisierte Einkaufsliste

* Frontend: *vue*
* NoSQL Datenbank: *mongodb*
* Datenbank-Cache: *redis*
* Application-Server: *nodejs*
* Reverse-Proxy: *nginx*

---

# Architektur Beispiel 2: Wordpress Seite

* Frontend: *jquery*
* Relationale Datenbank: *mariadb*
* Webserver: *apache*  mit *modphp*

---

# Architektur Beispiel 3: Statische Webseite

* Frontend: *react*
* Webserver: *nginx*

---

# Statische Webseiten

* Motivation:
  * Ein Angriffsvektor weniger
  * Hosting extrem günstig/einfach
  * Keine Updates der Homepage notwendig
  * Backup & Umzug extrem einfach
  * Enorm gute Performance

---

# Statische Webseite erstellen
## Möglichkeiten

* HTML Seite selbst schreiben
  * Tiefes Wissen über HTML notwendig
  * Anpassungen dauern sehr lange
  * Läuft in jedem (aktuellen) Browser
  * Empfehlung: *selfhtml*
* Seite mit JavaScript Framework schreiben
  * Wissen über JavaScript Framework notwendig
  * Läuft nicht in Browsern mit deaktivierem JavaScript
  * Empfehlung: *vue*
* Seite generieren
  * Erstellt aus Daten + Theme eine statische Webseite
  * Praktisch kein Wissen über HTML oder JavaScript notwendig
  * Erstellen & erweitern extrem schnell
  * HTML / JavaScript ergebnis je nach Generator unterschiedlich
  * Empfehlung: *hugo*

---

# Weitere Möglichkeiten 1

## WYSIWYG

* "What you see is what you get"
* "Zusammenklicken" von Inhalten / Seitenelementen
* Beispiele: Frontpage, iWeb, Microsoft Word, LibreOffice/Openoffice Writer
* Ergebnis sieht je nach Browser oft sehr unterschiedlich aus
* Zumeist sehr unflexibel, inkonsistent, keine modernen Bedienelemente
* Nahezu ausgestorben

---
# Weitere Möglichkeiten 2

## Homepage-Generatoren

* Hosting-Angebote erlauben das Zusammenklicken von Webseiten
* Zumeist bekommt man keine HTML Dateien, sondern nur das komplette Hosting
* Umziehen damit praktisch nicht möglich
* Oft keine individuellen Themes/Erweiterungen möglich - oder diese kosten extra

---

# Neue Lösungen
## Statische Webseiten Generatoren

* Markdown Homepage-Generatoren
* Erstellen aus Markdown statische Webseiten
* Für Kurs relevant: *hugo*
* Weitere populäre Generatoren:
  * Pelican (Python)
  * Jekyll (Ruby)

---

# Hugo

* Geschrieben in Go(lang)
* Open Source
* Verwandelt Markdown in Webseiten

---

# Markdown

* Auszeichnungssprache
* Populär
* Omnipräsent

---

# Content here

---

# Kontakt:
## Philipp Weißmann

* [mail@philipp-weissmann.de](mail@philipp-weissmann.de)

## Jürgen Krauß

* [oh-mein-gott@es-ist-ein-krauss.de](mailto:oh-mein-gott@es-ist-ein-krauss.de)