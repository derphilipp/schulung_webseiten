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
6. Nach 24 Stunden funktioniert auch HTTPS Transport

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

# Content here

---

# Kontakt:
## Philipp Weißmann

* [mail@philipp-weissmann.de](mail@philipp-weissmann.de)

## Jürgen Krauß

* [oh-mein-gott@es-ist-ein-krauss.de](mailto:oh-mein-gott@es-ist-ein-krauss.de)