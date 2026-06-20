# MGD Divi 5 Dev Skill

Ein umfangreicher Skill für Claude Code und ChatGPT Codex, der KI-Agenten dazu befähigt,
professionell mit WordPress und Divi 5 zu entwickeln und zu designen. Animationen,
Scroll-Effekte, Three.js, eigene Plugins, Child-Themes — alles nach MGD-Standard: sauber,
sicher, DSGVO-konform und kommerziell nutzbar.

Dieser Skill ist kein Schnellschuss. Er entstand aus echter Arbeit mit WordPress, Divi und
KI-Agenten im Agentur-Alltag von Michael Gahn DESIGN — und soll genau das widerspiegeln.

## Für Wen Ist Dieser Skill Gedacht?

- Entwickler und Designer, die mit Claude Code oder ChatGPT Codex an WordPress/Divi-Projekten arbeiten
- Agenturen, die ihren Agenten klare Regeln und Qualitätsstandards für WordPress-Arbeit mitgeben wollen
- Menschen, die Divi-Child-Themes, eigene WordPress-Plugins und Animationen professionell umsetzen möchten
- Projekte, bei denen DSGVO-Konformität, lokale Assets und kommerzielle Nutzbarkeit Pflicht sind

## Was Dieser Skill Macht

| Befehl | Was passiert |
|--------|-------------|
| `/divi-install` | WordPress + Divi lokal installieren und konfigurieren |
| `/divi-install-docker` | Docker-Entwicklungsumgebung für WordPress + Divi aufsetzen |
| `/divi-childtheme` | Divi Child-Theme mit korrekter Struktur, lokalen Fonts und Enqueue erstellen |
| `/divi-backup` | Lokales Backup von Datenbank und Dateien erstellen |
| `/divi-dev` | Entwicklungs-Checkliste, Datei-Watcher, Workflow-Übersicht starten |
| `/divi-project-filesystem` | Projektordner mit MGD-AI-Basic-Projektordner anlegen |
| `/divi-plugin` | Neues WordPress-Plugin für Divi erstellen (sicher, strukturiert) |
| `/divi-animations` | Animations-Bibliotheken lokal einbinden und konfigurieren |
| `/divi-deploy` | Deployment auf Live-Server durchführen |
| `/divi-debug` | Systematisches Debugging von Divi-Problemen |
| `/divi-release` | Versions-Bump, CHANGELOG, Release-Workflow |
| `/divi-module` | Natives Divi 5 Custom Module erstellen (React/TSX + PHP Traits) |
| `/divi-optimize` | Performance optimieren — Core Web Vitals, Caching, Bilder |

## Grundregeln — Was Dieser Skill Immer Tut

Diese Regeln sind nicht verhandelbar und gelten für jeden Output:

- **Umlaute korrekt** — ä, ö, ü, ß statt ae/oe/ue/ss
- **Deutsch** — alle Erklärungen, Kommentare und Texte auf Deutsch
- **Lokal** — Fonts, Libraries, Icons, Scripts immer lokal hosten (kein CDN ohne explizite Erlaubnis)
- **DSGVO-konform** — keine Google Fonts direkt, kein externes IP-Logging, kein Tracking ohne Consent
- **Kommerziell nutzbar** — nur MIT-lizenzierte oder anderweitig frei kommerziell nutzbare Libraries
- **Sicherheit** — Nonces, Capability-Checks, Sanitization und Escaping bei jedem Plugin
- **Neues Projekt → Projektordner** — Hinweis auf MGD-AI-Basic-Projektordner
- **Fragen bei Unklarheit** — sofort fragen, bevor Code produziert wird

## Erlaubte Libraries (Lizenz-Übersicht)

| Library | Lizenz | Version | Zweck |
|---------|--------|---------|-------|
| Three.js | MIT | r175 | 3D-Grafik |
| GSAP + ScrollTrigger | No-Charge (Webflow) | 3.12.5+ | Hochwertige Animationen |
| AOS | MIT | 2.3.4 | Scroll-Entrance-Animationen |
| Lenis | MIT | 1.3.23 | Smooth Scroll |
| Vanilla Tilt.js | MIT | 1.8.1 | 3D-Tilt-Effekte |
| Alpine.js | MIT | 3.15.12 | UI-Interaktivität |
| Swiper.js | MIT | 12.2.0 | Slider/Karussell |
| Bunny Fonts | Gratis, DSGVO-OK | — | EU-sicherer Font-CDN |

GSAP ist seit 30. April 2025 vollständig kostenlos, auch kommerziell — inkl. ScrollTrigger,
SplitText und allen ehemaligen Club-Plugins. Nutzbar für alle normalen Websites und
Client-Projekte ohne Einschränkungen.

## Schnellstart

```bash
# Claude Code
git clone https://github.com/MichaelGahnDESIGN/MGD-Divi5-Dev ~/.claude/skills/MGD-Divi5-Dev
```

```bash
# ChatGPT Codex
git clone https://github.com/MichaelGahnDESIGN/MGD-Divi5-Dev ~/.codex/skills/MGD-Divi5-Dev
```

Dann im Projekt-Kontext:

```text
/divi-childtheme
Erstelle mir ein Divi Child-Theme für ein lokales Projekt.
Theme-Name: "Mein Shop Child"
Primärfarbe: #ce1517
Schrift: Open Sans (lokal)
```

```text
/divi-plugin
Erstelle ein WordPress-Plugin das nach dem Absenden eines Kontaktformulars
eine E-Mail sendet und den Eintrag in einer Custom-Tabelle speichert.
```

```text
/divi-animations
Binde GSAP mit ScrollTrigger lokal ein und erstelle Scroll-Animationen
für alle Divi-Sektionen auf der Startseite.
```

