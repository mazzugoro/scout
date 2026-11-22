# Scout Panchina: guida completa (versione web)

Questa guida ha due parti:
- **Parte A: installazione** (la fa chi pubblica l'app, una sola volta).
- **Parte B: uso** (per chi fa lo scout).

---

# PARTE A: installazione (una volta sola)

## A1. Google Cloud (console.cloud.google.com)
1. Crea un **nuovo progetto** (es. "Scout Panchina").
2. **API e servizi → Libreria**: abilita **Google Sheets API** e **Google Drive API**.
3. **Schermata consenso OAuth** (o "Google Auth Platform"):
   - Tipo utente: **Esterno**; nome app, email di assistenza e di contatto.
   - Ambiti: solo **`.../auth/drive.file`** (l'app vede solo i file che crea lei).
   - Stato: **In produzione** (con "In test" entrano solo gli utenti aggiunti a mano e l'accesso scade dopo pochi giorni).
4. **Credenziali → Crea credenziali → ID client OAuth → Applicazione web**. Copia l'**ID client** (finisce con `.apps.googleusercontent.com`).
5. In quell'ID client, dopo aver pubblicato la pagina (A3), inserisci:
   - **Origini JavaScript autorizzate**: solo dominio, senza percorso né barra finale. Esempio: `https://tuonome.github.io`
   - **URI di reindirizzamento autorizzati**: indirizzo completo della pagina **con la barra finale**. Esempio: `https://tuonome.github.io/nomerepo/`

## A2. Inserisci l'ID client nella pagina
Apri `index.html` con un editor di testo, cerca la riga
`const CLIENT_ID="INSERISCI_QUI_IL_CLIENT_ID.apps.googleusercontent.com";`
e sostituisci il testo tra virgolette con il tuo ID client. **Ripeti questo passaggio a ogni nuovo `index.html` che ricevi.**

## A3. Pubblica la pagina (serve un indirizzo https)
Una delle due:
- **GitHub Pages**: crea un repository **pubblico**, carica i file (elenco sotto), poi *Settings → Pages → Deploy from a branch → main → / (root) → Save*. L'indirizzo è `https://tuonome.github.io/nomerepo/` (lo vedi in *Settings → Pages*).
- **Netlify Drop** (app.netlify.com/drop): trascini la cartella e ottieni subito un indirizzo.

**File da caricare, tutti nella cartella principale:**
`index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`

## A4. Aggiornare l'app
1. Sostituisci `index.html` (con il tuo `CLIENT_ID`) e `sw.js` nel repository (*Add file → Upload files → Commit changes*).
2. Controlla la scritta "Versione pagina" nella finestra iniziale: deve corrispondere alla nuova versione.
3. Chi usa l'app riceve l'aggiornamento alla prima apertura con la rete; se vede una versione vecchia deve chiuderla del tutto e riaprirla una seconda volta.
4. Aggiorna le app **fuori dalle partite**.

## A5. Costi
Google Cloud (Sheets e Drive API): nessun costo per questo uso. GitHub Pages e Netlify: gratuiti. Solo la pubblicazione su Google Play, se un giorno servirà, ha una quota una tantum.

---

# PARTE B: uso dell'app

## B1. Installare e collegare Google
1. Apri il link con **Chrome** (non da un'altra app) e tocca ⋮ → **Installa app** (o *Aggiungi a schermata Home*). Apri il link **una volta con la rete**: dopo si apre anche senza connessione.
2. Alla prima apertura puoi **Accedere con Google** subito, oppure premere **Inizia** e provare l'app senza account: Google si collega dopo (tasto **G** in alto, o in *Partita*).
3. Inserisci **squadra** e **categoria**, poi le **atlete** (almeno 6). Questo passaggio compare **solo la prima volta**: dopo, le atlete si gestiscono da **Formazione**.
4. Con Google collegato, l'app crea da sola il foglio **"Scout Panchina"** nel tuo Drive.

**Il tasto G in alto**
- Per sapere **con quale account** sei collegata: l'email compare in *Partita* (riga "Google"), nella legenda **?** e in *Squadre / società*. Se colleghi un account diverso, l'app avvisa e usa i fogli del nuovo account.
- **G ✓** = collegato · **G !** = scaduto, toccalo per rinnovare · **G** = non collegato.
- Il collegamento dura circa un'ora e l'app lo rinnova da sola in background. Se si scollega (ad esempio dopo molti giorni senza usarla), tocca G e scegli l'account.
- Senza collegamento puoi comunque fare scout: i dati restano sul telefono e li invii dopo.

## B2. Fare lo scout
1. In **Partita** scrivi avversario, data, casa/fuori, categoria.
2. In **Formazione** scegli le convocate (massimo 14, con 6 + libero in campo), imposta dove sta il palleggiatore (P1–P6) e tocca le zone per scegliere le atlete.
3. Durante la partita: **tocca l'atleta → fondamentale → esito**. Nella finestra compaiono le azioni decisive; i tasti piccoli sotto l'atleta registrano le azioni non decisive (Ric ✓, Dif ✓, Att dif, Bat ✓).
4. **Verde** = punto fatto, **rosso** = punto perso. **PASTE** = battuta sotto rete (errore di battuta). **Errore / Attacco Avversario** hanno i loro pulsanti.
5. **Annulla** cancella l'ultima azione. I set vanno da 1 a 5 e il punteggio si calcola dalle azioni.
6. Il tasto **?** apre la legenda con le spiegazioni; il tasto **⚙** sceglie quali **fondamentali ed esiti** mostrare durante lo scout.

## B3. Foto delle atlete
In **Formazione**, apri la scheda dell'atleta e scegli la **Foto** (galleria o fotocamera). Compare sopra il numero e il nome nello scout. La foto viene salvata anche nel foglio (colonna **Foto** di `Atleti`), quindi si ritrova su un altro telefono dopo **Importa atlete dal foglio Google**. Non modificare a mano la colonna Foto.

## B4. Più categorie
- In **Partita → Categoria**: scegli la categoria o aggiungine una con **＋ Aggiungi**.
- **✎ Rinomina o elimina categorie**: rinominando con il nome di un'altra, le due si uniscono. Una categoria con partite non si elimina. Per aggiornare anche il foglio, collega Google prima di rinominare.
- Ogni atleta può giocare in **più categorie** (si spunta nella sua scheda; nessuna spunta = tutte).
- In **Statistiche** i filtri in alto mostrano i dati di una categoria o di tutte.

## B5. Più squadre o società (stesso telefono e stesso account)
- **Partita → 🏐 Squadre / società**: elenco delle squadre, con **Apri**, **Elimina** e **＋ Crea e apri**.
- Ogni squadra ha i propri dati e il proprio foglio nel Drive ("Scout Panchina - Nome squadra"). Cambiare squadra riavvia l'app, senza perdere nulla.
- **Elimina** toglie la squadra solo dal telefono; il foglio resta nel Drive.
- Su un **telefono nuovo**: accedi con lo stesso account. L'app cerca da sola le altre squadre nel Drive (o usa **🔍 Cerca altre squadre nel mio Google Drive**). Apri ogni squadra, poi **Importa atlete dal foglio Google** e **Richiama altra partita** per riprendere i dati.

## B6. Atlete: aggiungere, modificare, eliminare
- Da **Formazione**. Eliminare un'atleta la toglie anche dalla scheda `Atleti` del foglio (con Google collegato; altrimenti la cancellazione parte al prossimo invio).
- Un'atleta con azioni nella partita aperta non si elimina: togli la convocazione. Eliminando un'atleta con partite passate, nelle statistiche vecchie comparirà "?" al posto del nome.
- **Atlete scritte a mano nel foglio**: nella scheda `Atleti` compila `Nome`, `Numero`, `Ruolo` (Palleggiatore, Opposto, Banda, Centrale, Libero, bastano le iniziali), `Convocata` (Sì/No) e `Categorie` (es. `U16, U18`; vuoto = tutte). Poi nell'app: **Importa atlete dal foglio Google**.

## B7. Correggere gli errori di inserimento
- **Partita aperta**: *Esporta/Azioni → ✎ Correggi o elimina azioni*. ✎ modifica atleta, fondamentale, esito e set; 🗑 elimina (conferma con "Sicuro?").
- **Partita vecchia**: prima richiamala da **Partita → Richiama altra partita** (dall'archivio), poi correggi.
- Per portare le correzioni nel foglio premi **Salva partita e invia**: le righe eliminate o modificate vengono tolte e quelle corrette riscritte.

## B8. Salvare, inviare, stampare
- Il salvataggio sul telefono è **automatico**.
- **Salva partita e invia**: manda al foglio azioni, riga della partita e atlete. Senza rete o senza collegamento, la partita resta sul telefono; invia quando puoi.
- **Stampa**: PDF di una pagina (A4 orizzontale) con tabella per atleta e risultati per set. Scegli le colonne da stampare in *Esporta* → **⚙ Colonne da stampare nel PDF**.
- **Statistiche**: modalità **Globale** (partita per partita) o **Singola partita** (set per set). Per default contano solo le azioni decisive; l'indice è (punti − errori) ÷ (punti + errori).
- Il **backup in testo** (in *Esporta*) serve a recuperare i dati se qualcosa va storto.

## B9. Schermo
L'app è pensata per l'uso su **telefono, in verticale**. I tasti **Scout, Partita, Formazione, Statistiche, Stampa, Esporta** sono **fissi in basso** e restano visibili anche con una finestra aperta; **Scout** chiude le finestre e riporta alla schermata di gioco.
Telefono e altro dispositivo con lo stesso account condividono i dati tramite il foglio Google: **Salva partita e invia** su uno, poi **Importa atlete** e **Richiama altra partita** sull'altro.

## B10. Se qualcosa non funziona
| Problema | Cosa fare |
|---|---|
| **G !** o "Google non collegato" | Tocca **G** e scegli l'account. I dati sul telefono non si perdono. |
| La pagina di accesso non si apre | Apri l'app dal browser Chrome e consenti i popup per il sito. |
| Dopo l'accesso la pagina sembra "desktop" | Chrome ⋮ → togli la spunta a **Sito desktop**; chiudi e riapri l'app. |
| Mancano i tasti in basso | Chiudi del tutto l'app e riaprila. |
| Versione vecchia dopo un aggiornamento | Chiudi l'app, riaprila con la rete, poi chiudila e riaprila ancora. |
| Un'atleta o una squadra non compare su un altro telefono | Collega Google, poi usa **Importa atlete** e **Cerca altre squadre**. |
| Errore 403 `access_denied` all'accesso | Il progetto Google Cloud è ancora "In test": va portato **In produzione** (A1.3). |
| `origin_mismatch` o `redirect_uri_mismatch` | Origine o URI di reindirizzamento non coincidono con l'indirizzo della pagina (A1.5). |
