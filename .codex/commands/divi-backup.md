# /divi-backup

Erstelle ein lokales Backup von Datenbank und Dateien.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-backup` durch:

1. `backups/`-Ordner prüfen/anlegen
2. Datenbank-Dump via WP-CLI: `wp db export backups/db-DATUM.sql`
3. Dateien sichern: `tar -czf backups/files-DATUM.tar.gz wp-content/ wp-config.php`
4. Backup mit Datum und Uhrzeit benennen

## Sicherheitsregeln

- Backups NIEMALS nach GitHub pushen
- `backups/` in `.gitignore` eintragen
- Alte Backups nach 30 Tagen löschen (Speicherplatz)

## Ergebnis

Am Ende kurz berichten:
- Welche Dateien erstellt wurden
- Wie groß die Backups sind
- Wo sie liegen
