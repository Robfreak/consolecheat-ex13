# Combo-Trainer

Kampfspiel-Eingabefolgen per Tastatur oder Controller nachspielen, mit Frame-Timing. Teil der inoffiziellen consolecheat-Werkzeuge rund um [consolecheat.com](https://consolecheat.com). German is the primary language, English is the other. Light and dark theme, self-hosted fonts, footer, Impressum, and Datenschutz are included. There is no Webmail link.

No account, no tracking, nothing uploaded. Fonts (Outfit, Source Sans 3) are self-hosted from `@fontsource`, so the page makes no request to Google or any other third party. The Impressum fields are placeholders until the operator fills them in. No name or address was invented.

Site: <https://robfreak.github.io/consolecheat-ex13/>

Inoffiziell. Nicht von Sony.

## What it does

A local fighting-game training page. Open it at `/consolecheat-ex13/`. German is the default. English is the other language. Light and dark follow `consolecheat-theme`. There is no Webmail link. Fonts are the self-hosted Outfit and Source Sans 3 files. The page does not call a third party.

Built-in combos are Hadouken (↓ ↘ →□), Shoryuken (→ ↓ ↘△), Tatsu (↓ ↙ ←○), a half-circle (← ↙ ↓ ↘ →□), a double quarter-circle (↓ ↘ → ↓ ↘ →△), a 360-ish spin (→ ↘ ↓ ↙ ← ↖ ↑×), and a button chain (□ □ △ ×). Directions are numpad notation inside the code. A step is a direction, a button, or both.

Keyboard: **W A S D** or the arrow keys. Hold two keys for a diagonal, so down, then down and right, then right alone, is ↓ ↘ →. **J K L I** is □ △ × ○. The other layout, **U I J K**, is the same four symbols in that order. The legend on the page shows the active map. Keys are ignored while a text field is focused.

A standard controller is polled with `requestAnimationFrame`. D-pad buttons 12–15 and the left stick (deadzone 0.5, negative Y is up) become the same 8-way direction. The direction is the held state each frame, so a diagonal appears when both axes are outside the deadzone. Face buttons are 0 ×, 1 ○, 2 □, 3 △. The first poll seeds whatever is already held and does not count it. After that, a direction change or a new press counts. On a narrow screen the same directions and buttons are on-screen controls.

Each step after the first has to land within the frame window. The window is 4 to 30 frames at 60 fps, default 12, from `performance.now()`. The page shows the frame gap of each accepted step, whether it was on time, the hit rate, the attempt count, and the success streak. A wrong direction, a wrong button, or a late input aborts, names the reason, and returns to step 0. Neutral and a repeat of the direction already accepted do not abort. The input history keeps the last 20 inputs with their frame gaps.

**Eigenes Combo** records inputs or adds steps from the palette. A custom combo has a name and an optional window. It can be edited and deleted. Built-in combos cannot be deleted.

Best streak, best hit rate, and fastest total frames stay in this browser under `localStorage` key `consolecheat-combo-v1` (`version` 1, `window`, `layout`, `customs`, `bests`, `stats`). A missing key is not created until you save a combo, change a setting, or finish an attempt. A value that does not parse, or a different version, falls back to the defaults and does not crash. **Gespeicherte Combos und Bestwerte löschen** on the Datenschutz page removes only `consolecheat-combo-v1`. Language (`consolecheat-lang`) and appearance (`consolecheat-theme`) stay. The Datenschutz page names the key, says the values stay in the browser, and names Art. 6 Abs. 1 lit. f DSGVO for the host’s connection logs.

`prefers-reduced-motion` drops transitions and animation. Results are announced in an `aria-live` region. The on-screen buttons stay usable at 390px.

To try it: `npm run dev`, open `http://127.0.0.1:5173/consolecheat-ex13/`, set the window if you are clicking rather than playing on a pad, and enter ↓ ↘ →□ for Hadouken. **J** is □ in the default layout.

## Storage

- `consolecheat-combo-v1` (localStorage)
- `consolecheat-lang` and `consolecheat-theme` (localStorage, shared with the other consolecheat tools on robfreak.github.io)

The Datenschutz page has a button that removes this page's keys. Nothing else is stored.

## Run and test

```bash
npm install
npm test        # node --experimental-strip-types --test src/combo/*.test.ts
npm run dev     # http://127.0.0.1:5173/consolecheat-ex13/
npm run build   # typecheck, Vite build (base /consolecheat-ex13/), offline check of dist/
npm run preview # http://127.0.0.1:4173/consolecheat-ex13/
```

Node `>=22.6` (`package.json` `engines`).

## Files

- `index.html` — the HTML entry (Vite input)
- `src/combo/` — React + TypeScript source, styles, and tests
- `src/combo/tools.ts` + `src/combo/tool-links.tsx` — the footer list **Weitere Werkzeuge** (keep it identical across the consolecheat repos)
- `public/` — `favicon.svg`, `FONT-OFL.txt`, `.nojekyll`
- `scripts/check-dist.mjs` — offline check of `dist/` (no third-party hosts, no `.woff` fallback, woff2 fonts present)
- `.github/workflows/pages.yml` — test, build, and deploy to `gh-pages`

## Other tools

The footer group **Weitere Werkzeuge** (English: **Other tools**) links to the other consolecheat tools: Title-ID-Finder (ex1), PS-Plus-Archiv (ex2), Controller-Tester (ex3), Save-Info-Leser (ex4), Fehlercode-Nachschlager (ex5), the [Spiele-Merkliste](https://robfreak.github.io/consolecheat-ex6/), and [Bildschirm-Test](https://robfreak.github.io/consolecheat-ex7/), [Download-Zeit-Rechner](https://robfreak.github.io/consolecheat-ex8/), [Tastenbelegung](https://robfreak.github.io/consolecheat-ex9/), [HDR/Helligkeit](https://robfreak.github.io/consolecheat-ex10/), [Audio-Kanal-Test](https://robfreak.github.io/consolecheat-ex11/), [USB-Stick-Checkliste](https://robfreak.github.io/consolecheat-ex12/), [Sprite-Animator](https://robfreak.github.io/consolecheat-ex14/). These are ordinary links. The page does not request those sites.

This tool was moved here from [Robfreak/consolecheat-ex6](https://github.com/Robfreak/consolecheat-ex6).

## GitHub Pages

`.github/workflows/pages.yml` runs install, test, and build on pull requests and on every push. A push to `main` also pushes `dist/` to the orphan branch `gh-pages` (`peaceiris/actions-gh-pages`, Jekyll off). Vite `base` is `/consolecheat-ex13/`, which matches the project site <https://robfreak.github.io/consolecheat-ex13/>.

Enable once in the repository settings:

1. **Settings → Actions → General → Workflow permissions → Read and write permissions.** Save.
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch.** Branch: **`gh-pages`**, folder: **`/ (root)`.** Save.

After that, every push to `main` updates the site.

## Credits

Outfit and Source Sans 3 are bundled from `@fontsource` under the SIL Open Font License; see `public/FONT-OFL.txt` and `THIRD_PARTY_NOTICES.md`.

Replace the Impressum placeholders with the operator’s real details before treating that page as a legal notice.
