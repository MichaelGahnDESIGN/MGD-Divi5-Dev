# /divi-childtheme

Erstelle ein neues Divi Child-Theme mit korrekter Struktur, lokalen Fonts und DSGVO-konformem Enqueue.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-childtheme` durch:

1. Ordnerstruktur anlegen (themes/mein-child-theme/)
2. `style.css` mit Theme-Header erstellen
3. `functions.php` mit vollständigem Enqueue-Template erstellen
4. `css/fonts.css` mit @font-face für lokale Fonts erstellen
5. Ordner für lokale Libraries anlegen (js/libs/, css/libs/)
6. Fragen nach: Theme-Name, Primärfarbe, gewünschte Schriften

## Regeln

- Fonts IMMER lokal hosten — niemals Google Fonts CDN direkt
- In Divi → Theme Options → General "Google Fonts" deaktivieren (Hinweis ausgeben)
- Libraries-Dateien müssen manuell heruntergeladen und in js/libs/ abgelegt werden
- Parent-Theme-Style korrekt mit `get_template_directory_uri()` einbinden

## Ergebnis

Am Ende kurz berichten:
- Welche Dateien erstellt wurden
- Welche Libraries-Downloads noch manuell nötig sind
- Hinweis auf Divi Theme Options → Google Fonts deaktivieren
