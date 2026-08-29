# Verlorene Hundeseelen e.V. – Website

Neue Website, gebaut mit [Eleventy](https://www.11ty.dev/) (statischer Seitengenerator → reines, natives HTML/CSS/JS als Output, kein Framework-Overhead zur Laufzeit). Gedacht für Verwaltung in GitHub und Deployment auf [Vercel](https://vercel.com/).

## Was hier drin ist

```
src/                   Quelldateien (Nunjucks-Templates, CSS, JS, Bilder)
  _includes/            Layout + wiederverwendbare Bausteine (Header, Footer, Logo, Platzhalter)
  _data/site.json        Alle zentralen Fakten (Adresse, IBAN, Formulare, Navigation …)
  index.njk               Startseite
  mitglied-werden/         Mitgliedsantrag
  impressum/                Impressum
  datenschutz/                Datenschutzerklärung
  assets/                      CSS, JS, Bilder, selbst gehostete Fonts
.eleventy.js             Build-Konfiguration
vercel.json               Vercel-Deploy-Einstellungen
```

Build-Ergebnis landet in `_site/` (nicht eingecheckt, wird bei jedem Deploy neu erzeugt).

## Lokal testen

```bash
npm install
npm start        # Dev-Server mit Live-Reload unter http://localhost:8080
npm run build     # Produktions-Build nach _site/
```

Voraussetzung: Node.js 18+ (getestet mit Node 22).

## 1. Bei GitHub einchecken

```bash
cd verlorene-hundeseelen
git init
git add .
git commit -m "Initial commit: Redesign Verlorene Hundeseelen e.V."
```

Dann auf [github.com](https://github.com) ein neues, leeres Repository anlegen (z. B. `verlorene-hundeseelen`) – **ohne** README/License/gitignore anzuhaken, die sind schon da – und:

```bash
git remote add origin https://github.com/DEIN-USERNAME/verlorene-hundeseelen.git
git branch -M main
git push -u origin main
```

## 2. Auf Vercel deployen

1. Auf [vercel.com](https://vercel.com) mit dem GitHub-Account einloggen.
2. „Add New… → Project“ → das eben erstellte Repository auswählen → „Import“.
3. Vercel erkennt die `vercel.json` automatisch (Build-Command `npm run build`, Output-Ordner `_site`). Einfach auf „Deploy“ klicken.
4. Nach ein paar Sekunden ist die Seite unter einer `*.vercel.app`-Adresse live.

### Eigene Domain verbinden

Im Vercel-Projekt unter **Settings → Domains** `verlorene-hundeseelen.de` (und optional `www.verlorene-hundeseelen.de`) hinzufügen. Vercel zeigt dir die nötigen DNS-Einträge (meist ein `A`-Record auf `76.76.21.21` sowie ein `CNAME` für `www`) – die trägst du beim Domain-Registrar/DNS-Provider der Domain ein. Danach jeder Push auf `main` automatisch live.

## 3. Was noch fehlt, bevor die Seite online geht

Diese Punkte sind **bewusst offen gelassen**, weil sie echte Daten/Entscheidungen von dir brauchen:

### Bilder & Logo
Aktuell sind an allen Bildstellen gestrichelte Platzhalter-Boxen mit Beschriftung eingebaut (z. B. „Platzhalter · Herzstück-Foto eines geretteten Hundes“). Sobald du mir die echten Fotos/das Logo schickst, ersetze ich sie 1:1 – oder du legst sie selbst in `src/assets/img/` ab und tauschst in den jeweiligen `.njk`-Dateien den `{{ placeholder(...) }}`-Aufruf gegen ein normales `<img>`-Tag.

Folgende Stellen brauchen Fotos:
- **Hero** (`src/index.njk`): 1 Hochformat-Foto, ca. 4:5, „Herzstück“-Bild
- **So helfen wir**: 1 Querformat-Foto, ca. 4:3
- **Unsere Schützlinge**: 3 Hundefotos, ca. 4:3
- **Erfolgsgeschichten**: je 1 quadratisches Foto für Kiro und Lucky
- **Logo**: aktuell ein selbst gezeichnetes Pfoten-Icon als Platzhalter (`src/_includes/partials/logo-mark.njk`) – bei echtem Logo einfach durch euer Logo-SVG/PNG ersetzen (in Header, Footer und Favicon)

### IBAN
Im Spenden-Bereich steht noch die Platzhalter-IBAN `DE00 0000 0000 0000 0000 00` (das war schon in der alten Seite so leer). Bitte die echte Vereins-IBAN in `src/_data/site.json` (`"iban"`) eintragen.

### E-Mail-Adresse
Ich habe testweise **info@verlorene-hundeseelen.de** für die neue Domain eingesetzt. Bitte prüfen, ob dieses Postfach tatsächlich eingerichtet ist (bzw. eine Weiterleitung auf die bestehende Adresse existiert), bevor die Seite live geht – sonst gehen Anfragen ins Leere.

### Rechtliche Prüfung (wichtig)
- Im **Impressum** und der **Datenschutzerklärung** habe ich Name, Adresse und Kontaktdaten unverändert aus der alten Seite übernommen, den Vereinsnamen aber auf „Verlorene Hundeseelen e.V.“ umgestellt. **Bitte prüfen/bestätigen, dass „Verlorene Hundeseelen e.V.“ auch der offiziell im Vereinsregister eingetragene Name ist** – falls die Umbenennung noch nicht offiziell eingetragen ist, muss im Impressum übergangsweise der eingetragene Name stehen.
- In den alten Dateien gab es zwei unterschiedliche Adressen für die „verantwortliche Stelle“ (Impressum: Gewanne Mittelrhein 3a, Hagenbach – Datenschutz: Kirchstraße 2, Schwegenheim). Ich habe beide auf die Impressum-Adresse vereinheitlicht – bitte kurz bestätigen, welche aktuell korrekt ist.
- Die Datenschutzerklärung habe ich inhaltlich überarbeitet, damit sie zur *neuen* Technik passt (Vercel-Hosting, Zoho-Formulare, PayPal) – die alten Abschnitte zu Borlabs Cookie, Facebook-Connect-Login und WhatsApp Business habe ich entfernt, da diese Dienste auf der neuen Seite nicht eingesetzt werden. Ich bin kein Anwalt – bitte vor Veröffentlichung von einer fachkundigen Stelle (z. B. e-recht24.de-Vorlage oder Anwalt) gegenprüfen lassen, insbesondere auch, ob eine Vereinsregisternummer im Impressum ergänzt werden muss.

### Externe Dienste (bewusst unverändert übernommen)
- **Kontaktformular & Mitgliedsantrag**: weiterhin als eingebettetes Zoho-Formular (gleiche Formular-Links wie vorher)
- **Spenden**: weiterhin per Direktlink zu PayPal
- **Hunde-Vermittlung**: weiterhin verlinkt auf die externe Übersicht unter hundepension-lalupo.de/vermittlung

Falls ihr das mittelfristig durch eigene, native Lösungen ersetzen wollt (z. B. eigenes Formular über eine Vercel-Funktion, eigene Hunde-Datenbank), sag Bescheid – das ist mit dem jetzigen Aufbau problemlos nachrüstbar.

## Inhalte pflegen

- Alle wiederkehrenden Fakten (Adresse, Telefon, Links, Navigation) stehen zentral in `src/_data/site.json` – dort ändern, überall aktualisiert es sich automatisch.
- Neue Unterseite anlegen: neuen Ordner unter `src/` mit `index.njk` anlegen, Front-Matter `layout: base.njk` + `permalink: /pfad/` setzen.
- Texte auf der Startseite direkt in `src/index.njk` anpassen (durchgehend mit Kommentaren `<!-- ... -->` in Abschnitte gegliedert).
- Nach jeder Änderung: `npm start` zeigt die Vorschau live, ein `git push` löst automatisch ein neues Vercel-Deployment aus.
