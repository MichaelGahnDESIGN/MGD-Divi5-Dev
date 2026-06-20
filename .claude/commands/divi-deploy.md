# /divi-deploy

Deployment auf Live-Server — schrittweise, mit Backups und Tests.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-deploy` durch:

1. Lokales Backup erstellen (→ /divi-backup)
2. Live-Server-Backup initiieren (Anleitung geben)
3. Geänderte Dateien identifizieren und übertragen
4. Datenbank migrieren wenn nötig
5. URLs mit `wp search-replace` ersetzen
6. Caches leeren
7. Teste-Checkliste ausgeben

## Sicherheitsregeln

- IMMER Backup VOR dem Deployment
- `wp-config.php` mit Live-Credentials nie nach GitHub pushen
- NIEMALS WordPress Core-Dateien manuell überschreiben — nur `wp-content/`
- SSL nach Deployment prüfen (https://)

## Ergebnis

Am Ende kurz berichten:
- Was deployed wurde
- Welche Tests durchgeführt werden sollten
- Ob URLs korrekt ersetzt wurden
