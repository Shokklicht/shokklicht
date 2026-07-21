# PBI Tuning — Tiedostorakenne

## Rakenne

```
tuning-site/
├── index.html          ← Pääsivu (navigaatio + runko)
├── models/
│   ├── _template.html  ← Pohja uusille malleille
│   ├── nissan-100a.html ← Esimerkki täytetystä mallista
│   ├── nissan-120a.html
│   ├── aasc16.html
│   └── ... (yksi tiedosto per automalli)
```

## Miten toimii

1. **index.html** sisältää kaiken navigaation ja sivupohjan.
2. Kun käyttäjä klikkaa automallia, `loadModel()` funktio tekee
   `fetch()`-kutsun ko. mallin HTML-tiedostoon.
3. Haettu HTML injektoidaan `#spec-body`-elementtiin.
4. Jokainen mallitiedosto on pelkkä HTML-fragmentti (ei `<html>`/`<head>`).

## Uuden mallin lisääminen

1. Kopioi `models/_template.html` → `models/uusimalli.html`
2. Täytä `<table class="spec-table">` -rakenteet oikeilla tiedoilla:

```html
<div class="spec-section">
  <div class="spec-section-title">Osion nimi</div>
  <table class="spec-table">
    <tr><td>Kenttä</td><td>Arvo</td></tr>
    ...
  </table>
</div>
```

3. Lisää linkki `index.html`-tiedoston navigaatioon:

```html
<button class="model-link" onclick="loadModel('merkki','Mallin nimi','models/uusimalli.html')">
  Mallin nimi
</button>
```

## Hosting

Koska käytetään `fetch()`:iä, sivusto täytyy ajaa web-palvelimelta.
Ei toimi suoraan tiedostojärjestelmästä (file://).

Vaihtoehdot:
- `python3 -m http.server 8080` (kehitys)
- Nginx / Apache (tuotanto)
- GitHub Pages (ilmainen hosting)
