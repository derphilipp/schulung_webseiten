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

# Wordpress

---

# Wordpress ist:

* ein Content-Management-System (CMS) mit Fokus auf das Bloggen
* entwickelt von der Wordpress Foundation
* 2003 erstmals erschienen
* open source ("GPL-2.0+"-Lizent)
* erhältlich in 62 Sprachen

???
* auch aus dem Jahr 2003 (Dezember): Begriff "Web 2.0" 
* User wird zum Prosumenten im "Mitmachweb"
* "Goldenen Jahre" der privaten Webseiten und Blogs – weil einfacher und dynamisch

---

# Wordpress ist:
.center[![Schweizer Taschenmesser](https://media.giphy.com/media/xT5LMxAxpGSb5AZt8A/giphy.gif)]

???
und dann kam Wordpress und entwickelte sich schnell zur eierlegenden Blogmilchsau

---

# .center[32,8 Prozent] 
## .center[.red.bold[aller] Webseiten basieren auf Wordpress]

.footnote[*Quelle: W3Techs (abgerufen am 11.1.2019), https://w3techs.com/technologies/overview/content_management/all*] 

???
* Verbreitung spricht für WordPress ...     **(Resourcen, Hilfestellungen)**
* ... spricht aber auch irgendwie dagegen.   **(Sicherheit)**

* Andere beliebte CMS sind Joomla (2. Platz mit 6 Prozent), Drupal, Shopify, Magento, Typo 3 ...
* Knapp 60 Prozent der Webseiten, _die ein CMS nutzen_, verwenden Wordpress.

---

# Wofür sich Wordpress eignet:

* Blogs
* private Webseiten mit regelmäßigen Updates
* kleine Shops
* Webprojekte mit mehreren Beteiligten in kleinem und mittlerem Umfang

---

# Wofür sich Wordpress nicht (so gut) eignet:

* große mehrsprachige Unternehmensseiten
* komplexe Shop-Systeme mit ERP-Anbindung
* statische Webprojekte
* Seiten mit besonderen spezifischen Anforderungen
* Arbeiten mit vielen Medien/Dokumenten
* Foren mit vielen Benutzern

???
Gibt's alles auch mit Wordpress! Ist aber halt in vielen Fällen nur ein Kompromiss.

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

???
* (und 5.: Sonderseiten)

---

# Grundlagen
## Aufbau
### 1. Wordpress
.center[![Dateien und Verzeichnisse](https://es-ist-ein-krauss.de/wordpress-schulung/01_files_and_folders.png)]


---

# Grundlagen
## Aufbau
### 1. Wordpress
Neben den Core-Dateien, ist vor allem ein Verzeichnis für uns interessant:

wp-content:
* plugins
* themes
* uploads

???
* Was das alles ist, schauen wir uns später an.
* Wichtig nur: außer config.php passiert alles hier!

---

# Grundlagen
## Aufbau
### 1. Wordpress
.center[![Datenbank](https://es-ist-ein-krauss.de/wordpress-schulung/02_database.png)]

???
* Prefix
* Tabellen für:
  * Kommentare
  * Optionen
  * Posts
  * usw.

---

# Grundlagen
## Aufbau
### 1. Wordpress
Die Datenbank enthält:
* Einstellungen
* Inhalte
* Beitragstexte
* Nutzer
* Meta-Informationen

???
* Medien landen im Dateiverzeichnis

---

# Grundlagen
## Aufbau
### 2. Inhalte

|`SEITEN`            | `BEITRÄGE`          |
|-----------------------|-----------------------|
|feststehende Inhalte |regelmäßige Informationen | 
|Evergreens mit oder ohne regelmäßigem Aktualisierungsbedarf\*    |Content mit begrenzter Halbwertszeit\* |
|Beispiel: _Impressum_    |Beispiel: _Die 5 besten Death-Metal-Bands aus Franken_ |

???
* \*mit Ausnahmen 
  * Seiten: ohne Datumsangabe, stets aktuell
  * Beiträge: mit Erstellungsdatum (=implizite Halbwertszeit), aber bei Bedarf Aktualisierungen

---

# Grundlagen
## Aufbau
### 3. Design
sogenannte Themes bestimmen:
* Look and Feel
* Farben, Schriften und Hintergründe
* Anordnung der Elemente
* zum Teil auch: Funktionalitäten

???
* Stichwort "Model-View-Controller" – ist Wordpress per Definition nicht, aber so kann man es sich vorstellen: Inhalt und Design sind getrennt voneinander
* für richtiges MVC: Plugins wie Churro – da bin ich dann aber raus

---

# Grundlagen
## Aufbau
### 4. Funktionalitäten
aktuell\* erweitern mehr als .red.bold[54.200 Plugins] den Wordpress-Funktionsumfang – und verwandeln es in:
* Forum
* soziales Netzwerk
* Online-Shop
* Wiki
* Crowdfunding-Plattform
* Buchungssystem 
* Online-Galerie
* …

.footnote[\* *Quelle: Wordpress.org (abgerufen am 11.1.2019), https://wordpress.org/plugins/*]

---

# Grundlagen
## Aufbau
### 4. Funktionalitäten
.center[![Vielseitigkeit](https://i.giphy.com/media/1hBWtlec4aAb37ggn8/giphy.webp)]

---

# Grundlagen
## Aufbau
### 5. Sonderseiten

Wordpress bringt vieles Weitere von Haus auf mit:
* Kategorieübersicht
* 404-Fehler
* Suchergebnisseiten
* ...

???
* Gab kein 5. auf der Übersicht, ist auch eher so "meta".
* Das schauen wir uns gleich live an.

---

# Grundlagen
## Hosting
--

### Voraussetzungen
* dynamischer Webspace
  * Apache oder Nginx
  * PHP (> 7.3)

* Datenbank
  * MySQL (> 5.6)
  * oder: MariaDB (> 10.0)

---

# Grundlagen
## Hosting
### Varianten

|`spezialisierter Bloghoster`   |`allgemeiner Hoster`       |`eigener Server`       |
|----------------------------|-------------------------------|---------------------------|
|**Vorteil:** Zuverlässigkeit, Support, Staging-Option |**Vorteil:** Kompromiss aus Kontrolle und Zuverlässigkeit |**Vorteil:** maximale Flexibilität |
|**Nachteil:** reines Wordpress-Hosting, manchmal eingeschränkter Theme, Plugin und Dateizugriff |**Nachteil:** viel Kontrolle, aber nicht über alles |**Nachteil:** hoher Administrationsaufwand |

???

* spezialisierte Bloghoster (Raidboxes, wordpress.com, etc.)
* allgemeine Hoster (1 & 1, all-inkl, Strato, etc.) – oft mit 1-Klick-Installation

* eigener Server (zu Hause oder im Rechenzentrum) – evtl. mit File- und Datenbankinstallation  

* Zeit für die Installation!

---

# kurze Pause?

---

# Erste Schritte
## Installation
### lokale Test- und Entwicklungsumgebung
Installation "zu Hause":
* Xampp, Mampp, Lampp
* Docker [docker-compose.yaml](http://ktshannon.com/how-to-setup-wordpress-locally-with-docker-phpmyadmin-included/)

???
* Docker
* Wir verwenden hier die Variante "xampp"; bereits vorinstalliert

---

# Erste Schritte
## Installation
### lokale Test- und Entwicklungsumgebung 

* Starten von "Xampp Control Panel"
    * Starten von "Apache"
    * Starten von "MySQL"

.center[![xampp](https://es-ist-ein-krauss.de/wordpress-schulung/10_xampp.png)]

???
* praktisch: Wir sehen gleich auch die Ports

---

# Erste Schritte
## Installation
### Schritt 1: Download Wordpress
Vorsicht: 
* [de.wordpress.com](https://de.wordpress.com) => kommerzieller Hosting-Service
* [de.wordpress.org](https://de.wordpress.org) => Wordpress-Download (open source)

.footnote[mehr dazu hier: [https://de.wordpress.com/com-vs-org/](https://de.wordpress.com/com-vs-org/)] 

---

# Erste Schritte
## Installation
### Schritt 1: Download Wordpress
Download unter:
* [https://de.wordpress.org/latest-de_DE.zip](https://de.wordpress.org/latest-de_DE.zip)

Entpacken nach:\*
* C:\xampp\htdocs 

.footnote[\* Wordpress im Verzeichnis /wordpress –– alternativ: Installation ins Root-Verzeichnis "/"]

???
Ich hoffe, das ist auch unter C: installiert ...

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
.center[![Neue Datenbank](https://es-ist-ein-krauss.de/wordpress-schulung/04_new_database2.png)]

???
Menüpunkt (rechts) heißt "Benutzerkonten"

---

# Erste Schritte
## Installation
### Schritt 3: Grundkonfiguration
Wordpress-Installer: [http://127.0.0.1/wordpress](http://127.0.0.1/wordpress)

---

# Erste Schritte
## Wordpress-Frontend und -Backend

**Frontend** <= was Besucher sehen
* [http://127.0.0.1/wordpress](http://127.0.0.1/wordpress)

**Backend** <= Arbeit und Contentpflege „hinter den Kulissen“
* [http://127.0.0.1/wordpress/wp-admin](http://127.0.0.1/wordpress/wp-admin)

???
* kurze Erinnerung

Frontend anschauen: Hier sehen wir erstmal nicht viel. Es gibt:
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

In ähnlicher Form kann es auch weitere Inhaltstypen geben, die sogenannten `Custom Post Types` – etwa für:
* Portfolio
* Referenzen
* Kundenstimmen
* Podcast-Episoden
* ...

.footnote[Mehr dazu [hier](https://www.drweb.de/wordpress-intern-einstieg-custom-post-types-50402/).]

???
Custom Post Types von Haus auf z. B. für:
* Medien

Custom Post Types unterscheiden sich in:
* den Feldern, die hier auszufüllen sind
* im Design
* je nach Theme auch in der Darstellung

---

# Erste Schritte
## Aufgabe:
* Anlegen und veröffentlichen **mindestens einer Seite**

* Anlegen und veröffentlichen von **mindestens zwei Beiträgen**, inklusive:
  * Beitragsbild
  * Kategorie
  * Schlagwörter

.footnote[Ideenlos beim Text? => [Franconian Ipsum](https://www.frankenipsum.de/index.php)]
  
???
Danach Check im Frontend: Wie sehen Seiten aus, wie Beiträge, was sind Kategorien, wie sehen Schlagwort-Archive aus, etc.
Unterschiede?

---

# Ein Wordpress? Mein Wordpress! 
## Level 0: Einstellungen  

???
* Jetzt wo Inhalte drin sind => Seite individualisieren

--

**Aufgabe:**
* Erkunden der Einstellungen
* Was würden Sie spontan ändern? Warum?

???
Permalinks, Umstellung auf SSL, Diskussion (besonders im Hinblick auf die DSGVO interessant), Datenschutz

---

# Ein Wordpress? Mein Wordpress! 
## Level 1: Customizer
.center[![Customizer](https://es-ist-ein-krauss.de/wordpress-schulung/06_customizer.png)]]

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
* ein Logo hinzufügen ([Beispieldatei](https://es-ist-ein-krauss.de/wordpress-schulung/09_logo.png))
* Linkfarbe ändern
* ein Schlagwörter- und ein Kalender-Widget hinzufügen

???
* Möglichkeiten sind begrenzt => deshalb schauen wir mal, was ein Theme macht
* darüber haben wir ja schon geredet

---

# Ein Wordpress? Mein Wordpress! 
## Level 2: Themes
.left[![Coral Dark](https://es-ist-ein-krauss.de/wordpress-schulung/07_coral_dark2.png)]

???
* Layoutbeispiele: Hell/dunkel, einspaltig/mehrspaltig, große Bilder/keine Bilder, "magazin-ig"/"shop-ig", ...

---

# Ein Wordpress? Mein Wordpress! 
## Level 2: Themes
**Aufgabe:**
* "Coral Dark"-Theme [installieren](http://127.0.0.1/wordpress/wp-admin/theme-install.php?search=coral%20dark)
* Seite individualisieren 

---

# Ein Wordpress? Mein Wordpress! 
## Level 3: Widgets und Menüs

* **Hinweis:** Darstellung und Positionen hängen vom Theme ab

* **Aufgabe:**
  * Hauptmenü anlegen mit Links auf:
    * Impressum
    * Datenschutzerklärung
    * Kategorie "Allgemein"

---

# Ein Wordpress? Mein Wordpress! 
## Level 4: Plugins

**Aufgabe:**
* Suchen, installieren und testen des "Classic Editor"-Plugins. Was macht es?
* Suchen, installieren und aktivieren eines "Maintenance Mode"-Plugins.

**Fortgeschrittenen-Aufgabe:**
* Suchen, installieren und testen eines Plugins, das Bilder beim Upload automatisch komprimiert.

???
* Anekdote zum Classic Editor, Hinweis, dass viele Plugins nach wie vor nur mit dem Classic Editor funktionieren
* Erklärung, warum Maintenance-Modus
* Smush für Bilder – weil beliebter Fehler: Bilder zu groß, Seite zu langsam

---

# Ein Wordpress? Mein Wordpress! 
## Level 4: Plugins
Essentielle Plugins:
* Backup
* Sicherheit
* Cache
* SEO
* Anti-Spam
* DSGVO
* ...

---

# Ein Wordpress? Mein Wordpress! 
## Level 5: Page Builder
**Page Builder**-Plugins sind oft an Themes gekoppelt und liefern vorgefertigten Content-Elemente für Drag'n'Drop-Seitengestaltung:

.center[![Elementor](https://es-ist-ein-krauss.de/wordpress-schulung/08_elementor.png)]

---

# Ein Wordpress? Mein Wordpress! 
## Level 5: Page Builder

**Aufgabe:**
* "Elementor"-Plugin installieren
* Seite oder Beitrag mit "Icon-Box", "Bild-Karussell" und "Video" aufbauen

**Fortgeschrittenen-Aufgabe:**
* Beitrag mit mehrspaltigem Layout anlegen

---

# Ein Wordpress? Mein Wordpress! 
## Level 6: Child-Themes

Mit Child-Themes:
* Themes individualisieren
* kompatibel zu zukünftigen Updates
* eigener PHP-Code
* eigenes CSS
* quasi ein "eigenes Plugin-Theme-Kombinat auf Speed"

???
Nur der Vollständigkeit halber => würde den Rahmen sprengen

---

# Kurze Pause?

???
Kurze Pause? [Pause!](https://www.es-ist-ein-krauss.de/wordpress-schulung/hack.zip)

---

# Wordpress sicher machen
## Was tun im Hackingfall?

* Unterstützung durch den Hoster?
* Wurde ein Backup gemacht?
* Kann ich mich noch anmelden?
* Wurden Seiten, Beiträge oder Links manipuliert?
* Gibt es auffällige Plugins, Dateien, Benutzer?
* Plugins zur [Malware](https://kb.sucuri.net/plugins/malware-scanner)- und [Template](https://wordpress.org/plugins/tac/)-Überprüfung

---

# Wordpress sicher machen
## Level 1

* sichere Passwörter verwenden
* Benutzername ≠ admin (auch verboten: root bzw. Teil der Domain)
* regelmäßige Updates 
* Plugins und Themes nur aus vertrauenswürdigen Quellen installieren
* eingeschränkte Rechte für weitere Nutzer
* SSL-Verschlüsselung


---

# Wordpress sicher machen
## Level 2

* regelmäßige Backups (z. B. über den Hoster oder mit [UpdraftPlus](https://de.wordpress.org/plugins/updraftplus/))
* 2FA = Zweifaktorauthentifizierung (etwa mit [Two Factor](https://de.wordpress.org/plugins/two-factor/))
* Wordpress-Firewall/-Sicherheitsplugin (z. B. [Wordfence](https://de.wordpress.org/plugins/wordfence/), [Sucuri Security](https://de.wordpress.org/plugins/sucuri-scanner/) oder [All In One WP Security & Firewall](https://de.wordpress.org/plugins/all-in-one-wp-security-and-firewall/))

---

# Wordpress sicher machen
## Level 3

* Login-Seite umbenennen (z. B. mit [WPS Hide Login](https://wordpress.org/plugins/wps-hide-login/) – vorher Backup!)
* Geoblocking von Logins (etwa per [IP Geo Block](https://de.wordpress.org/plugins/ip-geo-block/))

.footnote[Ansonsten: [das hier lesen](https://www.wpbeginner.com/wordpress-security/)]

---

# Wordpress "sicher" machen
## Bonus

* Antispam mit [AntispamBee](https://de.wordpress.org/plugins/antispam-bee/) 

---

# Wordpress & DSGVO

* Datenschutzerklärung und Impressum (Generatoren z. B. bei [RA Schwenke](https://datenschutz-generator.de/) oder bei [eRecht 24](https://www.e-recht24.de/impressum-generator.html))
* SSL
* Kommentare (Datenschutzerklärung, IP anonymisieren)
* externe Ressourcen
* "Cookie Notice"
* Analytics, Matomo

???
* Tipp: Generator anschauen und Liste machen, was dort abgefragt wird, dann checken: Videos, Fonts, Maps, Analytics, etc.
* SSL: Zertifikat, Let's Encrypt, Webseite umstellen Wordpress

---

# Weitere Optimierungen
* SEO-Plugins: 
    * [Yoast](https://de.wordpress.org/plugins/wordpress-seo/) 
    * oder [All-in-one SEO](https://de.wordpress.org/plugins/all-in-one-seo-pack/)
    * [XML-Sitemap](https://de.wordpress.org/plugins/xml-sitemap-feed/)
* eigene Entwicklung:
    * [Wordpress-Kodex](https://codex.wordpress.org/)
    * [Theme-Boilerplate](http://html5blank.com/)
    * [Plugin-Boilerplate](https://wppb.me/)

---

# Kontakt:
## Philipp Weißmann

* [mail@philipp-weissmann.de](mail@philipp-weissmann.de)

## Jürgen Krauß

* [oh-mein-gott@es-ist-ein-krauss.de](mailto:oh-mein-gott@es-ist-ein-krauss.de)
