# /divi-install-docker

Starte den MGD Divi 5 Dev Skill für Docker-basierte WordPress + Divi Entwicklungsumgebung.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-install-docker` durch:

1. Voraussetzungen prüfen (Docker Desktop, Docker Compose)
2. Projektordner anlegen (→ /divi-project-filesystem)
3. `docker-compose.yml` erstellen
4. `.env`-Datei für Credentials anlegen
5. Container starten und WordPress konfigurieren
6. Divi installieren, Child-Theme anlegen

## Sicherheitsregeln

- `.env`-Datei immer in `.gitignore` aufnehmen
- Nie echte Produktions-Credentials in `.env` für lokale Entwicklung
- Docker-Volumes für Uploads/Datenbank außerhalb des Git-Repos

## Ergebnis

Am Ende kurz berichten:
- Welche Container laufen
- Unter welcher URL WordPress erreichbar ist
- Welche nächsten Schritte empfohlen werden
