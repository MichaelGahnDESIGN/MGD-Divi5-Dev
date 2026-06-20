# /divi-install

Starte den MGD Divi 5 Dev Skill für lokale WordPress + Divi Installation.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-install` durch:

1. PHP-Version prüfen (8.3+ empfohlen)
2. WP-CLI prüfen oder Installationsanleitung geben
3. WordPress herunterladen und konfigurieren
4. Divi-Theme installieren
5. Child-Theme anlegen (→ /divi-childtheme)
6. Debug-Modus für lokale Entwicklung aktivieren

## Sicherheitsregeln

- `wp-config.php` niemals in Git committen
- `.env`-Dateien niemals nach GitHub pushen
- Debug-Modus (`WP_DEBUG true`) nur lokal — auf Live immer `false`

## Ergebnis

Am Ende kurz berichten:
- Was installiert/konfiguriert wurde
- Welche nächsten Schritte empfohlen werden (/divi-childtheme, /divi-dev)
