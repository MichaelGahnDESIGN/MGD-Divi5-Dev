# /divi-design-system

Divi 5 Design System aufbauen — Globale Farben, CSS-Variablen, Fluid Typography mit `clamp()`, Button-Presets und Farbschemata definieren, damit alle Seiten konsistent aussehen.

## Ablauf

1. **Markenfarben erfassen** (Primär, Sekundär, Akzent, Text, Hintergrund)
2. **Divi Global Colors** konfigurieren
3. **CSS Custom Properties** im Child-Theme definieren
4. **Fluid Typography** mit `clamp()` aufsetzen
5. **Button-Presets** anlegen
6. **Spacing-System** definieren
7. **Divi Presets** exportieren (für Wiederverwendung)

---

## Schritt 1 — Divi Global Colors

```
Divi → Customize → Global Colors
```

Dort folgende Farben anlegen und benennen:

| Name | Variable | Beispiel |
|------|----------|---------|
| Primärfarbe | `--clr-primary` | `#ce1517` |
| Primär Hell | `--clr-primary-light` | `#e01915` |
| Text Dunkel | `--clr-text-dark` | `#333333` |
| Text Mittel | `--clr-text-mid` | `#666666` |
| Hintergrund | `--clr-bg` | `#ffffff` |
| Hintergrund Alt | `--clr-bg-alt` | `#f8f8f8` |
| Akzent | `--clr-accent` | `#1a1a2e` |

> Divi 5 speichert Global Colors als CSS Custom Properties — die stehen dann in allen Modulen zur Verfügung.

---

## Schritt 2 — CSS Custom Properties (Child-Theme)

```css
/* style.css — Design Tokens */
:root {
    /* Farben */
    --clr-primary:        #ce1517;
    --clr-primary-light:  #e01915;
    --clr-primary-dark:   #a01012;
    --clr-text-dark:      #333333;
    --clr-text-mid:       #666666;
    --clr-text-light:     #999999;
    --clr-bg:             #ffffff;
    --clr-bg-alt:         #f8f8f8;
    --clr-accent:         #1a1a2e;
    --clr-border:         #e5e5e5;

    /* Typografie — Fluid Sizing (siehe Schritt 3) */
    --fs-xs:   clamp(0.75rem, 0.5vw + 0.65rem, 0.875rem);
    --fs-sm:   clamp(0.875rem, 0.6vw + 0.75rem, 1rem);
    --fs-base: clamp(1rem, 0.8vw + 0.85rem, 1.125rem);
    --fs-md:   clamp(1.125rem, 1vw + 0.95rem, 1.375rem);
    --fs-lg:   clamp(1.375rem, 1.5vw + 1.1rem, 1.875rem);
    --fs-xl:   clamp(1.75rem, 2.5vw + 1.2rem, 2.5rem);
    --fs-2xl:  clamp(2.25rem, 4vw + 1.4rem, 3.5rem);
    --fs-3xl:  clamp(3rem, 6vw + 1.5rem, 5rem);

    /* Spacing — 8px-Raster */
    --sp-1:  0.5rem;   /*  8px */
    --sp-2:  1rem;     /* 16px */
    --sp-3:  1.5rem;   /* 24px */
    --sp-4:  2rem;     /* 32px */
    --sp-6:  3rem;     /* 48px */
    --sp-8:  4rem;     /* 64px */
    --sp-12: 6rem;     /* 96px */
    --sp-16: 8rem;     /* 128px */

    /* Radius */
    --radius-sm: 4px;
    --radius-md: 8px;
    --radius-lg: 16px;
    --radius-full: 9999px;

    /* Schatten */
    --shadow-sm: 0 1px 3px rgba(0,0,0,0.08);
    --shadow-md: 0 4px 16px rgba(0,0,0,0.1);
    --shadow-lg: 0 8px 32px rgba(0,0,0,0.15);

    /* Übergänge */
    --transition-fast:   150ms ease;
    --transition-normal: 300ms ease;
    --transition-slow:   600ms ease;
}
```

---

## Schritt 3 — Fluid Typography mit clamp()

`clamp(MIN, BEVORZUGT, MAX)` — Schriftgröße skaliert flüssig zwischen Viewport-Breiten ohne Media-Queries.

### Formel für den bevorzugten Wert

```
BEVORZUGT = FAKTOR * 1vw + OFFSET
```

Berechnung für z.B. h1 (22px bei 320px Viewport, 56px bei 1440px):
- Steigung = (56 - 22) / (1440 - 320) = 34 / 1120 ≈ 0.0304 → ca. `3vw`
- Offset = 22 - (0.0304 × 320) ≈ 12.3 → ca. `0.77rem`
- Ergebnis: `clamp(1.375rem, 3vw + 0.77rem, 3.5rem)`

### Fluid Typography in Divi-Elementen

