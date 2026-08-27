# Teniski klub AS-NS — sajt

Jednostrani sajt kluba. Bez build koraka, bez zavisnosti: fajlovi se
postavljaju na hosting takvi kakvi su.

## Struktura

    index.html        markup svih sekcija (inline stilovi, vidi napomenu)
    404.html          stranica za nepostojece adrese
    css/style.css     globalna pravila: reset, prelazi, stanja linkova, keyframes
    js/main.js        logika: animacije, mobilni raspored, kalendar, FAQ, meni
    js/support.js     runtime koji vezuje js/main.js za markup u index.html
    slike/            fotografije
    robots.txt        dozvole za pretrazivace i AI botove
    sitemap.xml       mapa sajta

## Postavljanje

1. Prekopirati ceo folder na hosting (root domena).
2. U `robots.txt`, `sitemap.xml` i meta tagovima u `index.html` zameniti
   `PROMENI-DOMEN.rs` pravim domenom.
3. Podesiti da server vraca `404.html` za nepostojece adrese.
   Apache: `ErrorDocument 404 /404.html` u `.htaccess`.
   Nginx: `error_page 404 /404.html;`

## Zasto su stilovi inline

Raspored i boje su u `style` atributima, a ne u CSS klasama, da bi se
stranica iscrtala odmah pri ucitavanju, bez cekanja na stylesheet. U
`css/style.css` je samo ono sto inline ne moze: reset, prelazi, `:hover`,
`@keyframes`. Mobilni raspored ne ide kroz media query nego kroz listu
`pravila` u `js/main.js` (jedno mesto za sve mobilne izmene).

## Gde se sta menja

| Izmena | Fajl | Gde |
|---|---|---|
| Tekst sekcije | index.html | komentar sa nazivom sekcije iznad nje |
| Cene | index.html | sekcija `#cene` |
| Pitanja u FAQ | js/main.js | `Component.PITANJA` |
| Kalendar (zauzeti dani, termini) | js/main.js | `renderVals()` |
| Mobilni raspored | js/main.js | lista `pravila` |
| Boja fiksne trake | js/main.js | `primeniNav()` |
| Fotografije | slike/ | zameniti fajl istog imena |
| SEO, Open Graph, JSON-LD | index.html | `<head>` |

## Slike

Velike fotografije su `.webp` (hero 258 KB umesto 3.4 MB), male kvadratne
ostaju `.png` jer su tako manje. Hero se preuzima prioritetno
(`<link rel="preload">`), logotipi imaju zadate dimenzije da se raspored ne
pomera pri ucitavanju.

## Rezervacije

Kalendar u sekciji `#rezervacija` je prikaz, ne pravi sistem rezervacija:
zauzeti dani i termini su upisani u `renderVals()` u `js/main.js`.
Rezervacije se za sada obavljaju telefonom (063 681 739).
