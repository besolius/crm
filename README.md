# Flipbook – Catalog de produse 2024/2025

Versiunea online a catalogului PDF (44 de pagini), cu efect de întoarcere a paginii. Pe calculator se vede ca o carte deschisă, iar pe telefon apare câte o pagină și se răsfoiește cu swipe.

## Ce conține folderul

```
flipbook/
├── index.html      ← pagina flipbook-ului (asta se deschide)
├── pages/          ← cele 44 de pagini la rezoluție mare (p-01.jpg … p-44.jpg)
├── thumbs/         ← miniaturile pentru meniul „Cuprins”
└── README.md       ← fișierul acesta
```

Există și o variantă într-un singur fișier: **Catalog-produse-2024-2025-flipbook.html** (~11 MB). În ea, toate imaginile sunt incluse în fișier, așa că se poate deschide direct de pe calculator sau telefon, chiar fără internet.

| Variantă | Când o folosești |
|---|---|
| Folderul `flipbook/` (index.html + imagini) | **Pentru găzduire pe un site.** Se încarcă mai repede, pentru că imaginile se descarcă pe rând, pe măsură ce se răsfoiește. |
| Fișierul unic `.html` | Pentru trimis direct sau deschis local, fără site. |

Folderul are nevoie de internet, pentru că biblioteca de răsfoire (`page-flip`) și fontul se încarcă de pe CDN. Fișierul unic nu are nevoie.

---

## Găzduire – variante gratuite

### Varianta 1: Netlify Drop (cea mai simplă, ~2 minute)

1. Intră pe **https://app.netlify.com/drop**.
2. Trage **tot folderul** `flipbook/` (nu doar `index.html`) în zona „Drag and drop your site output folder here”.
3. După câteva secunde primești un link de forma `https://nume-aleator.netlify.app`.
4. Ca linkul să rămână permanent, fă-ți un cont gratuit (sau intră cu Google/GitHub) și revendică site-ul. Fără cont, site-ul este șters după scurt timp.
5. Opțional: **Site configuration → Change site name** și pui un nume ușor de ținut minte, de exemplu `catalog-forever-cinca` → `https://catalog-forever-cinca.netlify.app`.

**Actualizare:** în Netlify intri pe site → **Deploys** și tragi din nou folderul modificat. Linkul rămâne același.

### Varianta 2: GitHub Pages

1. Creează un cont pe https://github.com, apoi un repository nou și public (ex. `catalog`).
2. **Add file → Upload files** și încarci tot conținutul folderului: `index.html`, `pages/`, `thumbs/`.
3. **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.
4. După 1–2 minute, site-ul e disponibil la `https://utilizator.github.io/catalog/`.

### Varianta 3: Site propriu (cPanel / hosting / WordPress)

1. Prin **File Manager** sau FTP, creează un folder în `public_html`, de exemplu `catalog`.
2. Urcă în el `index.html`, `pages/` și `thumbs/`, păstrând structura.
3. Linkul devine `https://site-ul-tau.ro/catalog/`.

**WordPress:** nu lipi codul într-o pagină WordPress, pentru că editorul îl strică. Urcă folderul prin File Manager ca mai sus, apoi pune în meniu sau în articole un link către `/catalog/`.

**Atenție:** un fișier HTML se încarcă singur ca pagină doar dacă se numește `index.html`. Dacă urci fișierul unic, redenumește-l `index.html` sau accesează-l cu numele complet în link.

---

## Link direct către o pagină

Adaugă `#p` + numărul paginii la finalul linkului:

| Link | Se deschide la |
|---|---|
| `https://…/catalog/#p6` | Băuturi și geluri |
| `https://…/catalog/#p12` | Produse apicole |
| `https://…/catalog/#p14` | Suplimente alimentare |
| `https://…/catalog/#p24` | Controlul greutății |
| `https://…/catalog/#p28` | Îngrijirea pielii |
| `https://…/catalog/#p36` | Îngrijire personală |
| `https://…/catalog/#p42` | Oportunitate Forever |

Pe măsură ce cititorul răsfoiește, linkul din bara browserului se actualizează singur, așa că se poate copia direct de acolo.

## Cum se folosește

- **Răsfoire:** trage de colțul paginii, glisează pe telefon, apasă săgețile de pe ecran sau folosește tastele ← → de pe tastatură.
- **Cuprins** (butonul galben): lista secțiunilor și miniaturile tuturor paginilor.
- **Pagina 3** (cuprinsul catalogului): titlurile secțiunilor se pot apăsa și duc direct la secțiune.
- **Mărește:** deschide pagina la rezoluție mare. Pe telefon mărești cu două degete, iar pe calculator cu dublu-click sau cu butoanele +/−.
- **Ecran complet:** butonul din dreapta jos (doar pe calculator).

---

## Actualizare pentru un catalog nou

1. Transformă PDF-ul nou în imagini JPG, câte una pe pagină, cu lățimea în jur de 1000 px, numite `p-01.jpg`, `p-02.jpg` … Poți folosi de exemplu https://www.ilovepdf.com/pdf_to_jpg.
2. Înlocuiește imaginile din `pages/`. Pentru `thumbs/` folosește aceleași imagini micșorate la ~220 px lățime.
3. Dacă se schimbă numărul de pagini sau cuprinsul, deschide `index.html` într-un editor de text (Notepad, VS Code) și modifică la începutul scriptului:
   - `const N=44` → numărul nou de pagini;
   - `const SECTIONS=[[4,"Mesajul lui …"],[6,"Băuturi și geluri"], …]` → pagina și numele fiecărei secțiuni;
   - `const HOTS=[…]` → zonele pe care se poate apăsa pe pagina de cuprins. Dacă noua pagină de cuprins arată altfel, șterge conținutul dintre paranteze: `const HOTS=[];`
   - Dacă imaginile noi au alt raport lățime/înălțime, modifică și `RATIO=991/1406`.
4. Urcă din nou folderul (vezi „Actualizare” la Netlify).

## Probleme frecvente

| Problemă | Soluție |
|---|---|
| Pagina e goală sau paginile nu apar | Ai urcat doar `index.html`. Trebuie urcate și folderele `pages/` și `thumbs/`, cu aceleași nume. |
| Paginile apar una sub alta, fără efect de răsfoire | Scriptul de răsfoire nu s-a putut încărca (internet slab sau blocat). Catalogul rămâne lizibil. Reîncarcă pagina. |
| Fișierul unic nu se deschide bine pe iPhone | Pe telefoane e mai sigur să trimiți linkul site-ului găzduit decât fișierul de 11 MB. |
| Imaginile nu se actualizează după ce le-am schimbat | Browserul păstrează versiunea veche. Reîncarcă forțat (Ctrl+F5) sau deschide într-o fereastră privată. |

## Detalii tehnice

- Efectul de răsfoire: [StPageFlip](https://github.com/Nodlik/StPageFlip) (`page-flip` 2.0.7, licență MIT), încărcat de pe `cdn.jsdelivr.net`.
- Font: Figtree (Google Fonts). Dacă nu se încarcă, se folosește fontul sistemului.
- Pagini: JPG 991×1406 px (~170 dpi), în medie ~230 KB fiecare, ~10 MB în total. Se încarcă doar paginile din jurul celei deschise.
- Fără server, bază de date, cookie-uri sau urmărire. Sunt doar fișiere statice.
