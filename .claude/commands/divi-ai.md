# /divi-ai

Divi AI sinnvoll einsetzen — kombiniert mit Claude Code für maximale Qualität. DSGVO-Aspekte beachten.

## Wichtig vorab — DSGVO

**Divi AI sendet Daten an Elegant Themes Server** (USA). Das bedeutet:

- Seiteninhalt, den du in Divi AI eingibst, verlässt die EU
- Für DSGVO-konforme Projekte gilt: **Keine Kundendaten in Divi AI eingeben**
- Im Cookie-Consent-Banner muss Divi AI als Drittdienst nicht separat ausgewiesen werden (da serverseitig), aber Elegent Themes Nutzungsbedingungen + Datenschutzerklärung sollten im Impressum/Datenschutz erwähnt werden wenn Divi AI aktiv genutzt wird

---

## Was Divi AI kann

| Funktion | Gut für | Besser mit Claude Code |
|----------|---------|----------------------|
| Layout generieren | Schneller Entwurf | Nein — das ist Divi AIs Stärke |
| Sektionen erstellen | Erste Ideen | Nein — perfekt für Einstieg |
| Texte schreiben | Platzhalter, Rohtext | Ja — Claude Code für finalen Content |
| Bilder generieren | Mockup-Bilder | Ja — Firefly/Midjourney für Produktion |
| Custom CSS | Einfache Stile | Ja — Claude Code für komplexe Logik |
| Plugins entwickeln | Nein | Ja — immer Claude Code |
| Sicherheit | Nein | Ja — immer Claude Code |
| DSGVO-Code | Nein | Ja — immer Claude Code |

---

## Empfohlener Workflow

### Phase 1 — Entwurf mit Divi AI

```
Divi Visual Builder → Sektion hinzufügen → Mit KI erstellen
→ Beschreibung eingeben:
  "Hero-Sektion für ein Rechtsanwaltsbüro. Dunkler Hintergrund,
   Headline groß, kurzer Untertitel, zwei Buttons (Kontakt + Leistungen),
   professionell und seriös."
→ Variante wählen und anpassen
```

### Phase 2 — Feinarbeit mit Claude Code

Sobald das Layout steht, übernimmt Claude Code:

```
/divi-childtheme   — Child-Theme strukturieren
/divi-design-system — Farben, Typo, Spacing systematisieren
/divi-animations   — Animationen sauber einbinden
/divi-optimize     — Performance prüfen
```

### Phase 3 — Content mit Claude Code (nicht Divi AI)

Für finale Texte, Datenschutzerklärung, Impressum, Meta-Tags:

```
Erstelle mir die Datenschutzerklärung für folgende Dienste:
- WordPress (lokal gehostet)
- WooCommerce (keine externen Payment-Provider)
- Kontaktformular (kein Drittanbieter, E-Mail direkt über Server)
Rechtsform: Einzelunternehmer, Sitz: Deutschland
```

---

## Divi AI konfigurieren

### Aktivierung (Divi Dashboard)

```
WordPress Admin → Divi → Divi AI
→ API-Verbindung prüfen (Elegant Themes Konto erforderlich)
→ Sprache: Deutsch setzen
→ Kontext definieren: Firmenname, Branche, Tonalität
```

### Kontext richtig setzen

```
Divi AI → Einstellungen → Website-Kontext:

Firmenname: [Kunde]
Branche: [Branche]
Zielgruppe: [Beschreibung]
Tonalität: Professionell, vertrauenswürdig, klar
Primärfarbe: [Hex-Code]
Keine politischen oder religiösen Aussagen
Alle Texte auf Deutsch
```

> WICHTIG: Keinen Klarnamen, keine Adresse, keine Telefonnummern oder andere persönliche Kundendaten in den Kontext eingeben. Nur allgemeine Geschäftsbeschreibung.

---

## Divi AI für Custom CSS

Divi AI kann einfaches CSS generieren:

```
Divi Modul → Advanced → Custom CSS → KI-Symbol

Prompt: "Füge einen roten Unterstrich-Animation hinzu wenn der
Benutzer mit der Maus über den Text fährt. Nutze CSS-Transitions."
```

Für komplexes CSS besser Claude Code:

```
/divi-design-system
Erstelle mir das vollständige Button-Preset-System mit
Primär, Outline und Ghost-Button als CSS Custom Properties.
```

---

## Divi AI Module — was ist verfügbar

Ab Divi 5:

- **AI Layout Builder** — komplette Seite per Prompt generieren
- **AI Section Builder** — einzelne Sektion generieren
- **AI Text** — Texte generieren und umschreiben
- **AI Image** — Bilder generieren (Stable Diffusion-basiert)
- **AI Custom CSS** — CSS per Beschreibung

Freikontingent: **100 Nutzungen** pro Monat für Elegant Themes Mitglieder.

---

## Was Divi AI nicht kann (und Claude Code übernimmt)

- PHP-Plugin-Entwicklung mit Sicherheits-Best-Practices
- AJAX-Handler, REST-API-Endpunkte
- Datenbank-Interaktionen mit `$wpdb->prepare()`
- Divi 5 Native Module (React/TSX)
- DSGVO-konforme Implementierungen
- Deployment-Workflows
- Performance-Optimierung (Core Web Vitals)
- Child-Theme-Struktur und Enqueue-System
- Animationen mit GSAP, Three.js, Lenis

---

## Checkliste vor Divi AI Nutzung

- [ ] Divi AI Konto aktiv und Sprache auf Deutsch gesetzt
- [ ] Website-Kontext ohne persönliche Kundendaten
- [ ] Generierter Content wurde auf Richtigkeit geprüft (KI halluziniert!)
- [ ] Bilder aus Divi AI: Lizenz prüfen (ET-Nutzungsbedingungen gelten)
- [ ] Finale Texte wurden manuell überarbeitet
- [ ] Kein generierter Plugin-Code ohne Code-Review in Produktion

---

## Verwandte Commands

- `/divi-design-system` — Design System das Divi AI aufgreift
- `/divi-plugin` — Plugin-Entwicklung (immer Claude Code, nie Divi AI)
- `/divi-optimize` — Performance nach Divi AI Seitenaufbau prüfen
