# /divi-release

Versions-Bump, CHANGELOG aktualisieren, Release-Workflow abschließen.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-release` durch:

1. Aktuelle Version ermitteln
2. Neue Version nach SemVer bestimmen (MAJOR.MINOR.PATCH)
3. Version in `style.css` erhöhen
4. `CHANGELOG.md` mit Datum und Änderungen aktualisieren
5. Git-Commit und Tag erstellen
6. Backup erstellen (→ /divi-backup)
7. Deployment durchführen (→ /divi-deploy)

## Sicherheitsregeln

- Kein Release ohne vorheriges Backup
- Kein Force-Push auf main
- Tag-Name immer `v` + Versionsnummer (z.B. `v1.2.0`)

## Ergebnis

Am Ende kurz berichten:
- Neue Versionsnummer
- Was sich geändert hat
- Ob Deployment erfolgreich war
