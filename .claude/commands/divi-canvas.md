# /divi-canvas

Divi Canvases erstellen — Popups, Off-Canvas Menüs, modales Overlays und Slide-In Panels.

Divi Canvases (neu in Divi 5) sind separate Layout-Bereiche die außerhalb des normalen Seitenlayouts existieren und per Trigger ein- und ausgeblendet werden.

## Ablauf

1. **Canvas-Typ klären**: Popup, Off-Canvas Menü, Slide-In, Vollbild-Overlay?
2. **Canvas anlegen**: Divi Theme Builder → Canvases
3. **Inhalt gestalten** (normale Divi-Module)
4. **Trigger setzen** (Button, Link, Scroll, Timer, Exit Intent)
5. **Conditions definieren** (auf welchen Seiten)
6. **Testen auf Desktop + Mobil**

---

## Canvas anlegen

```
Divi → Theme Builder → Canvases → Neuer Canvas
→ Canvas-Name vergeben (intern, nicht öffentlich)
→ Layout aufbauen mit normalen Divi-Modulen
→ Speichern
```

---

## Popup — klassisches Modal

```
Canvas-Einstellungen:
  Typ: Modal/Popup
  Position: Mitte
  Hintergrund: rgba(0, 0, 0, 0.7) (Overlay)
  Breite: 600px (Desktop), 90vw (Mobil)
  Animation: Fade In + Scale (0.8 → 1)
```

```css
/* Popup-Stile (Custom CSS im Canvas) */
.mgd-popup-wrapper {
    background: #ffffff;
    border-radius: 8px;
    padding: 2.5rem;
    position: relative;
    max-height: 90vh;
    overflow-y: auto;
}

/* Schließen-Button */
.mgd-popup-close {
    position: absolute;
    top: 1rem;
    right: 1rem;
    width: 32px;
    height: 32px;
    background: transparent;
    border: none;
    cursor: pointer;
    font-size: 1.25rem;
    color: #666666;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transition: background-color 200ms ease;
}

.mgd-popup-close:hover {
    background: #f0f0f0;
}
```

---

## Off-Canvas Menü (Slide-In von links/rechts)

```
Canvas-Einstellungen:
  Typ: Off-Canvas
  Position: Links oder Rechts
  Breite: 320px (Desktop), 85vw (Mobil)
  Animation: Slide In
  Overlay: aktiv, klick schließt Canvas
```

```css
/* Off-Canvas Navigation */
.mgd-offcanvas {
    height: 100%;
    display: flex;
    flex-direction: column;
    padding: 2rem 1.5rem;
    background: #ffffff;
}

.mgd-offcanvas__logo {
    margin-bottom: 2rem;
    padding-bottom: 1.5rem;
    border-bottom: 1px solid #e5e5e5;
}

.mgd-offcanvas__nav {
    list-style: none;
    margin: 0;
    padding: 0;
    flex: 1;
}

.mgd-offcanvas__nav li {
    margin: 0;
    border-bottom: 1px solid #f0f0f0;
}

.mgd-offcanvas__nav a {
    display: block;
    padding: 0.875rem 0;
    font-weight: 600;
    color: #333333;
    text-decoration: none;
    font-size: 1.0625rem;
    transition: color 200ms ease, padding-left 200ms ease;
}

.mgd-offcanvas__nav a:hover {
    color: #ce1517;
    padding-left: 0.5rem;
}

.mgd-offcanvas__footer {
    margin-top: auto;
    padding-top: 1.5rem;
    font-size: 0.875rem;
    color: #999999;
}
```

---

## Trigger per Button

```
Divi Button-Modul → Advanced → Link:
  URL: #
  Link-Klasse: mgd-canvas-trigger
  Data-Attribut: data-canvas-id="mein-canvas-id"
```

Oder per JavaScript (wenn kein natives Divi-Trigger-System verfügbar):

```javascript
// js/canvas-trigger.js
(function () {
    'use strict';

    // Divi Builder ausschließen
    if (document.body.classList.contains('et-fb')) return;

    // Alle Trigger-Buttons
    document.querySelectorAll('[data-canvas-trigger]').forEach(function (btn) {
        btn.addEventListener('click', function (e) {
            e.preventDefault();
            const canvasId = btn.dataset.canvasTrigger;
            const canvas = document.getElementById(canvasId);
            if (!canvas) return;

            canvas.classList.add('mgd-canvas--aktiv');
            document.body.classList.add('mgd-canvas-offen');
            document.body.style.overflow = 'hidden';

            // Schließen-Button innerhalb Canvas
            const schliessen = canvas.querySelector('.mgd-canvas-schliessen');
            if (schliessen) {
                schliessen.addEventListener('click', schliessCanvas, { once: true });
            }

            // Overlay-Klick schließt
            const overlay = canvas.querySelector('.mgd-canvas-overlay');
            if (overlay) {
                overlay.addEventListener('click', schliessCanvas, { once: true });
            }
        });
    });

    function schliessCanvas() {
        document.querySelectorAll('.mgd-canvas--aktiv').forEach(function (c) {
            c.classList.remove('mgd-canvas--aktiv');
        });
        document.body.classList.remove('mgd-canvas-offen');
        document.body.style.overflow = '';
    }

    // Escape-Taste schließt
    document.addEventListener('keydown', function (e) {
        if (e.key === 'Escape') schliessCanvas();
    });
}());
```

