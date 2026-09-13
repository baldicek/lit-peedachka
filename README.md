# Prague Stop Collector

A personal, installable, mostly-offline web app for tracking which Prague
public transport stops you've visited or driven through.

## What's in this folder

- `index.html`, `css/style.css`, `js/app.js` — the app itself
- `data/stops.json` — the stop + line data the app reads. Ships with a
  starter set (~15 real, verified stops) — see "Getting every stop" below.
- `manifest.json`, `service-worker.js`, `icons/` — what makes this
  installable on your phone and usable offline
- `icons/star.png` — the "visited" marker. **Replace this file with any
  other PNG of the same name** to use a different icon; nothing else needs
  to change.

## 1. Put it online (so it can be "installed" and work offline)

A phone needs to load this over `https://` (or `localhost`) at least once
for "Add to Home Screen" and offline mode to work — opening the raw files
from a folder on the phone doesn't support that. The easiest free way:

1. Create a free account at [github.com](https://github.com) if you don't
   have one.
2. Create a new repository (e.g. `prague-stops`), and upload every file in
   this folder to it (drag-and-drop on the GitHub website works fine —
   keep the folder structure, e.g. `css/style.css` stays inside a `css`
   folder).
3. In the repository, go to **Settings → Pages**, set "Source" to the
   `main` branch, root folder, and save.
4. After a minute, GitHub gives you a URL like
   `https://yourname.github.io/prague-stops/`. Open that on your phone.

## 2. Install it on your phone

- **Android (Chrome):** open the URL, tap the ⋮ menu → **"Add to Home
  screen"** (or you'll see a banner offering to install it).
- Once installed, it opens full-screen like a normal app, and works
  without internet for everything except *new* map areas you haven't
  scrolled to before (those need one data connection to fetch tiles; after
  that they're cached).

## 3. Getting every Prague stop (not just the starter set)

The app ships with a real, verified sample of ~15 stops so you can try it
today. To get **every** Prague PID stop with its exact line list:

1. On a computer with a normal browser, go to:
   `https://data.pid.cz/stops/json/stops.json`
2. Save the file (Ctrl+S / Cmd+S).
3. Send me that file in our chat and ask me to rebuild `data/stops.json`
   from it, filtered to Prague only (I'll match on `"municipality":
   "Praha"`) and reshaped into the format this app expects.
4. I'll hand you back an updated `data/stops.json` — replace the one in
   your GitHub repo with it (or re-download the whole app from me) and
   reload the page on your phone once while online.

This file is published by ROPID/PID (Prague's transit authority) as open
data under a CC-BY 4.0 licence, and is regenerated daily, so it's always
current — see `pid.cz/en/opendata/` for details and licence terms.

## Notes on accuracy

- The starter data was pulled live from PID's feed and double-checked
  against PID's own line-B documentation, so it's accurate as far as it
  goes — but it's only a sample.
- "Karlovo náměstí" in the sample only lists metro line B. The physical
  hub at that square also has tram stops, but PID lists those under the
  adjacent stop names ("Novoměstská radnice", "Palackého náměstí", etc.)
  that share the same transfer node — they'll show up correctly as separate
  markers once the full dataset is loaded.
- Ferries, the Petřín funicular, metro A/C, and the S-line trains aren't in
  the starter sample (I didn't have verified data for them on hand yet) —
  they'll all appear once the full file is imported.

## Customising

- **Colours:** edit the `:root` variables at the top of `css/style.css`
  (`--lime`, `--black`, etc).
- **Visited icon:** replace `icons/star.png` with any PNG (square, ideally
  transparent background, ~128×128px works well).
- **App name on the home screen:** edit `short_name` in `manifest.json`.
