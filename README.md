# codeweek.at

Website der EU Code Week Austria — [codeweek.at](https://codeweek.at)

Gebaut mit Jekyll und gehostet auf GitHub Pages. Bei jedem Push auf `master` wird die Seite automatisch neu gebaut.

---

## Lokale Vorschau mit Apple Container

Voraussetzung: [Apple Container](https://github.com/apple/container) ist installiert.

### 1. Container-System starten

```bash
container system start
```

### 2. Image bauen

```bash
container build --tag codeweek-at .
```

Dieser Schritt installiert Ruby, Jekyll und alle Abhängigkeiten im Container. Dauert beim ersten Mal 2–3 Minuten.

### 3a. Container starten (statisch)

```bash
container run --rm -p 4000:4000 --name codeweek codeweek-at
```

### 3b. Container starten mit Live-Reload (empfohlen für Entwicklung)

Dateien vom Host werden live in den Container gemountet — Jekyll erkennt Änderungen an `.md`-Dateien und CSS automatisch und baut neu. Einfach Datei speichern, Browser-Tab neu laden.

```bash
container run --rm -p 4000:4000 \
  -v /Users/nicogrienauer/Projects/codeweek.at:/site \
  --name codeweek codeweek-at
```

### 4. Im Browser öffnen

```
http://localhost:4000
```

### Container stoppen

`Ctrl+C` im Terminal — oder in einem anderen Tab:

```bash
container stop codeweek
```

### Image neu bauen

Nur nötig wenn sich `Gemfile` ändert (neue Gems). Für Markdown, CSS und Layouts reicht der Live-Reload-Modus.

```bash
container build --tag codeweek-at --no-cache .
```

---

## Inhalt bearbeiten

- **Startseite:** `index.md`
- **Styles:** `assets/css/style.scss`
- **Layout (Nav, Footer):** `_layouts/default.html`

Im Live-Reload-Modus (3b) werden Änderungen automatisch erkannt.

## Deployment

Push auf `master` → GitHub Pages baut und deployed automatisch.