```css
/* Divi Überschriften fluid überschreiben */
.et_pb_text h1, .et_pb_posts h1 {
    font-size: var(--fs-3xl) !important;
    line-height: 1.1;
}

.et_pb_text h2 {
    font-size: var(--fs-2xl) !important;
    line-height: 1.15;
}

.et_pb_text h3 {
    font-size: var(--fs-xl) !important;
    line-height: 1.2;
}

.et_pb_text p, .et_pb_text li {
    font-size: var(--fs-base) !important;
    line-height: 1.7;
}
```

### Fluid Section-Abstände

```css
/* Divi Sektionen fluid padding */
.et_pb_section {
    padding-top:    clamp(3rem, 8vw, 8rem) !important;
    padding-bottom: clamp(3rem, 8vw, 8rem) !important;
}

.et_pb_section.mgd-section--eng {
    padding-top:    clamp(1.5rem, 4vw, 4rem) !important;
    padding-bottom: clamp(1.5rem, 4vw, 4rem) !important;
}
```

---

## Schritt 4 — Button-Presets

```css
/* Primär-Button — Divi Button Modul */
.et_pb_button.mgd-btn-primary,
.mgd-btn-primary.et_pb_button {
    background-color: var(--clr-primary) !important;
    border-color:     var(--clr-primary) !important;
    color:            #ffffff !important;
    border-radius:    var(--radius-sm) !important;
    font-weight:      600 !important;
    letter-spacing:   0.03em !important;
    transition:       background-color var(--transition-fast),
                      transform var(--transition-fast),
                      box-shadow var(--transition-fast) !important;
}

.et_pb_button.mgd-btn-primary:hover {
    background-color: var(--clr-primary-dark) !important;
    border-color:     var(--clr-primary-dark) !important;
    transform:        translateY(-2px) !important;
    box-shadow:       var(--shadow-md) !important;
}

/* Outline-Button */
.et_pb_button.mgd-btn-outline {
    background-color: transparent !important;
    border-color:     var(--clr-primary) !important;
    color:            var(--clr-primary) !important;
    border-width:     2px !important;
    border-radius:    var(--radius-sm) !important;
    font-weight:      600 !important;
    transition:       background-color var(--transition-fast),
                      color var(--transition-fast) !important;
}

.et_pb_button.mgd-btn-outline:hover {
    background-color: var(--clr-primary) !important;
    color:            #ffffff !important;
}

/* Ghost-Button (für dunkle Hintergründe) */
.et_pb_button.mgd-btn-ghost {
    background-color: rgba(255,255,255,0.1) !important;
    border-color:     rgba(255,255,255,0.6) !important;
    color:            #ffffff !important;
    border-width:     2px !important;
    border-radius:    var(--radius-sm) !important;
    backdrop-filter:  blur(4px) !important;
}

.et_pb_button.mgd-btn-ghost:hover {
    background-color: rgba(255,255,255,0.2) !important;
    border-color:     #ffffff !important;
}
```

---

## Schritt 5 — Colorscheme Generator (Divi 5.5+)

Ab Divi 5.5 gibt es den eingebauten **Colorscheme Generator**:

```
Divi Visual Builder → Design → Colors → Colorscheme Generator
→ Basisfarbe eingeben → Harmonie-Typ wählen:
  - Komplementär (gegenüberliegend)
  - Analog (nebeneinander)
  - Triadisch (3 gleichmäßig verteilt)
  - Split-Komplementär (weicher Kontrast)
→ Palette in Global Colors übernehmen
```

---

## Schritt 6 — Design System in functions.php registrieren

```php
// functions.php
add_action('wp_enqueue_scripts', function () {

    // Style mit Design-Tokens zuerst laden
    wp_enqueue_style(
        'mgd-design-tokens',
        get_stylesheet_directory_uri() . '/css/design-tokens.css',
        ['divi-style'],
        '1.0.0'
    );

    // Haupt-Stylesheet
    wp_enqueue_style(
        'mgd-main-style',
        get_stylesheet_directory_uri() . '/style.css',
        ['mgd-design-tokens'],
        '1.0.0'
    );
});

// Design Tokens auch im Divi Builder verfügbar machen
add_action('et_builder_ready', function () {
    add_action('et_fb_enqueue_assets', function () {
        wp_enqueue_style(
            'mgd-design-tokens-builder',
            get_stylesheet_directory_uri() . '/css/design-tokens.css',
            [],
            '1.0.0'
        );
    });
});
```

---

## Checkliste — Design System

- [ ] Markenfarben als Divi Global Colors angelegt
- [ ] CSS Custom Properties in `design-tokens.css` oder `style.css` definiert
- [ ] Fluid Typography für h1–h3 und Body-Text aktiv
- [ ] Button-Presets als CSS-Klassen bereit (im Divi Modul → Advanced → CSS Class eintragen)
- [ ] Spacing-System mit `--sp-*` Variablen definiert
- [ ] Design-Tokens im Divi Builder sichtbar (kein weißer Hintergrund im Editor)
- [ ] Presets in Divi exportiert und gesichert

---

## Verwandte Commands

- `/divi-childtheme` — Basis-Struktur für Design System
- `/divi-optimize` — Kritisches CSS aus Design Tokens extrahieren
- `/divi-theme-builder` — Design System auf alle Templates anwenden
