# Scout Panchina: versione web con "Accedi con Google"

Chi la usa non deve copiare fogli né pubblicare script: apre il link, accede con il proprio account Google e l'app crea da sola il foglio **"Scout Panchina"** nel suo Drive.
Queste operazioni le fai **tu una sola volta**, per tutti gli utenti.

## 1. Google Cloud (console.cloud.google.com)
1. Crea un **nuovo progetto** (es. "Scout Panchina").
2. **API e servizi → Libreria**: abilita **Google Sheets API** e **Google Drive API**.
3. **Schermata consenso OAuth** (o "Google Auth Platform"):
   - Tipo utente: **Esterno**.
   - Nome app, email di assistenza, email di contatto.
   - Ambiti: aggiungi solo **`.../auth/drive.file`** (permette all'app di vedere solo i file che crea lei).
   - Stato di pubblicazione: **In produzione** (con "In test" possono entrare solo gli utenti che aggiungi a mano, e l'accesso scade dopo pochi giorni).
4. **Credenziali → Crea credenziali → ID client OAuth → Applicazione web**.
   - **Origini JavaScript autorizzate**: l'indirizzo dove pubblicherai la pagina (passo 3), per esempio `https://tuonome.github.io`.
5. Copia l'**ID client** (finisce con `.apps.googleusercontent.com`).

6. Nello stesso ID client, sezione **URI di reindirizzamento autorizzati**: aggiungi l'indirizzo completo della pagina **con la barra finale**, es. `https://mazzugoro.github.io/nomerepo/`. Serve se il browser blocca il popup di accesso: in quel caso la pagina usa l'accesso a tutta pagina e torna a questo indirizzo.

## 2. Inserisci l'ID client nella pagina
Apri `index.html` con un editor di testo, cerca la riga
`const CLIENT_ID="INSERISCI_QUI_IL_CLIENT_ID.apps.googleusercontent.com";`
e sostituisci il testo tra virgolette con il tuo ID client.

## 3. Pubblica la pagina (serve un indirizzo https)
Una delle due:
- **GitHub Pages**: crea un repository, carica `index.html`, poi *Settings → Pages → Deploy from a branch*. L'indirizzo sarà `https://tuonome.github.io/nomerepo/`.
- **Netlify Drop** (app.netlify.com/drop): trascini la cartella con `index.html` e ottieni subito un indirizzo.

Poi torna al passo 1.4 e inserisci l'indirizzo (solo dominio, senza percorso) tra le origini autorizzate.

## 4. Prova sul telefono
1. Apri l'indirizzo con Chrome.
2. Al primo avvio: **Accedi con Google**, poi squadra, categoria e atlete.
3. Menu ⋮ → **Aggiungi a schermata Home** (o **Installa app**).
4. Fai una partita finta, premi **Salva partita e invia** e controlla nel tuo Drive il foglio **Scout Panchina**.

## 3 bis. Uso offline (file da caricare)
Nel repository GitHub, accanto a `index.html`, carica anche: `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` (**Add file → Upload files**, nella cartella principale).
- Apri il link **una volta con la rete**: la pagina viene salvata nel telefono. Dopo si apre anche senza connessione.
- Per installarla come app: Chrome ⋮ → **Installa app** (o **Aggiungi a schermata Home**).
- Offline funzionano scout, formazione e statistiche. **Accedi con Google** e **Salva partita e invia** richiedono la rete: i dati restano sul telefono e li invii quando torni online.
- **Aggiornare la pagina:** quando cambi `index.html`, apri `sw.js` e cambia `VERSION` (es. `scout-v8-2`), così i telefoni scaricano la nuova versione alla prima apertura con la rete.

## Da sapere
- Il pulsante **G** in alto ricollega l'account se l'accesso scade (dopo circa un'ora). Premendo **Salva partita e invia**, Google può chiedere di nuovo la conferma.
- L'app vede solo il foglio che ha creato lei. I fogli fatti con la versione Apps Script non vengono letti: per i vecchi dati servirebbe un'importazione.
- Il PDF viene scaricato dal browser.
- Dopo questa tappa, la stessa pagina si può inserire in un'app Android (tappa successiva).
