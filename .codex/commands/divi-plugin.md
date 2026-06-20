# /divi-plugin

Erstelle ein neues WordPress-Plugin für Divi — sicher strukturiert, mit Hooks, Nonces und korrektem Enqueue.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-plugin` durch:

1. Plugin-Anforderungen abfragen (Zweck, Features, braucht es Admin-Seite?, REST API?, AJAX?)
2. Ordnerstruktur anlegen
3. Haupt-Plugin-Datei mit korrektem Header erstellen
4. Sicherheits-Grundgerüst implementieren (ABSPATH-Check, Nonces, Capabilities)
5. Gewünschte Features implementieren

## Sicherheitsregeln

- `defined('ABSPATH') || exit;` in JEDER PHP-Datei
- Alle User-Inputs sanitieren bevor speichern
- Alle Ausgaben escapen (esc_html, esc_attr, esc_url)
- Nonces auf ALLEN Formularen und AJAX-Requests
- `current_user_can()` vor jeder privilegierten Aktion
- SQL nur via `$wpdb->prepare()` — niemals String-Konkatenation

## Ergebnis

Am Ende kurz berichten:
- Welche Dateien erstellt wurden
- Wie das Plugin aktiviert wird
- Welche Sicherheits-Features implementiert wurden
