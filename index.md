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

# Praxis Hugo

---

# Installation
* Paketmanager: `apt install hugo`, `pacman S hugo`, etc.
* Homebrew: `brew install hugo`
* Installationsanleitung unter Windows: [https://gohugo.io/getting-started/installing/](https://gohugo.io/getting-started/installing/)

---

# Starten einer neuen Seite

* `hugo new site hugo-webseite`
* Theme installieren,
  * Hier: [Theme Ananke](https://github.com/budparr/gohugo-theme-ananke/archive/2.40.zip)
  * Entpacken nach *themes/ananke* (ggf. Verzeichnisname ändern)
* Anpassen von `config.toml`

```
baseURL = "http://meine-wunderbare-webseiten-url.de/"
languageCode = "en-us" # Spracheinstellung für das Theme
title = "Meine wunderbare Homepage"
theme = "ananke"
```

* Praxistipp: Theme via Git als Submodul einbinden!

---

# Erster Eintrag

* Erstellen einer ersten Seite aus einem Template
* `hugo new posts/hugo.md`
* Inhalt schon durch Template in Teilen vorgegeben:

```
---
title: "Hugo"
date: 2019-03-08T15:53:00+01:00
draft: true
---

# Hugo

Dies ist meine Webseite.
Alle Inhalte sind in Markdown geschrieben und werden als HTML dargestellt.
```

---

# Webseite testen

* `hugo serve -D`
* Starten Webserver zum lokalen Testen der Webseite, inklusive "Drafts"
* Zum öffnen Link auf der Kommandozeile folgen: http://localhost:1313
* Erstellt Seiten bei Änderungen sofort neu (auch Warnungen auf der Ausgabe beachten!)

---

# Webseite erstellen

* `hugo`
* Erstellt in `public` Verzeichnis HTML Seiten
* Beinhaltet (je nach Theme) jedoch oft absolute Pfade

---

# Markdown-Elemente 1

* Überschriften:
```md
# Überschrift Level 1
## Überschrift Level 2
### Überschrift Level 3
```

---

# Markdown-Elemente 2

* Formatierung:
```md
*Kursiv*
**Fett**
~~Durchgestrichen~~
`Code`
```

---

# Markdown-Elemente 3

* Code-Block:
    `````md
    ```python
    # Codeblock
    import sys

    def goodbye():
        sys.exit(0)
    ```
    `````

---

# Markdown-Elemente 4

* Aufzählung
    ```md
    * Auf...
    * ...zählung
    ```
* Numerierte Aufzählung
    ```md
    1. Eins
    2. Zwei
    3. Drei
    ```
* ToDos:
    ```md
    - [ ] ToDo
    - [ ] Listen
    - [x] Eintrag
    ```

---

# Markdown-Elemente 5

* Tabellen
```md
| Tabelle   | Inhalt |
| --------- | ------ |
| Eintrag 1 | Wert 1 |
| Eintrag 2 | Wert 2 |
```

* Tipp: Markdown Plugins für Editoren sorgen für einfaches schreiben von Tabellen (z.B. Visual Studio Code)

---

# Markdown-Elemente 6


* Definitionen
    ```md
    Definition
    : genaue Bestimmung eines Begriffes

    Beispiel
    : typischer Einzelfall
    ```

* Fußnoten
    ```md
    Fußnote.[^1]

    ...

    [^1]: Fußnotentext
    ```


---

# Markdown-Elemente 7

* Links
    ```md
    https://wikipedia.org
    [Wikipedia](https://wikipedia.org)
    [Wikipedia](https://wikipedia.org "The Free Encyclopedia")
    [Wikipedia][WikiPediaSeite]
    [Wikipedia][1]

    ...

    [WikiPediaSeite]: https://wikipedia.org
    [1]: https://wikipedia.org
    ```

---

# Markdown-Elemente 8

* Das Verzeichnis `static` wird zum Speichern statischer Inhalte verwendet
* Auch Unterverzeichnisse möglich
* Beispiel: Lege Bilddatei unter `static/img/igel.jpg` ab
* Referenziere diese in einer neuen Seite: `hugo new post/igel.md`

```md
Hier ist ein Bild eines Igels:
![Alt Text für Barrierefreiheit!](/img/igel.jpg "Mouseover-Text")

Das gleiche Bild:
![alt text][igel]

...

[igel]: /img/igel.jpg "Mouseover-Text"
```

---

# Statische Seite bei github.com 1

1. Auf [github.com](https://github.com) anmelden
2. Projekt erstellen (public). Name: `BENUTZERNAME.github.io`
3. In `config.toml` folgenden Wert setzen: `canonifyURLs = true`
4. Hugo generieren: `hugo`
5. `public` Verzeichnis als Repository intialisieren: In Verzeichnis: `git init .`
6. Alle Dateien der Verzeichnisses rekursiv hinzufügen: `git add .`
7. Commiten: `git commit -am "Initial commit"`
8. Serververbindung herstellen: `git remote add origin git@github.com:derphilipp/example_page.git` (Hier Pfad von github einstellen)
9. Daten auf Server pushen `git push -u origin master`
10. Einstellung auf Github:
  * Settings
  * Github Pages
  * Source auf `master branch` setzen

---

# Statische Seite bei github.com 2

1. Wichtig: Geht nur mit Projektname `BENUTZERNAME.github.io`
2. Checken, ob sie Seite auch unter https://BENUTZERNAME.github.io erreichbar ist
3. Auf Github die eigene Domain (oder Subdomain) eintragen:
   * Settings
   * Github Pages
   * Custom Domain
4. Für Subdomain (z.B. `www.beispiel.de`) einen `CNAME` eintrag auf `BENUTZERNAME.github.io` setzen
5. Für Domain (z.B. `beispiel.de`) einen `A` oder `ALIAS` / `ANAME` Eintrag machen. Aktuelle IP Adressen von Github auf den Github Hilfeseiten abrufen
6. Nach (spätestens) 24 Stunden funktioniert auch HTTPS Transport

---

# Statische Seite: Tipps

* Github liefert direkt mit HTTPS aus
* Eigene Domains können eingetragen werden
* Supergünstige eigene Homepage:
  * Seite bei Github.com hosten
  * Blanke Domain z.B. bei Amazon bestellen
  * Einrichten einer Route der eigenen Domain auf die statische Seite

---

# Fazit statische Seiten Pro

* Statische Webseiten können genau so schick sein wie dynamische
* Eigene Homepage kann sehr kostengünstig erstellt werden
* Markdown zu HTML ist ein einfacher und schneller Weg zu arbeiten
* Hosting bei github.com erspart sämtliche Hostingkosten
* Keine dauerhafte Pflege
* Auch bei anderen Hosts gibt es günstige Angebote (oft inklusive Domain)
* Sicherheitsaspekt liegt komplett beim Hosting-Anbieter

---

# Fazit statische Seiten Contra

* Kein einfaches Hochladen von Photos vom Handy direkt auf die Seite
* Mobiles Editieren nicht/schwer möglich
* Zum Editieren der Seite stets der Computer notwendig
* Kein Interaktivität (Gästebuch, Bildupload, Kommentare) möglich
* Metriken nur über Webserver erfassbar (z.B. Seitenabrufe)

---

# Wordpress ist:

* ein Content-Management-System (CMS) mit Fokus auf das Bloggen
* entwickelt von der Wordpress Foundation
* 2003 erstmals erschienen
* open source ("GPL-2.0+"-Lizent)
* erhältlich in 62 Sprachen

---

# Wordpress ist:

![Schweizer Taschenmesser](https://media.giphy.com/media/xT5LMxAxpGSb5AZt8A/giphy.gif)

---

## 32,8 Prozent aller Webseiten basieren auf Wordpress

(*Quelle: W3Techs (abgerufen am 11.1.2019), https://w3techs.com/technologies/overview/content_management/all*) 

???
* Spricht irgendwie für WordPress
* Spricht aber auch irgendwie dagegen
* Andere sind Joomla (2. Platz mit 6 Prozent), Drupal, Typo 3, blankes HTML …
* Knapp 60 Prozent der Webseiten, die ein CMS nutzen, verwenden Wordpress

---

# Wofür sich Wordpress eignet

* Blogs
* private Webseiten mit regelmäßigen Updates
* kleine Shops
* Webprojekte mit mehreren Beteiligten in kleinem und mittlerem Umfang

---

# Wofür sich Wordpress nicht eignet

* große, internationale Unternehmensseiten
* komplexe Shop-Systeme mit ERP-Anbindungen
* statische Webprojekte
* Seiten mit besonderen spezifischen Anforderungen
* Arbeiten mit vielen Medien/Dokumenten
* Foren mit vielen Benutzern

---

# Grundlagen
## Aufbau

### 1. Wordpress
=> Core-Dateien und Datenbank
### 2. Inhalte
=> Seiten, Beiträge, Medien
### 3. Design
=> Themes
### 4. Funktionalitäten
=> Plugins


---

# Grundlagen
## Aufbau
.right[![Dateien und Verzeichnisse](https://es-ist-ein-krauss.de/wordpress-schulung/01_files_and_folders.png)]
### 1. Wordpress
Neben den Core-Dateien, ist vor allem ein Verzeichnis für uns interessant:

wp-content/
* Plugins
* Themes
* Uploads

---

# Grundlagen
## Aufbau
.right[![Datenbank](https://es-ist-ein-krauss.de/wordpress-schulung/02_database.png)]
### 1. Wordpress
Die Datenbank enthält:
* Einstellungen
* Inhalte
* Beiträgestexte
* Nutzer
* Meta-Informationen

---

# Grundlagen
## Aufbau
### 2. Inhalte

**Seiten:**
* feststehende Inhalte
* Evergreens mit oder ohne regelmäßigem Aktualisierungsbedarf\*
* Beispiel: _Impressum_

**Beiträge:**
* regelmäßige Informationen
* Content mit begrenzter Halbwertszeit\*
* Beispiel: _Die 5 besten Death-Metal-Bands aus Franken_

???
\** mit Ausnahmen – Seiten: ohne Datumsangabe stets aktuelle – Beiträge: mit Erstellungsdatum, aber bei Bedarf Aktualisierungen

---

# Grundlagen
## Aufbau
.right[![Design](https://es-ist-ein-krauss.de/wordpress-schulung/03_theme.png)]
### 3. Design
sogenannte Themes bestimmen:
* Look and Feel
* Farben, Schriften und Hintergründe
* Anordnung der Elemente
* zum Teil auch: Funktionalitäten

---

# Grundlagen
## Aufbau
.right[![Vielseitigkeit](https://i.giphy.com/media/1hBWtlec4aAb37ggn8/giphy.webp)]
### 4. Funktionalitäten
aktuell\* mehr als **_54.200 Plugins_** erweitern den Funktionsumfang – und verwandeln Wordpress in:
* Forum oder soziales Netzwerk
* Online-Shop
* Wiki
Crowdfunding-Plattform
* Buchungssystem 
* …

\*_Quelle: [Wordpress.org](https://wordpress.org/plugins/) (abgerufen am 11.1.2019)_

---

# Grundlagen
## Aufbau
### Außerdem

Viele Seiten bringt Wordpress automatisch mit:
* Kategorieübersicht
* 404-Fehler
* Suchergebnisse
* etc.

Dazu später mehr.

---

# Erste Schritte
## Installation
--

### Voraussetzungen
* dynamischer Webspace
  * Apache oder Nginx
  * PHP (> 7.3)

* Datenbank
  * MySQL (> 5.6)
  * oder: MariaDB (> 10.0)

---

# Erste Schritte
## Installation
### Voraussetzungen
* eigener Server (zu Hause oder im Rechenzentrum)
* allgemeine Hoster (1 & 1, all-inkl, Strato, etc.)
* spezialisierte Bloghoster (Raidboxes, wordpress.com, etc.)

---

# Erste Schritte
## Installation
### Schritt 1: Download
Vorsicht: 
* [de.wordpress.com](https://de.wordpress.com) => kommerzieller Hosting-Service
* [de.wordpress.org](https://de.wordpress.org) => Wordpress-Download (open source)

mehr dazu hier: [https://de.wordpress.com/com-vs-org/](https://de.wordpress.com/com-vs-org/) 

---

# Erste Schritte
## Installation
### Schritt 1: Download
Download unter:
* [https://de.wordpress.org/latest-de_DE.zip](https://de.wordpress.org/latest-de_DE.zip)

---

# Erste Schritte
## Installation
### Schritt 2: Datenbank vorbereiten
Datenbankverwaltung:
* http://127.0.0.1/phpmyadmin 

* Benutzer: root
* kein Passwort

---

# Erste Schritte
## Installation
### Schritt 2: Datenbank vorbereiten
![Neue Datenbank](https://es-ist-ein-krauss.de/wordpress-schulung/04_new_database.png)]
[http://localhost/phpmyadmin/server_privileges.php?adduser=1](http://localhost/phpmyadmin/server_privileges.php?adduser=1) 

---

# Erste Schritte
## Installation
### Schritt 3: Grundkonfiguration
Wordpress-Installer: [http://127.0.0.1](http://127.0.0.1)

---

# Erste Schritte
## Installation
### Alternative
Für die Entwicklungsumgebung zu Hause:
* Xampp, Mampp, Lampp
* Docker [docker-compose.yaml](http://ktshannon.com/how-to-setup-wordpress-locally-with-docker-phpmyadmin-included/)
--

<video width="560" height="420" controls>
    <source src="https://es-ist-ein-krauss.de/wordpress-schulung/05_docker.mov" type="video/mp4">
</video>

---

# Erste Schritte
## In Frontend und Backend

(kurze Erinnerung)

**Frontend** <= was Besucher sehen
* [http://127.0.0.1/](http://127.0.0.1/)

**Backend** <= Arbeit und Content-pflege „hinter den Kulissen“
* [http://127.0.0.1/wp-admin](http://127.0.0.1/wp-admin)

???
Im Frontend: Hier sehen wir erstmal nicht viel. Es gibt:
* einen Titel
* einen "Hallo Welt"-Beitrag
* ein paar Links
* einen Bereich mit weiteren Links
* ein Suchfeld
=> relativ langweilig für den Anfang

Schauen wir lieber mal ins Backend.
(Wechseln über die Leiste oben)

---

# Erste Schritte 
## Im Backend

Elemente eines Beitrags:
* Titel
* Text und Bild (Blöcke)
* Kategorien
* Schlagwörter
* Beitragsbild
* Auszug
* Meta-Informationen:
  * Link
  * Veröffentlichungsdatum

---

# Erste Schritte 
## Im Backend

Elemente einer Seite:
* Titel
* Text und Bild (Blöcke)
* Beitragsbild
* Meta-Informationen:
  * Link
  * Veröffentlichungsdatum

---

# Erste Schritte 
## Im Backend

In ähnlicher Form kann es auch weitere Inhaltstypen geben, die sogenannten `Custom Post Types` – die unterscheiden sich jeweils in den Feldern, die hier auszufüllen sind, im Design und je nach Theme auch in der Darstellung. Je nach Plugins und Themes könnten das beispielsweise sein:
* Portfolio
* Referenzen
* Kundenstimmen
* Podcast-Episoden
* und, und, und

Mehr dazu [hier](https://www.drweb.de/wordpress-intern-einstieg-custom-post-types-50402/)

---

# Erste Schritte
## Aufgabe:
* Anlegen und veröffentlichen **einer Seite**
* Anlegen und veröffentlichen von **mindestens zwei Beiträgen**, inklusive:
  * Beitragsbild
  * Kategorie
  * Schlagwörter

Ideenlos beim Text? 
  => [Franconian Ipsum](https://www.frankenipsum.de/index.php)
  
???
Danach Check im Frontend: Wie sehen Seiten aus, wie Beiträge, was sind Kategorien, wie sehen Schlagwort-rchive aus, etc.

---

# Ein Wordpress? Mein Wordpress! 
## Level 0: Einstellungen  

**Aufgabe:**
* Erkunden der Einstellungen
* Was würden Sie spontan ändern? Warum?

???
Permalinks, Umstellung auf SSL, Diskussion (besonders im Hinblick auf die DSGVO interessant), Datenschutz

---

# Ein Wordpress? Mein Wordpress! 
## Level 1: Customizer
[http://127.0.0.1/wp-admin/customize.php](http://127.0.0.1/wp-admin/customize.php)
![Customizer](https://es-ist-ein-krauss.de/wordpress-schulung/06_customizer.png)]

???
Erstmal nur: 
* Webseiten-Informationen
* Farben
* Widgets
* Startseiten-Einstellungen

Für später:
* Zusätzliches CSS
* Menüs

??? 
Teilweise dieselben Einstellungen wie eben

---

# Ein Wordpress? Mein Wordpress! 
## Level 1: Customizer

**Aufgabe:**
* ein Logo hinzufügen (Beispieldatei gibt es hier)
* Linkfarbe ändern
* ein Schlagwörter - und ein Kalender-Widgets hinzufügen

---

# Ein Wordpress? Mein Wordpress! 
## Level 2: Themes
.right[![Coral Dark](https://es-ist-ein-krauss.de/wordpress-schulung/07_coral_dark.png)]
**Aufgabe:**
* Coral Dark-Theme [installieren](http://127.0.0.1/wp-admin/theme-install.php?search=coral%20dark)
* Seite "Customizen" 

---

# Ein Wordpress? Mein Wordpress! 
## Level 3: Plugins

**Aufgabe:**
* Suchen, installieren und testen des Classic Editor-Plugins. Was macht das Plugin?
* Suchen, installieren und aktivieren eines Maintenance-Modus-Plugins.

**Bonusaufgabe:**
* Suchen, installieren und testen eines Plugins, das Bilder beim Upload automatisch komprimiert.

???
Anekdote zum Classic Editor, Hinweis, dass viele Plugins nach wie vor nur mit dem Classic Editor funktionieren
Erklärung, warum Maintenance-Modus

---

# Ein Wordpress? Mein Wordpress! 
## Level 3: Plugins
Essentielle Plugins:
* Backup
* Sicherheit
* Cache
* SEO
* Anti-Spam
* DSGVO

---

# Ein Wordpress? Mein Wordpress! 
## Level 4: Page Builder

---

# Ein Wordpress? Mein Wordpress! 
## Level 5: Child-Themes

---

# DSGVO

* Datenschutzerklärung/Impressum
* SSL
* Kommentare (Datenschutzerklärung, IP anonymisieren)
* externe Ressourcen
* Analytics, Matomo

---

# Wordpress sicher machen
## Level 1

* sichere Passwörter verwenden
* Benutzername ≠ admin (oder root oder Teil der Domain)
* regelmäßige Updates 
* Plugins und Themes nur aus vertrauenswürdigen Quellen installieren
* eingeschränkte Rechte für weitere Nutzer

---

# Wordpress sicher machen
## Level 2

* regelmäßige Backups (z. B. über den Hoster oder mit [UpdraftPlus](https://de.wordpress.org/plugins/updraftplus/))
* 2FA = Zweifaktorauthentifi-zierung (etwa mit [Two Factor](https://de.wordpress.org/plugins/two-factor/))
* Wordpress-Firewall/-Sicherheitsplugin (z. B. [Wordfence](https://de.wordpress.org/plugins/wordfence/), [Sucuri Security](https://de.wordpress.org/plugins/sucuri-scanner/) oder [All In One WP Security & Firewall](https://de.wordpress.org/plugins/all-in-one-wp-security-and-firewall/))

---

# Wordpress sicher machen
## Level 3

* Login-Seite umbenennen (z. B. mit [WPS Hide Login](https://wordpress.org/plugins/wps-hide-login/) – vorher Backup!)
* Geoblocking von Logins (etwa per [IP Geo Block](https://de.wordpress.org/plugins/ip-geo-block/))

---

# Wordpress "sicher" machen
## Bonus

* Antispam mit [AntispamBee](https://de.wordpress.org/plugins/antispam-bee/) 

---

# Ausblick
* SEO
* Theme- und Plugin-Entwicklung (per Boilerplates)
* Wordpress-Kodex

---

# Kontakt:
## Philipp Weißmann

* [mail@philipp-weissmann.de](mail@philipp-weissmann.de)

## Jürgen Krauß

* [oh-mein-gott@es-ist-ein-krauss.de](mailto:oh-mein-gott@es-ist-ein-krauss.de)