## Repository-Struktur

```text
MGD-Divi5-Dev/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── .gitignore
├── .github/
│   └── ISSUE_TEMPLATE/
│       └── bug_report.md
├── .claude/
│   └── commands/             ← Claude Code Slash-Commands
│       ├── divi-install.md
│       ├── divi-install-docker.md
│       ├── divi-childtheme.md
│       ├── divi-backup.md
│       ├── divi-dev.md
│       ├── divi-project-filesystem.md
│       ├── divi-plugin.md
│       ├── divi-animations.md
│       ├── divi-deploy.md
│       ├── divi-debug.md
│       └── divi-release.md
├── .codex/
│   └── commands/             ← ChatGPT Codex Commands (gleiche Dateien)
└── skill/
    └── DIVI5-SKILL.md        ← Vollständige Skill-Dokumentation
```

## Was Der Skill Enthält

### WordPress Plugin-Entwicklung
Vollständige Plugin-Struktur mit korrektem Header, Lifecycle-Hooks, Sicherheits-Template
(Nonces, Capability-Checks, Sanitization, Escaping), AJAX-Handler, REST-API-Endpunkte,
Datenbank-Interaktionen via `$wpdb`, Custom Post Types und Taxonomien, Settings API.

### Divi Child-Themes
Komplette Child-Theme-Struktur mit lokalem Font-Hosting (@font-face, kein Google Fonts CDN),
korrektem Enqueue via `functions.php`, SCSS-Vorbereitung, Divi-Builder-Kompatibilität.

### Animations-Stack
Vollständige lokale Integration von Three.js, GSAP + ScrollTrigger, AOS, Lenis,
Vanilla Tilt, Alpine.js und Swiper — alle mit Divi-spezifischen Quirks und Fixes:
- `window.load` statt `DOMContentLoaded` wegen Divi Lazy-Loading
- `wp-admin`-Check um Builder-Konflikte zu vermeiden
- `jQuery`-noConflict-Pattern
- `ScrollTrigger.refresh()` nach AJAX-Content
- Lenis + Divi Anchor-Scroll Konflikt-Fix
- Alpine.js + `wp_kses_post()` Workaround

### DSGVO / EU-Datenschutz
Vollständige Checkliste: Google Fonts deaktivieren, lokale Fonts, Consent-Management,
SSL, keine externen Tracker ohne Zustimmung.

### Docker-Entwicklungsumgebung
`docker-compose.yml` für lokale WordPress + Divi Entwicklung mit PHP 8.3,
`.env`-Template, WordPress-Debug-Einstellungen.

### Deployment-Workflow
Schrittweises Deployment mit Backup, `wp search-replace`, Cache-Clearing und Tests.

## Verwandte Projekte Von Michael Gahn DESIGN

- [MGD-AI-Basic-Projektordner](https://github.com/MichaelGahnDESIGN/MGD-AI-Basic-Projektordner)
  Projektordner-Vorlage für neue KI-Projekte — als Basis für jedes neue WordPress-Projekt nutzen.

- [MGD-DEV-Skill](https://github.com/MichaelGahnDESIGN/MGD-DEV-Skill)
  Projektneutraler Skill für Release, Sync, Backup, Cleanup und Tests — passt direkt zu /divi-release.

- [MGD-AI-PlayTest-Skill](https://github.com/MichaelGahnDESIGN/MGD-AI-PlayTest-Skill)
  Funktionstest aus Nutzer-Perspektive — nach jedem Divi-Deployment sinnvoll.

- [MGD-ProjectClean-Skill](https://github.com/MichaelGahnDESIGN/MGD-ProjectClean-Skill)
  Aufräumen nach Projekt-Abschluss — Backups, Versionierung, sauber übergeben.

- [MGD-Bugreport-Skill](https://github.com/MichaelGahnDESIGN/MGD-Bugreport-Skill)
  Professionelle Bug-Reports erstellen wenn etwas in Divi schief läuft.

- [MGD-AI-Project-Updater-Skill](https://github.com/MichaelGahnDESIGN/MGD-AI-Project-Updater-Skill)
  Sichere Update-Workflows für WordPress, Plugins und Themes.

- [MGD-ToDo-SKILL](https://github.com/MichaelGahnDESIGN/MGD-ToDo-SKILL)
  Aufgabenverwaltung direkt im Projekt-Repo — für längere Divi-Projekte.

## Lizenz

MIT — frei verwendbar, anpassbar, weitergeben mit Namensnennung.

## Impressum

Angaben gemäß § 5 DDG (Digitale-Dienste-Gesetz)

Michael Gahn DESIGN<br>
Michael Gahn<br>
Dr.-Theodor-Brugsch Str. 12<br>
08529 Plauen, Sachsen, Deutschland<br>
Tel.: +49 (0) 176 557 647 48<br>
E-Mail: Anfrage@Michael-Gahn.de<br>
Steuernummer: 223/222/02451 | USt-ID: DE288143343

## 🔒 Lokal-only — Playtests, Backups & sensible Daten

Diese Daten dürfen **niemals** die lokale Maschine verlassen — weder nach GitHub noch nach Live/Deploy:

- **Backups:** DB-Dumps, `*.sql`, `*.sql.gz`, `backups/` bleiben lokal — nie nach GitHub, nie in den Webroot/Live.
- **Sensible Daten:** `.env*` (außer `.env.example`), Tokens, API-Keys, Passwörter, `wp-config.php` — niemals committen/pushen.
- **Push-Disziplin:** Nur den Hauptbranch (`main`) pushen, **niemals** `git push --all`/`--mirror`.
