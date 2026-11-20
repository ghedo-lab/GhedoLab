# GhedoLab — istruzioni per Claude

Questo repository è il sito **ghedolab.com** (GitHub Pages, dominio in `CNAME`): la
home di GhedoLab, le pagine dei prodotti, l'informativa privacy e i termini d'uso.

## Ambito: solo questo repository

- Le sessioni che lavorano qui modificano **solo** il repository GhedoLab.
- **Mai** commit, push, branch o merge nei repository delle app (`ghedo-lab/worktracker`,
  `ghedo-lab/elekit` e le app future). Quei repository si possono solo **leggere**
  (fetch, log, diff, lettura del codice) per tenere il sito allineato all'app.
- Se serve una modifica in un'app, scrivi un **prompt pronto da incollare** nella chat
  dedicata a quel repository: cosa cambiare e perché, file coinvolti, testo esatto da
  usare se c'è, come verificarlo. Chi gestisce il progetto lo copia nella chat dell'app.

## Struttura del sito

| Percorso | Contenuto |
|---|---|
| `/` (`index.html`) | Home di GhedoLab: prodotti, chi siamo, contatti |
| `/worktracker/` | Home, `funzionalita/` e `prezzi/` (titolo "Versioni") di WorkTracker |
| `/privacy/` | Informativa privacy di WorkTracker. **Indirizzo fisso**: lo apre l'app |
| `/en/privacy/` | Traduzione inglese dell'informativa |
| `/elekit/` | Pagina di Elekit con lista d'attesa |
| `/termini/` | Termini d'uso di WorkTracker |
| `/funzionalita/`, `/prezzi/` | Solo rinvii ai nuovi indirizzi sotto `/worktracker/` |
| `404.html` | Pagina di errore, unica con percorsi assoluti (`/assets/...`) |
| `assets/` | `style.css` condiviso, `theme.js`, icone, font in `assets/fonts/` |

Elekit è "in lavorazione": scheda in home e pagina `/elekit/`. La sua informativa
(`/elekit/privacy/`) si pubblica solo dopo la rilettura di Nicholas.

## Logo e immagini

**Logo GhedoLab** (bozza del 20/11/2026, fonte `brand/ghedolab/` nel repository WorkTracker,
con un LEGGIMI). Quando arriva il definitivo si sostituiscono i file con lo stesso nome.
Regola di Nicholas: il logo con la scritta "GhedoLab" solo dove serve il nome (immagine
Open Graph); altrove solo il simbolo.

| File in `assets/ghedolab/` | Dove compare |
|---|---|
| `logo.png` (simbolo, 256 px) | intestazione di home, Termini e 404; logo grande nella home; piè di pagina di tutte le pagine |
| `favicon-32.png`, `favicon-48.png`, `favicon-192.png`, `apple-touch-icon.png`, `icon-512.png` | icone della scheda di home, Termini e 404 |
| `og-image.png` (1200×630, con la scritta) | `og:image` di tutte le pagine |

**Elekit**: `assets/elekit/` con logo e icone ricavati da `logo_elekit.png` del repository
Elekit (pagina Elekit e scheda in home).

**WorkTracker**: le pagine `/worktracker/` e `/privacy/` usano le icone dell'app in `assets/`
(`favicon.svg`, `logo-mark.svg`, ...). Le schermate in `worktracker/screenshot/` (WebP 540 px)
vengono da `screenshots/play-store/` del repository WorkTracker: aggiornarle quando cambiano.

## Regole sui contenuti

- Tutto in **italiano**, tono semplice e diretto.
- Nomi delle versioni: **WorkTracker Lite** e **WorkTracker** (mai "WorkTracker Base").
  WorkTracker è "in lavorazione", con **periodo di prova su richiesta** legato all'email.
- **Non usare "gratis", "gratuito/a"** né prezzi: al lancio non ci sono pagamenti.
- Contatto unico: **info@ghedolab.com** (inoltrato da Cloudflare Email Routing).
- Descrivi solo funzioni che esistono davvero nel `main` dell'app: verificale nel codice.

## Informativa privacy

