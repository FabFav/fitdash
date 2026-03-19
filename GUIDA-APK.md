# 📱 FitDash — Guida per generare l'APK Android

## Struttura file da caricare su GitHub

```
fitdash/
├── index.html        ← rinomina google-fit-dashboard.html → index.html
├── manifest.json
├── sw.js
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

---

## STEP 1 — Pubblica su GitHub Pages (gratuito)

1. Vai su [github.com](https://github.com) → accedi o registrati
2. Clicca **"+"** → **New repository**
   - Nome: `fitdash` (tutto minuscolo)
   - Visibilità: **Public**
   - Clicca **Create repository**
3. Carica tutti i file (trascina nella pagina o usa "uploading an existing file"):
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - Cartella `icons/` con i due file PNG
4. Vai su **Settings** → **Pages**
   - Source: **Deploy from a branch**
   - Branch: `main` / `/(root)`
   - Clicca **Save**
5. Dopo 1-2 minuti il tuo sito sarà live su:
   **`https://TUO-USERNAME.github.io/fitdash/`**

---

## STEP 2 — Aggiorna il Client ID Google Cloud

Questo passaggio è **fondamentale**: il nuovo dominio deve essere autorizzato.

1. Vai su [console.cloud.google.com](https://console.cloud.google.com)
2. **API e servizi → Credenziali**
3. Clicca sul tuo Client ID OAuth
4. In **Origini JavaScript autorizzate** aggiungi:
   ```
   https://TUO-USERNAME.github.io
   ```
5. In **URI di reindirizzamento autorizzati** aggiungi:
   ```
   https://TUO-USERNAME.github.io/fitdash/
   ```
6. Clicca **Salva**

> ⚠️ Aspetta 5-10 minuti prima di procedere (propagazione Google)

---

## STEP 3 — Verifica che la PWA funzioni

1. Apri `https://TUO-USERNAME.github.io/fitdash/` su Chrome Android
2. Prova ad effettuare il login con il tuo account Google
3. Se funziona, Chrome mostrerà un banner "Aggiungi a schermata Home"
4. Se qualcosa non va, apri **DevTools → Application → Manifest** per debug

---

## STEP 4 — Genera l'APK con PWABuilder

1. Vai su **[pwabuilder.com](https://www.pwabuilder.com)**
2. Inserisci l'URL della tua PWA:
   ```
   https://TUO-USERNAME.github.io/fitdash/
   ```
3. Clicca **Start** → PWABuilder analizza la PWA
4. Quando appare il punteggio (score), clicca **Package for stores**
5. Seleziona **Android**
6. Nelle opzioni Android scegli:
   - Package ID: `com.tuonome.fitdash`
   - App version: `1`
   - Signing: **"Generate a new signing key"** (per installazione diretta)
7. Clicca **Download** → scarichi uno ZIP con:
   - `fitdash.apk` ← quello da installare
   - `signing.keystore` ← conservalo per aggiornamenti futuri

---

## STEP 5 — Installa l'APK su Android

1. **Sul tuo telefono Android**:
   - Impostazioni → Sicurezza → abilita **"Installa app da origini sconosciute"**
     (oppure: Impostazioni → App → Chrome → "Installa app sconosciute")
2. Copia l'APK sul telefono (via USB, Google Drive, email a te stesso...)
3. Apri il file APK → conferma installazione
4. L'app appare nella home come qualsiasi altra app!

---

## Note importanti

| Cosa | Dettaglio |
|---|---|
| **Dati** | Tutti i dati arrivano in tempo reale da Google Fit, nessun dato locale |
| **Login** | Alla prima apertura chiederà il Client ID (come nel browser) |
| **Aggiornamenti** | Bastano aggiornamenti al file `index.html` su GitHub — l'app si aggiorna automaticamente |
| **APK firmato per Play Store** | Richiede account developer Google ($25 una tantum) e procedura diversa |

---

## Risoluzione problemi comuni

**"Errore redirect_uri_mismatch"**
→ Non hai aggiunto il dominio GitHub Pages alle origini autorizzate (Step 2)

**PWABuilder dà score basso**
→ Assicurati che `manifest.json` e `sw.js` siano nella root del sito

**APK si installa ma dà errore di login**
→ Aspetta 10 min dopo aver salvato le credenziali Google, poi riprova

**L'icona non appare**
→ Verifica che `icons/icon-192.png` sia accessibile su `https://TUO-USERNAME.github.io/fitdash/icons/icon-192.png`
