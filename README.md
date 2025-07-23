# 🧠 ADAXI – Agente AI per la Città di Bari

> Sistema modulare di agenti AI su n8n, integrati con Telegram, per la gestione partecipata di **eventi**, **segnalazioni urbane** e **interazione civica**.

---

## 📦 Contenuto del repository

| File | Descrizione |
|------|-------------|
| `TELEGRAM BOT v2.5.json` | Workflow principale per la gestione eventi su Telegram. |
| `promptBOT.txt` | Prompt di sistema per l'agente Adaxi, con linee guida per la creazione e moderazione eventi. |
| `Adaxi - Agente Orchestratore.json` | Esempio di Orchestratore che riceve le richieste e le smista agli agenti tecnici. |
| `Adaxi - Agente Parchi.json` | Agente tecnico di esempio per la gestione segnalazioni relative ai parchi. Usato dall'Agente orchestratore |
| `Adaxi - Agente Strade.json` | Agente tecnico di esempio per le segnalazioni relative alle strade. Usato dall'Agente orchestratore |
| `Agente - Segnalazione Parchi.json` | Interfaccia Telegram per gestire segnalazioni ambientali e eventi. |
| `Agente - Feedback Creazione Evento.json` | Tool per fornire feedback qualitativo automatico sugli eventi già creati. Viene chiamato da un flusso creato ad hoc su Gancio |
| `LICENSE` | Licenza open source del progetto. |

---

## 🧭 Struttura del sistema

### 1. **Interfaccia Utente (Telegram)**
Gli utenti interagiscono tramite Telegram:
- Possono inviare testi, immagini o messaggi vocali.
- L'agente Adaxi interpreta il contenuto e avvia il processo adeguato.

### 2. **Agente ADAXI (Ruolo centrale)**
Un AI agent con funzione di filtro, smista le richieste:
- Verifica che la richiesta sia relativa al Comune di Bari.
- La inoltra all’agente tecnico appropriato (eventi, strade, parchi).
- Non fornisce risposte tecniche, solo accoglienza e smistamento.

### 3. **Agenti Tecnici**
Moduli specializzati:
- `Agente Parchi`: richiede **luogo** e **numero di telefono**.
- `Agente Strade`: richiede **luogo** (indirizzo o coordinate) e **numero di telefono**.
- Ogni agente verifica se i dati sono completi prima di salvare.

### 4. **Creazione e Gestione Eventi**
L'agente eventi:
- Guida l’utente passo passo nella creazione di una scheda evento.
- Estrae dati strutturati (nome, data, luogo, mood, valori, etc.).
- Verifica duplicati nel database.
- Salva su Supabase e sincronizza con [Gancio](https://gancio.baricittaperta.xyz/).

### 5. **Feedback e Moderazione**
- L’agente `Feedback Creazione Evento` analizza una scheda evento già salvata e restituisce:
  - Un feedback sintetico.
  - Suggerimenti di miglioramento.
  - Notifiche in caso di linguaggio scorretto o contenuti sensibili.

---

## 🛠 Tecnologie

- **n8n** (automazione e orchestrazione): https://docs.n8n.io/hosting/
- **OpenAI GPT-4 / GPT-4o** (ragionamento linguistico)
- **Telegram Bot API**
- **Supabase** (database eventi)
- **Gancio** (federazione eventi)
- **Docker (opzionale)** per il deploy

---

## 🗂 Tassonomia eventi

Utilizzata per il tagging automatico e la moderazione etica. Include:
- **Categorie**: concerti, teatro, mostre, sport, etc.
- **Mood**: rilassante, creativo, underground...
- **Accessibilità**, **valori**, **fascia d’età**, etc.

(vedi `promptBOT.txt` per l’elenco completo)