---

## Scroll-Trigger Popup

```javascript
// js/scroll-popup.js — Popup nach 60% Scrollen
(function () {
    'use strict';

    if (document.body.classList.contains('et-fb')) return;

    // Nur einmal pro Session zeigen
    if (sessionStorage.getItem('mgd-popup-gezeigt')) return;

    const SCROLL_SCHWELLE = 0.6; // 60% der Seite

    function pruefeScroll() {
        const scrollPos = window.scrollY + window.innerHeight;
        const seitenHoehe = document.documentElement.scrollHeight;

        if (scrollPos / seitenHoehe >= SCROLL_SCHWELLE) {
            window.removeEventListener('scroll', pruefeScroll);

            const popup = document.getElementById('mgd-scroll-popup');
            if (popup) {
                popup.classList.add('mgd-canvas--aktiv');
                document.body.style.overflow = 'hidden';
                sessionStorage.setItem('mgd-popup-gezeigt', '1');
            }
        }
    }

    window.addEventListener('scroll', pruefeScroll, { passive: true });
}());
```

---

## Exit-Intent Popup

```javascript
// js/exit-intent.js — Popup wenn Maus den Browser verlässt
(function () {
    'use strict';

    if (document.body.classList.contains('et-fb')) return;
    if (sessionStorage.getItem('mgd-exit-gezeigt')) return;

    // Nur Desktop (kein Touch)
    if ('ontouchstart' in window) return;

    let ausgeloest = false;

    document.addEventListener('mouseleave', function (e) {
        if (e.clientY > 20 || ausgeloest) return;
        ausgeloest = true;

        const popup = document.getElementById('mgd-exit-popup');
        if (popup) {
            popup.classList.add('mgd-canvas--aktiv');
            document.body.style.overflow = 'hidden';
            sessionStorage.setItem('mgd-exit-gezeigt', '1');
        }
    });
}());
```

---

## Animationen für Canvas

```css
/* Canvas Basis-Stile */
.mgd-canvas {
    position: fixed;
    z-index: 99999;
    visibility: hidden;
    pointer-events: none;
}

.mgd-canvas--aktiv {
    visibility: visible;
    pointer-events: all;
}

/* Popup — Fade + Scale */
.mgd-canvas--popup .mgd-canvas-inhalt {
    transform: scale(0.92) translateY(-10px);
    opacity: 0;
    transition: transform 300ms cubic-bezier(0.34, 1.56, 0.64, 1),
                opacity 250ms ease;
}

.mgd-canvas--popup.mgd-canvas--aktiv .mgd-canvas-inhalt {
    transform: scale(1) translateY(0);
    opacity: 1;
}

/* Off-Canvas — Slide von rechts */
.mgd-canvas--rechts .mgd-canvas-inhalt {
    transform: translateX(100%);
    transition: transform 350ms cubic-bezier(0.4, 0, 0.2, 1);
}

.mgd-canvas--rechts.mgd-canvas--aktiv .mgd-canvas-inhalt {
    transform: translateX(0);
}

/* Overlay */
.mgd-canvas-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.6);
    opacity: 0;
    transition: opacity 300ms ease;
}

.mgd-canvas--aktiv .mgd-canvas-overlay {
    opacity: 1;
}
```

---

## Enqueue in functions.php

```php
add_action('wp_enqueue_scripts', function () {
    if (is_admin()) return;

    wp_enqueue_script(
        'mgd-canvas',
        get_stylesheet_directory_uri() . '/js/canvas-trigger.js',
        [],
        '1.0.0',
        ['strategy' => 'defer', 'in_footer' => true]
    );
});
```

---

## Checkliste

- [ ] Canvas im Theme Builder angelegt und gespeichert
- [ ] Trigger (Button/Scroll/Exit) funktioniert
- [ ] Schließen per Klick, Overlay-Klick und Escape-Taste
- [ ] `overflow: hidden` auf body wenn Canvas offen
- [ ] Kein Scrollen im Hintergrund wenn Canvas offen (iOS Fix beachten!)
- [ ] Divi Builder ausgeschlossen (`et-fb` Check)
- [ ] SessionStorage verhindert Popup-Spam
- [ ] Mobile getestet (Breakpoints, Touch-Verhalten)

### iOS Scroll-Lock Fix

```css
/* iOS verhindert overflow:hidden auf body — Fix: */
body.mgd-canvas-offen {
    overflow: hidden;
    position: fixed;    /* iOS Fix */
    width: 100%;
}
```

---

## Verwandte Commands

- `/divi-animations` — Animationen für Canvas-Inhalt
- `/divi-theme-builder` — Canvas-Templates im Theme Builder verwalten
- `/divi-design-system` — Einheitliche Stile für Canvas-Komponenten
