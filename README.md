# Teniski klub AS-NS — sajt

Jednostrani sajt kluba. Bez build koraka, bez zavisnosti: fajlovi se
postavljaju na hosting takvi kakvi su.

## Struktura

    index.html        markup svih sekcija (inline stilovi, vidi napomenu)
    404.html          stranica za nepostojece adrese
    css/style.css     globalna pravila: reset, prelazi, stanja linkova, keyframes
    js/support.js     runtime; logika sajta je ugradjena na dnu index.html
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
`pravila` u skripti na dnu `index.html` (jedno mesto za sve mobilne izmene).

Logika ne moze u spoljni fajl: runtime u `js/support.js` cita `<script
data-dc-script>` iz same stranice.

## Gde se sta menja

| Izmena | Fajl | Gde |
|---|---|---|
| Tekst sekcije | index.html | komentar sa nazivom sekcije iznad nje |
| Cene | index.html | sekcija `#cene` |
| Pitanja u FAQ | index.html | `Component.PITANJA` u skripti na dnu |
| Kalendar (zauzeti dani, termini) | index.html | `renderVals()` u skripti na dnu |
| Mobilni raspored | index.html | lista `pravila` u skripti na dnu |
| Boja fiksne trake | index.html | `primeniNav()` u skripti na dnu |
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
