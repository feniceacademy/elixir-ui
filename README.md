# elixir-ui

Design system condiviso dei gestionali Elixir Group.

Identità: `#ff9330` · `#000000` · `#f5f2ef` · Poppins + JetBrains Mono.

Consumato da: `crm` (amministrativo), `crm-marketing`, `serenamente-outreach`.

## Struttura

```
src/
  tokens.css              # variabili --eg-* : colori, tipografia, spazi, ombre, motion, z-index
  base.css                # reset minimo — volutamente non invasivo durante le migrazioni
  components/
    layout.css            # .eg-shell / .eg-sidebar / .eg-topbar / .eg-page
    button.css            # .eg-btn — primary | secondary | ghost | danger, sm | md | lg
    form.css              # .eg-field / .eg-input / .eg-select / .eg-textarea
    data.css              # .eg-table / .eg-card / .eg-badge / .eg-empty
    overlay.css           # .eg-modal / .eg-toast / .eg-alert / .eg-tabs
scripts/build.mjs         # concatena src/ in dist/ — l'ordine conta
dist/elixir-ui.css        # generato, committato: i consumer via submodule non eseguono npm install
demo.html                 # style guide navigabile, apribile in locale dopo il build
```

`dist/` è versionato di proposito. Un submodule non fa girare `npm install`, quindi
l'hook `prepare` non scatta: senza il file committato i gestionali agganciati non
avrebbero il CSS compilato.

## Build

```bash
npm run build      # rigenera dist/elixir-ui.css
open demo.html     # style guide
```

Dopo ogni modifica a `src/`: rilanciare il build e committare **anche** `dist/`.

## Come agganciarlo a un gestionale

Come submodule, così un aggiornamento qui si propaga a tutti i repo che lo puntano:

```bash
git submodule add https://github.com/feniceacademy/elixir-ui vendor/elixir-ui
```

Poi, a seconda del livello di adozione:

```css
/* solo token — l'app tiene le sue classi */
@import "../../vendor/elixir-ui/src/tokens.css";

/* sistema completo — l'app usa le classi .eg-* */
@import "../../vendor/elixir-ui/dist/elixir-ui.css";
```

Per aggiornare un gestionale all'ultima versione del design system:

```bash
git submodule update --remote vendor/elixir-ui
git add vendor/elixir-ui && git commit -m "chore(ui): allinea elixir-ui"
```

Il submodule punta a un commit preciso: l'aggiornamento è esplicito e va fatto per
ogni gestionale. È voluto — un design system che cambia sotto i piedi in produzione
senza che nessuno l'abbia deciso è un problema, non una feature.

## Temi e sotto-aziende

```html
<html data-eg-theme="dark">        <!-- tema scuro -->
<html data-eg-brand="serenamente"> <!-- accento per sotto-azienda -->
```

Senza attributi resta l'arancione di gruppo. Fenice Academy lo condivide: nessun override.

## Convenzioni

- Prefisso `eg-` su ogni classe e variabile: convive con Tailwind o CSS esistente senza collisioni.
- L'arancione è marchio e azione, **mai** avviso — il warning è ambra scuro (`--eg-warning-500`).
- Testo su arancione pieno: nero (`--eg-on-primary`), come nel logo.
- Per testo e link non usare `#ff9330` (2.2:1 sul bianco): esistono i toni 700/800.
- Le altezze dei controlli (30/38/46px) sono ciò che rende due app riconoscibilmente gemelle: non ritoccarle per singola app.
