# Tofu gallery copy

This repository is Tofu's copy of **pkalogiros/AudioMass** (licence: MIT), listed in Tofu's app gallery as **AudioMass**.

AudioMass is a free audio and waveform editor that runs entirely in the browser: open an audio file or the bundled sample, cut, trim, fade, apply effects, record, mix several tracks, and export WAV, MP3 or FLAC. It has no server part and no database.

- `production` mirrors the upstream repository (it is upstream's default branch) and is never committed to by Tofu.
- `tofu` carries Tofu's own changes; tags named `pin/<date>` (`pin/<date>.1`, `.2` and so on for a corrected pin on the same day) mark the versions the gallery points to.
- A visitor who chooses this app gets a private snapshot of the pinned version in their own Tofu account. Their copy does not follow upstream updates.

## Upstream

- Repository: https://github.com/pkalogiros/AudioMass
- Commit: `21f5ee1362a47be6f0dbe6e4969a15e43d21b044` ("(tweaks) tooltip being hidden", 2026-08-20), the head of `production` when this copy was pinned. `tofu` is that commit plus the changes listed below.

## How Tofu runs it

Tofu hosts the `src` folder as a finished static site; nothing is built. The app lives in `src` and the repository root has no `index.html`, so the root folder must be set to `src`.

| Setting | Value |
| --- | --- |
| Framework preset | `static` |
| Root folder | `src` |
| Install command | none |
| Build command | none |
| Output directory | none: the root folder is served as it is, and `src/index.html` is the page |
| Environment variables | none |
| Database | none |

Only the `src` folder is imported, which is why it carries its own `LICENSE` and `THIRD_PARTY_NOTICES.md`. Tofu's importer also drops every folder named `dist`, `build`, `target`, `node_modules` and a few others, so nothing the page loads may sit in one.

## What Tofu changes

Everything below is on `tofu`, dated 2026-10-23.

- `src/index.html` loads WaveSurfer.js from `src/vendor/wavesurfer/`. The editor needs `wavesurfer.js` and its regions plugin before it can start, and upstream keeps them in `src/dist/`. Tofu's importer drops every folder named `dist`, so an imported copy never got those two files and the editor could not start. `src/vendor/wavesurfer/wavesurfer.js` and `src/vendor/wavesurfer/plugin/wavesurfer.regions.js` are byte-for-byte copies of `src/dist/wavesurfer.js` and `src/dist/plugin/wavesurfer.regions.js` (SHA-256 `7a502bf2...` and `ce232939...`). Upstream's files stay where they are; the page no longer uses them. The only other change to `index.html` is one HTML comment that says this.
- `src/vendor/wavesurfer/LICENSE` is the BSD-3-Clause licence text of WaveSurfer.js (the `LICENSE` file at the `2.0.5` tag of katspaugh/wavesurfer.js, the version named in the headers of the copied files), so the vendored copies carry their licence.
- `src/LICENSE` is a byte-for-byte copy of the root `LICENSE`. `src/THIRD_PARTY_NOTICES.md` is the root notices file with its paths made relative to `src` and the WaveSurfer.js row naming the vendored copies; a note at its top says so. The root files are untouched.
- Five files are no longer in `src/`. Tofu's Free plan serves a finished site only when every file in it is a type its static hosting serves, and refuses the whole site for one it does not; the check named exactly these five, none of which the editor loads (`index.html` loads `main.css`, and `main.css` loads its icon font from `fonts/icomoon.woff`):
  - `src/audiomass.appcache`, the manifest of the retired AppCache, and `src/main.build.css.br`, a Brotli-compressed copy of `src/main.build.css` for servers that hand out compressed files: deleted. Upstream keeps both on `production`. Nothing in `src` loads `main.build.css` either; it stays.
  - `src/fonts/icomoon.eot`, the icon font in the format of Internet Explorer 8 and older: deleted. `icomoon.woff`, `.ttf` and `.svg` stay in `src/fonts/`.
  - `src/audiomass-server.go` and `src/audiomass-server.py`, upstream's two local dev servers: moved, byte for byte, to `dev-servers/` at the repository root, outside the imported folder. Both serve the folder they are started in on port 5055, so start them from `src`: `cd src && go run ../dev-servers/audiomass-server.go` (it also opens Google Chrome on macOS) or `cd src && python3 ../dev-servers/audiomass-server.py`. Upstream's README step 3 names them without the `../dev-servers/` part; the README is untouched.
- `TOFU.md` (this file) was rewritten to match, then updated for the five files above.

## Licence

- AudioMass itself: MIT, Copyright (c) 2018-present Pantelis Kalogiros. The root `LICENSE` is upstream's, untouched; `src/LICENSE` is a copy so the imported app carries it.
- Bundled libraries keep their own licences, as upstream's `THIRD_PARTY_NOTICES.md` lists them: WaveSurfer.js 2.0.5 with its regions plugin (BSD-3-Clause), libFLAC 1.3.3 (Xiph/New BSD), RNNoise (BSD-3-Clause), lz4-wasm (BSD-2-Clause).
- **Copyleft caveat: `src/lame.js` is LGPL.** It is the LAME MP3 encoder through lamejs, which `THIRD_PARTY_NOTICES.md` lists as LGPL; the file's own embedded notices (from the LAME sources) name the GNU Lesser General Public License, version 2 or later. The end of the file is a small worker wrapper (the `onmessage` handler the page talks to). Tofu ships the file unchanged, as plain readable JavaScript, and the page loads it as a separate Web Worker (`new Worker('lame.js')`, used for MP3 export), so it can be swapped for another build. Keep the file's notices and `THIRD_PARTY_NOTICES.md` with any copy of it.
- Sample audio and images: `src/piano-sample.mp3`, `src/test.mp3` and `src/mp3/multi/*.mp3` are the sample music (the app's welcome dialog calls them the author's own pieces); `src/about/` holds the About page's screenshots and a short video; `src/phone-switch.jpg`, `src/icon.png` and `src/ico.png` are images; `src/fonts/icomoon.*` (`.woff`, `.ttf`, `.svg`) is an icon font made with IcoMoon, the only font the page loads (as `icomoon.woff`). Upstream states no separate licence for any of these (`LICENSE` speaks of "AudioMass original code", and the notices file lists none of them), and Tofu has not checked where they come from. They ship in the copy because the app uses them; reuse outside this app is for the author to say.
- Third-party product screenshots: the About page shows two screenshots of other companies' audio software as design inspiration, `src/about/sonar.jpg` (captioned "Sonar") and `src/about/fruity.png` (captioned "Fruity loops"). Their makers' names and interfaces are theirs.
- Name and links: "AudioMass" is the upstream author's project name. The page's share-card tags in `index.html`, the About page and the app's GitHub link still point to https://audiomass.co and https://github.com/pkalogiros/audiomass, as upstream wrote them; Tofu changed none of that.

## Known limits (upstream's, left as they are)

- Help > Store Offline Version uses the retired AppCache and opens `index-cache.html`, which needs `all.build.js` and `all.css`. Upstream builds those two files but does not commit them, so that page cannot start in this copy. `index-final.html` has the same two missing files; nothing in the app links to it. The AppCache manifest `index-cache.html` names (`audiomass.appcache`) is one of the files removed above: its `manifest` attribute now points at a file that is not there, which changes nothing for a visitor, because AppCache is retired and that page could not start anyway.
- `about.html` asks for `/ico.ico`, which upstream does not ship (only the About page's icon is missing).

## Verification

Checked on 2026-10-23, after the five files above were removed, on a copy of `src/` with the paths Tofu's importer drops removed (`rsync -a --exclude node_modules --exclude dist --exclude build --exclude target --exclude .cache src/ <scratch>/`: 78 files, no `dist` folder), because that is what an imported copy contains. Nothing is installed or built: there is no `package.json`.

- Static lane: Tofu's own Free-plan check, run on the pushed `tofu` branch with root folder `src`, reads it as a finished static site (80 files) and its safety check passes. Run on the branch before the five files were removed, the same check refused it: five files of a type the static lane does not serve.
- Served with `python3 -I -m http.server <port> --bind 127.0.0.1 --directory <copy>`. `curl` of `/` answers HTTP 200, and so do `/vendor/wavesurfer/wavesurfer.js`, `/vendor/wavesurfer/plugin/wavesurfer.regions.js`, `/fonts/icomoon.woff`, `/LICENSE` and `/THIRD_PARTY_NOTICES.md`. `/fonts/icomoon.eot`, `/audiomass.appcache`, `/main.build.css.br` and `/audiomass-server.py` answer 404, as expected, and so does `/dist/wavesurfer.js`, which is what the importer drops.
- Browser check against 127.0.0.1 only: the editor starts, `WaveSurfer` and its regions plugin are defined, and the waveform area (`#pk_av_0`) is there, about 1376 x 735 pixels in the test window. The toolbar icons draw: the page loads `fonts/icomoon.woff` and the browser reports the icon font as loaded. The first-run welcome dialog shows and closes with OK. Console errors: none. Console warnings: none.
- Core action: "here to use a sample" loads the bundled piano sample (122.253 s, stereo, 44.1 kHz) and draws its waveform. Edit > Select All, then Effects > Reverse, replaces the audio with the time-reversed samples: 10,782,714 samples compared, none differing (largest difference 0), at the 3-sample offset AudioMass's own offline render adds. Console errors: none.
- The three Web Workers the app starts for export (`lame.js` for MP3, `flac.js` for FLAC, `wav.js` for WAV) start without an error.
- Server log of that run: every request the browser made was answered 200 or 304, and it asked for none of the removed files. The only 404s are the five deliberate `curl` probes above.
- Import filter: a dry run of Tofu's GitHub import against the pushed `tofu` branch with root folder `src` keeps 78 files and drops 2, the two upstream `src/dist` files that the page no longer loads. No file a page loads is dropped. It lists five references as missing in the pin, all upstream's own dead links described under Known limits (`about.html` to `/ico.ico`; `index-cache.html` and `index-final.html` to `all.build.js` and `all.css`).
- Dev server: `cd src && python3 ../dev-servers/audiomass-server.py` (with its listening address limited to 127.0.0.1 for the test) answers `/`, `/index.html`, `/main.css` and `/vendor/wavesurfer/wavesurfer.js` with HTTP 200. The Go dev server was not run.
- Not tried: exporting a file, recording from a microphone, the MultiTrack mode.
