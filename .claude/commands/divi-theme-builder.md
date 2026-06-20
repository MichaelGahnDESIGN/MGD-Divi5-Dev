# /divi-theme-builder

Divi 5 Theme Builder — Header, Footer, Single-Post-Templates, Archive-Seiten und Custom Post Type Templates erstellen.

## Ablauf

1. **Ziel klären**: Welche Templates werden gebraucht? (Header, Footer, Single, Archive, 404, CPT?)
2. **Divi Theme Builder öffnen**: Divi → Theme Builder
3. **Templates nach Typ anlegen** (siehe unten)
4. **Conditions setzen**: Wo gilt welches Template?
5. **Dynamic Content** einbinden (Titel, Featured Image, Autor, Datum, Kategorien)
6. **Testen**: Preview in verschiedenen Seitenkontexten prüfen

---

## Template-Typen und Conditions

### Globale Templates (gelten überall)

```
Theme Builder → Add Global Header
Theme Builder → Add Global Footer
```

Conditions: **All Pages** — gilt für alle Seiten außer explizit ausgeschlossenen.

### Single Post Template

```
Theme Builder → Add New Template
Conditions: Singular → Post
```

Dynamic Content-Module im Template:
- **Divi Post Title** — zeigt `{{Beitragsname}}`
- **Divi Post Content** — zeigt `{{Beitragsinhalt}}`
- **Divi Post Featured Image** — zeigt `{{Beitragsbild}}`
- **Divi Post Author** — zeigt `{{Autor}}`
- **Divi Post Date** — zeigt `{{Datum}}`
- **Divi Post Categories** — zeigt `{{Kategorien}}`
- **Divi Post Tags** — zeigt `{{Schlagwörter}}`

### Archive / Blog Template

```
Theme Builder → Add New Template
Conditions: Archive → Post Archive (oder Kategorie, Tag, Autor)
```

Empfehlung: Divi Blog-Modul im Loop-Modus verwenden:

```
Divi Blog-Modul → Layout: Masonry oder Grid
Beitragsanzahl: 9
Paginierung: aktiviert
Featured Image: aktiviert
```

### Custom Post Type Template

```
Theme Builder → Add New Template
Conditions: Singular → [Dein CPT-Name]
```

```php
// CPT registrieren (functions.php oder Plugin)
register_post_type('projekte', [
    'labels'    => ['name' => 'Projekte', 'singular_name' => 'Projekt'],
    'public'    => true,
    'has_archive' => true,
    'show_in_rest' => true,
    'supports'  => ['title', 'editor', 'thumbnail', 'custom-fields'],
    'rewrite'   => ['slug' => 'projekte'],
]);
```

### 404-Seite

```
Theme Builder → Add New Template
Conditions: 404 Page
```

Inhalt: Klare Botschaft + Suche + Link zur Startseite. Kein Dynamic Content nötig.

---

## Sticky Header — vollständige Implementierung

```php
// functions.php — Sticky Header Script
add_action('wp_enqueue_scripts', function () {
    if (is_admin()) return;

    wp_enqueue_script(
        'mgd-sticky-header',
        get_stylesheet_directory_uri() . '/js/sticky-header.js',
        ['jquery'],
        '1.0.0',
        ['strategy' => 'defer', 'in_footer' => true]
    );
});
```

```javascript
// js/sticky-header.js
(function ($) {
    'use strict';

    // Divi Builder ausschließen
    if (document.body.classList.contains('et-fb') ||
        new URLSearchParams(window.location.search).has('et_fb')) {
        return;
    }

    const header = document.querySelector('#main-header, .et-l--header');
    if (!header) return;

    let letzteScrollPos = 0;
    const SCHWELLENWERT = 100; // px ab wann Header sticky wird

    window.addEventListener('scroll', function () {
        const aktuellePos = window.scrollY;

        if (aktuellePos > SCHWELLENWERT) {
            header.classList.add('mgd-header--sticky');

            // Scrollen nach unten → Header verstecken
            if (aktuellePos > letzteScrollPos) {
                header.classList.add('mgd-header--versteckt');
            } else {
                // Scrollen nach oben → Header zeigen
                header.classList.remove('mgd-header--versteckt');
            }
        } else {
            header.classList.remove('mgd-header--sticky', 'mgd-header--versteckt');
        }

        letzteScrollPos = aktuellePos;
    }, { passive: true });

}(jQuery));
```

```css
/* style.css — Sticky Header Stile */
.mgd-header--sticky {
    position: fixed !important;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9999;
    background: rgba(255, 255, 255, 0.97) !important;
    backdrop-filter: blur(8px);
    box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.mgd-header--versteckt {
    transform: translateY(-100%) !important;
}

/* Platz für den fixierten Header kompensieren */
body.mgd-header--sticky-aktiv #page-container {
    padding-top: var(--header-hoehe, 80px);
}
```

---

## Dynamic Content — Custom Fields

Für ACF (Advanced Custom Fields) oder native WordPress Custom Fields:

```
Divi Textmodul → Inhalt → Dynamic Content Symbol (⚡)
→ Custom Field auswählen
```

Oder per PHP im Template:

```php
// Benutzerdefiniertes Feld ausgeben (sicher, escaped)
$wert = get_post_meta(get_the_ID(), 'mein_feld', true);
if ($wert) {
    echo '<div class="mgd-custom-feld">' . esc_html($wert) . '</div>';
}
```

---

## WooCommerce — Shop-Templates

```
Theme Builder → Add New Template
Conditions:
  - WooCommerce → Shop Page (Produktliste)
  - WooCommerce → Single Product (Produktdetail)
  - WooCommerce → Product Category Archive
```

> Divi hat eigene WooCommerce-Module: Divi Woo Product Grid, Divi Woo Product Image, Divi Woo Product Description, Divi Woo Add To Cart usw.

---

## Checkliste vor Go-Live

- [ ] Alle Templates im Preview getestet (Desktop + Mobil)
- [ ] 404-Seite existiert und ist sinnvoll
- [ ] Header und Footer auf allen Seiten korrekt
- [ ] CPT-Archive-URLs erreichbar (Permalinks neu speichern!)
- [ ] Keine Divi-Default-Templates aktiv die überschrieben werden sollten
- [ ] Ladezeit geprüft (Theme Builder kann CSS vervielfachen)

---

## Verwandte Commands

- `/divi-childtheme` — Child-Theme als Basis für Theme Builder
- `/divi-optimize` — Performance nach Theme Builder Aufbau prüfen
- `/divi-plugin` — Custom Post Types als Plugin auslagern
