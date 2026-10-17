# open-co.de – Website

Jekyll-Site auf GitHub Pages (`CNAME` → open-co.de). Gebaut wird von GitHub Pages selbst
(Gem `github-pages`, Jekyll 3.x) – kein eigener Workflow, kein Theme.

## Grundsätze
- Minimalistisch, professionell, deutschsprachig (Sie-Form, Kontaktbereich in Ich-Form).
- **Keine externen Ressourcen** (keine Webfonts, CDNs, Hotlinks), **kein JavaScript**,
  **kein Tracking/Cookies** – die Datenschutzseite (`datenschutz.md`) sagt das zu.
- Markenpalette (`assets/img/src/open-code-palette.svg`):
  `#2b4570` `#4167a6` `#8da9c4` `#a8d0db` `#eef4ed` – als CSS-Variablen in `assets/css/main.css`.
- Dark Mode automatisch über `prefers-color-scheme` (Variablen im `@media`-Block überschreiben).

## Aufbau
| Datei | Zweck |
|---|---|
| `_layouts/default.html` | Grundgerüst: Header (Logo, Nav), Footer (Impressum, Datenschutz), `{% seo %}` |
| `_layouts/page.html` | Textseiten (Titel + `.prose`) |
| `_includes/logo.svg` | Logo („C“) als Inline-SVG, Farbe via CSS (`.logo`) |
| `_includes/icon.html` | Linien-Icons, 24er-Raster, Strich 1.6, `currentColor`. Nutzung: `{% include icon.html name="mail" %}` |
| `assets/css/main.css` | Komplettes Styling, keine Preprocessors |
| `index.html` | Startseite: Hero → Prinzipien-Leiste → 4 Themen → Kontakt |
| `about.md` | Impressum unter `/impressum/` (Redirects von `/about/`) |
| `datenschutz.md` | Datenschutzerklärung (knapper Entwurf – rechtlich prüfen lassen) |
| `404.html` | Fehlerseite |

Verfügbare Icons: `compass users trend scale blocks share leaf mail phone code pin sun arrow-right arrow-down`.
Neue Icons als weiteres `when` in `_includes/icon.html` ergänzen, gleicher Stil (nur Striche, keine Füllung).

Kontaktdaten zentral in `_config.yml` (`email`, `phone`, `github_username`), in Templates über `site.*` verwenden.
Plugins (alle GitHub-Pages-kompatibel): `jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-redirect-from`.

## Lokal bauen / Vorschau
Bevorzugt mit Ruby ≥ 3:
```sh
bundle install && bundle exec jekyll serve
```
Auf dem Mac mit System-Ruby 2.6 (kein Bundler, Gems in ein Wegwerf-Verzeichnis):
```sh
export GEM_HOME=/tmp/jekyll-gems PATH=/tmp/jekyll-gems/bin:$PATH JEKYLL_NO_BUNDLER_REQUIRE=true
gem install -N ffi:1.15.5 i18n:1.14.1 concurrent-ruby:1.2.3 public_suffix:4.0.7 json:2.6.3
gem install -N jekyll:3.10.0 jekyll-seo-tag:2.8.0 jekyll-sitemap:1.4.0 jekyll-redirect-from:0.16.0
BUNDLE_GEMFILE=/nonexistent jekyll build -d /tmp/site-preview
python3 -m http.server 8765 -d /tmp/site-preview
```
Screenshots (Headless Chrome; Mindestbreite ist ~500 px, schmaler wird abgeschnitten):
```sh
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars \
  --blink-settings=preferredColorScheme=1 --window-size=1360,2300 --screenshot=desktop-light.png http://localhost:8765/
```
`preferredColorScheme=0` = dunkel, `1` = hell.

## Screenshots für PRs
Liegen auf dem verwaisten Branch `pr-1-screenshots` (nicht im Site-Branch) und werden per
`raw.githubusercontent.com/<repo>/<commit-sha>/<datei>.png` im PR-Kommentar eingebettet.
