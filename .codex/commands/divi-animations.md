# /divi-animations

Binde Animations-Bibliotheken lokal ein und konfiguriere sie Divi-kompatibel.

## Verhalten

Nutze `skill/DIVI5-SKILL.md` als Arbeitsgrundlage und führe den Abschnitt `/divi-animations` durch:

1. Abfragen welche Libraries gebraucht werden (GSAP, AOS, Lenis, Three.js, Swiper, Alpine, Tilt)
2. Download-Anleitung für lokale Dateien ausgeben
3. Enqueue-Code in `functions.php` einfügen
4. Initialisierungs-Code in `main.js` einfügen
5. Divi-spezifische Quirks beachten und erklären

## Regeln

- Libraries IMMER lokal hosten — keine CDN-Links ohne explizite Erlaubnis
- Divi Builder ausschließen (`et-fb`-Klasse und `?et_fb=1` prüfen)
- `window.load` statt nur `DOMContentLoaded` wegen Divi Lazy-Loading
- `jQuery` statt `$` im WordPress noConflict-Modus
- GSAP: `ScrollTrigger.refresh()` nach Image-Load aufrufen

## Ergebnis

Am Ende kurz berichten:
- Welche Libraries eingebunden wurden
- Welche Dateien manuell heruntergeladen werden müssen
- Divi-spezifische Hinweise die beachtet werden müssen
