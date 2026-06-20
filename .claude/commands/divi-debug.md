# /divi-debug

Systematisches Debugging von Divi-Problemen.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-debug` durch:

1. Problem-Beschreibung erfragen
2. Debug-Checkliste durchgehen
3. Wahrscheinliche Ursache eingrenzen
4. Lösungsschritte vorschlagen

## Debug-Reihenfolge

1. Browser-Console auf JS-Fehler prüfen
2. PHP-Fehler in `wp-content/debug.log` prüfen
3. Plugin-Konflikt durch schrittweises Deaktivieren eingrenzen
4. Theme-Konflikt mit Standard-Theme prüfen
5. Divi-Cache leeren (Divi → Theme Options → Builder)
6. WordPress-Cache leeren

## Ergebnis

Am Ende kurz berichten:
- Identifizierte Ursache
- Durchgeführte Schritte
- Lösung oder nächste Diagnoseschritte
