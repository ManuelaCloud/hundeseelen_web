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
Die von dir geschickten Hundefotos sind bereits eingebaut (komprimiert & responsive) unter `src/assets/img/`:
- **Hero**: `hero-welpe.jpg`
- **So helfen wir**: `gruppe-wald.jpg`
- **Unsere Schützlinge** (3 Fotos): `schnueffeln-gehege.jpg`, `welpe-und-hund-baumstamm.jpg`, `zwei-laufhunde.jpg`
- **Erfolgsgeschichten**: `story-kiro.jpg` (Kiro) und `story-lucky.jpg` (Lucky – aktuelles Foto)
- **Mitglied werden**: `mitglied-portrait.jpg`

Vier weitere von dir geschickte Fotos (zwei Nahaufnahmen einer Hand, die einen Hund streichelt, sowie zwei Alternativ-Crops) liegen unverbaut unter `src/assets/img/spares/` – falls ihr sie später z. B. für Social Media, einen Blog-Beitrag oder eine weitere Unterseite nutzen wollt. Ein Bild austauschen: einfach die entsprechende `.jpg`-Datei unter demselben Namen ersetzen, oder den `src`-Pfad im jeweiligen `.njk`-Template ändern.

**Logo**: Das offizielle Rundlogo („Tierschutzverein Verlorene Hundeseelen Südpfalz e.V.“) ist jetzt eingebaut – in Header, Footer und als Favicon (Browser-Tab-Icon, inkl. Homescreen-Icon fürs Handy). Datei: `src/assets/img/logo-badge.png` (512×512, transparenter Rand, funktioniert auf hellem wie dunklem Hintergrund). Die Favicon-Variante ohne Schriftzug liegt als `favicon-32.png` / `favicon-192.png` / `favicon-512.png` / `apple-touch-icon.png` daneben (bei Bedarf zentral in `src/_includes/partials/logo-mark.njk` bzw. `src/_includes/base.njk` austauschbar).

### IBAN
Die echte Vereins-IBAN ist eingetragen (`src/_data/site.json` → `"iban"`).

### E-Mail-Adresse
Ich habe testweise **info@verlorene-hundeseelen.de** für die neue Domain eingesetzt. Bitte prüfen, ob dieses Postfach tatsächlich eingerichtet ist (bzw. eine Weiterleitung auf die bestehende Adresse existiert), bevor die Seite live geht – sonst gehen Anfragen ins Leere.

### Rechtliche Prüfung (wichtig)
- **Vereinsname**: Im Impressum, in den Meta-Tags (Seitenbeschreibung für Google & Social-Media-Vorschau) und im Footer-Copyright steht jetzt der vollständige Name **„Tierschutzverein Verlorene Hundeseelen Südpfalz e.V.“** (laut Logo/deiner Bestätigung). Im Fließtext und der Navigation bleibt weiterhin die Kurzform „Verlorene Hundeseelen“ als Marke. Zentral gepflegt in `src/_data/site.json` → `"legalName"`.
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
