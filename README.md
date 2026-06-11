# Premio Diretto — Landing Page

Landing page premium in italiano per **Premio Diretto** — *"Informazioni semplici. Risposte rapide."*

Raccolta lead tramite modulo a due campi (Nome e Cognome + Numero WhatsApp), con contatto via WhatsApp.

## Stack

- HTML statico in singolo file ([`index.html`](index.html))
- Tailwind CSS (via CDN)
- JavaScript vanilla
- Deploy su Vercel

## ⚙️ Configurazione (2 valori da sostituire)

Apri [`index.html`](index.html) e cerca il blocco **`const CONFIG`** all'inizio della sezione `<script>` (verso il fondo del file):

```js
const CONFIG = {
  WHATSAPP_NUMBER: "393000000000",   // <-- il tuo numero WhatsApp (formato internazionale, senza +)
  GOOGLE_SHEETS_URL: "",             // <-- URL Apps Script (.../exec) dove arrivano i lead
  WHATSAPP_MESSAGE: "Ciao, vorrei ricevere informazioni"
};
```

### 1) Numero WhatsApp
Sostituisci `393000000000` con il tuo numero in **formato internazionale senza `+`, spazi o trattini**
(es. Italia: `393331234567`). Aggiorna automaticamente tutti i pulsanti e link WhatsApp della pagina.

### 2) URL Google Sheets (Apps Script)
Incolla tra le virgolette di `GOOGLE_SHEETS_URL` l'URL della tua Web App di Google Apps Script
(termina con `/exec`). Finché resta vuoto, il modulo funziona in **modalità demo** (mostra solo il
messaggio di successo, senza salvare i dati).

#### Come ottenere l'URL Apps Script
1. Crea un Google Sheet con le colonne: `Data | Nome | WhatsApp | Origine`.
2. `Estensioni → Apps Script` e incolla:
   ```js
   function doPost(e) {
     const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     const data = JSON.parse(e.postData.contents);
     sheet.appendRow([data.data, data.nome, data.whatsapp, data.origine]);
     return ContentService.createTextOutput(JSON.stringify({ ok: true }))
       .setMimeType(ContentService.MimeType.JSON);
   }
   ```
3. `Distribuisci → Nuova distribuzione → App web`, accesso **"Chiunque"**, e copia l'URL `/exec`.
4. Incollalo in `GOOGLE_SHEETS_URL`, salva e ridistribuisci il sito.

## Deploy

Ogni `git push` sul branch `main` aggiorna automaticamente il sito su Vercel.

```bash
git add .
git commit -m "Aggiorna configurazione"
git push
```

© 2026 Premio Diretto. Tutti i diritti riservati.
