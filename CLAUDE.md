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
| `/termini/` | Termini d'uso di WorkTracker |
| `/funzionalita/`, `/prezzi/` | Solo rinvii ai nuovi indirizzi sotto `/worktracker/` |
| `404.html` | Pagina di errore, unica con percorsi assoluti (`/assets/...`) |
| `assets/` | `style.css` condiviso, `theme.js`, icone, font in `assets/fonts/` |

Elekit per ora compare solo come scheda "In lavorazione" in home. Quando avrà pagine
proprie, andranno in `/elekit/` sul modello di `/worktracker/`.

## Regole sui contenuti

- Tutto in **italiano**, tono semplice e diretto.
- Nomi delle versioni: **WorkTracker Lite** e **WorkTracker** (mai "WorkTracker Base").
  WorkTracker è "in lavorazione", con **periodo di prova su richiesta** legato all'email.
- **Non usare "gratis", "gratuito/a"** né prezzi: al lancio non ci sono pagamenti.
- Contatto unico: **info@ghedolab.com** (inoltrato da Cloudflare Email Routing).
- Descrivi solo funzioni che esistono davvero nel `main` dell'app: verificale nel codice.

## Informativa privacy

- La versione ufficiale è `privacy/index.html`. Nell'app ne esiste una copia offline
  (`app/app/src/main/assets/privacy_policy.html` nel repository WorkTracker): ogni volta
  che cambi l'informativa, prepara anche il prompt per aggiornare quella copia.
- A ogni modifica: aggiorna "Ultimo aggiornamento" e aggiungi una voce in
  "13. Modifiche a questa informativa" (sezione con `id="modifiche"`).
- Ogni nuovo servizio esterno, permesso Android o dato inviato fuori dal telefono va
  nella tabella della sezione 4 (servizio, dati, quando, finalità e base giuridica),
  nei permessi, nella conservazione e, se è fuori dall'UE, nella sezione trasferimenti.
- Segnala a chi gestisce il progetto cosa va aggiornato in Play Console (Sicurezza dei
  dati, permessi): non lo puoi fare tu.

## Regole tecniche

- HTML statico, nessun build. Percorsi **relativi** in tutte le pagine tranne `404.html`.
- Nessuna risorsa di terze parti: niente Google Fonts, CDN, analytics o cookie
  (l'informativa dichiara che il sito non li usa). I font sono in `assets/fonts/`.
- Il tema chiaro/scuro usa solo `localStorage` (`wt-theme`).
- Ogni pagina ha `title`, `meta description`, `canonical` e tag Open Graph.
  Aggiorna `sitemap.xml` (anche `lastmod`) quando aggiungi o cambi pagine.
- Prima di pubblicare, controlla con Playwright tutte le pagine a 390 px e 1280 px:
  nessuno scorrimento orizzontale e nessun link interno rotto.

## Git

- Lavora su un branch e unisci in `main` solo quando richiesto: GitHub Pages pubblica
  da `main`.
- Messaggi di commit in italiano, con prefisso "Sito:" o "Privacy:".
