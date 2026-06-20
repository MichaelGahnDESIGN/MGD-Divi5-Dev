# /divi-optimize

Analysiere und optimiere eine WordPress/Divi-Installation für maximale Performance — Core Web Vitals, Ladezeit, Caching.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-optimize` durch:

1. Ist-Zustand erfassen:
   - Welches Hosting? (Shared, VPS, Managed WP, lokale Dev?)
   - Welches Caching-Plugin ist aktiv? (keines / WP Rocket / LiteSpeed / W3TC / SiteGround)
   - Gibt es ein CDN? (nein / Cloudflare / BunnyCDN)
   - Werden externe Scripts geladen? (Google Analytics, GTM, Facebook Pixel …)
2. Divi Performance-Einstellungen optimieren
3. Bild-Optimierung einrichten
4. Kritisches CSS und Script-Strategie umsetzen
5. Caching konfigurieren (passend zum vorhandenen Plugin)
6. Core Web Vitals Checkliste durchgehen

## Keine externen Dienste ohne Erlaubnis

- Kein Google Fonts CDN (DSGVO!)
- Kein externes Analytics ohne Consent
- Keine CDN-URLs wenn lokale Hosting-Option besteht

## Ergebnis

- Konkrete Einstellungen mit Screenshot-Pfad oder Menüpfad in WordPress
- Vorher/Nachher Schätzung der Auswirkung
- Checkliste der umgesetzten Maßnahmen
