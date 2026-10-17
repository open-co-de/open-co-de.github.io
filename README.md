# open-co.de

Quellcode der Website [open-co.de](https://open-co.de), gebaut mit Jekyll und GitHub Pages.

- Keine Themes, kein JavaScript, keine externen Ressourcen, kein Tracking
- Layout: `_layouts/`, Styles: `assets/css/main.css`, Inhalte: `index.html`, `about.md` (Impressum), `datenschutz.md`

Lokale Vorschau:

```sh
docker run --rm -p 4000:4000 -v "$PWD":/srv/jekyll -w /srv/jekyll ruby:3.3 \
  sh -c 'bundle install && bundle exec jekyll serve --host 0.0.0.0'
```