- La versione ufficiale è `privacy/index.html`. La traduzione inglese è `en/privacy/index.html`,
  copiata da `privacy_policy_en.html` dell'app (àncora `#account-deletion`): aggiornale insieme. Nell'app ne esiste una copia offline
  (`app/app/src/main/assets/privacy_policy.html` nel repository WorkTracker): ogni volta
  che cambi l'informativa, prepara anche il prompt per aggiornare quella copia.
- A ogni modifica: aggiorna "Ultimo aggiornamento" e aggiungi una voce in
  "13. Modifiche a questa informativa" (sezione con `id="modifiche"`).
- Ogni nuovo servizio esterno, permesso Android o dato inviato fuori dal telefono va
  nella tabella della sezione 4 (servizio, dati, quando, finalità e base giuridica),
  nei permessi, nella conservazione e, se è fuori dall'UE, nella sezione trasferimenti.
- Segnala a chi gestisce il progetto cosa va aggiornato in Play Console (Sicurezza dei
  dati, permessi): non lo puoi fare tu.

## Sicurezza dei dati di Play Console

- `play-console/worktracker-data-safety.csv` è il modulo "Sicurezza dei dati" di
  WorkTracker nel formato di esportazione/importazione di Play Console (non pubblicato
  sul sito: escluso in `_config.yml`).
- Quando una modifica all'app cambia i dati raccolti (nuovo servizio, nuovo dato inviato
  fuori dal telefono, nuova finalità), aggiorna questo file insieme all'informativa e
  invialo a chi gestisce il progetto, che lo importa in Play Console.
- Mantieni il formato identico all'esportazione: stesse righe e colonne, cambia solo la
  colonna "Response value", fine riga CRLF, nessun a capo finale.
- Regole usate: i fornitori di servizi (Sentry, servizio licenze, Google Apps Script,
  Resend) non sono "condivisione"; i dati trattati solo sul telefono (posizione,
  calendario) non si dichiarano; il backup su Google Drive si dichiara come raccolto e
  facoltativo; le ricerche di indirizzi (Photon e servizio di indirizzi di Android) sono
  "Cronologia delle ricerche in-app"; OpenStreetMap (mappe e Overpass) riceve solo IP e
  area, nessun tipo di dato in più.
- Fonte del CSV dalla 1.0.15: `legal/worktracker-data-safety.csv` nel `main` di WorkTracker;
  qui se ne tiene una copia identica byte per byte.

## Regole tecniche

- **Non rimuovere** il tag `<meta name="google-site-verification" ...>` nell'intestazione di
  `index.html` e `worktracker/index.html`: verifica la proprietà di ghedolab.com su Google
  Search Console (verifica del marchio OAuth per Google Drive). Se sparisce, Google revoca la verifica.

- HTML statico, nessun build. Percorsi **relativi** in tutte le pagine tranne `404.html`.
- Nessuna risorsa di terze parti: niente Google Fonts, CDN, analytics o cookie
  (l'informativa dichiara che il sito non li usa). I font sono in `assets/fonts/`.
- Il tema chiaro/scuro usa solo `localStorage` (`wt-theme`).
- Ogni pagina ha `title`, `meta description`, `canonical` e tag Open Graph.
  Aggiorna `sitemap.xml` (anche `lastmod`) quando aggiungi o cambi pagine.
- Prima di pubblicare, controlla con Playwright tutte le pagine a 390 px e 1280 px:
  nessuno scorrimento orizzontale e nessun link interno rotto.

## Git

- Lavora su un branch. **Al termine delle modifiche unisci nel `main`** (GitHub Pages
  pubblica da `main`, quindi la modifica va online subito), poi **elimina gli altri branch
  di lavoro di questo repository** (regola confermata da Nicholas il 3 novembre 2026).
- Prima di eliminare, elenca i branch con `git branch -r --merged origin/main`: elimina
  solo quelli già uniti. Un branch con commit non uniti non si elimina: segnalalo.
- Mai force push su `main`: solo avanzamento diretto (fast-forward) o merge.
- La regola vale solo per GhedoLab: mai toccare i branch di WorkTracker, Elekit o altre app.
- Messaggi di commit in italiano, con prefisso "Sito:", "Privacy:" o "Repo:".
