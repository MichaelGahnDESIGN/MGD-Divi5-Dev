# /divi-module

Erstelle ein natives Divi 5 Custom Module — mit React/TSX Frontend, PHP Traits Backend und `module.json` Deklaration.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-module` durch:

1. Modul-Anforderungen abfragen:
   - Wie heißt das Modul? (Technischer Slug + Anzeigename)
   - Welche Inhaltsfelder? (Text, Bild, URL, Toggle, Select …)
   - Welche Design-Optionen? (Farbe, Schrift, Abstand, Schatten …)
   - Statisches oder dynamisches Modul (REST API)?
   - Hat es Child-Module (z.B. Akkordeon mit Items)?
2. Plugin-Grundstruktur anlegen
3. `module.json` schreiben (Attribute, Breakpoints, States)
4. PHP-Klasse mit Traits erstellen (Render, Styles, Classnames, ScriptData)
5. TSX-Komponenten schreiben (edit.tsx, settings-content.tsx, settings-design.tsx)
6. Assets registrieren und einbinden
7. Divi 4 Kompatibilitäts-Check (falls Fallback nötig)

## Pflichtregeln

- `defined('ABSPATH') || exit;` in jeder PHP-Datei
- Webpack-Externals für alle `@divi/*` Pakete
- Builder via `et-fb` / `?et_fb=1` ausschließen wenn Frontend-Scripts geladen werden
- Alle Styles via PHP Traits ausgeben — kein direktes CSS-Inline

## Ergebnis

Vollständige Plugin-Dateistruktur, fertig zum Aktivieren und im Divi Builder nutzen.
Klarer Hinweis welche npm-Befehle zum Bauen nötig sind.
