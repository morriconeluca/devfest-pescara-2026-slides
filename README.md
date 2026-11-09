# Dalla Sicofanzia alla Realtà: Agent Harness Deterministici per l'SDLC

> **DevFest Pescara 2026**  
> **Speaker:** Luca Morricone (Frontend Developer)  
> Materiale ufficiale della presentazione e slide del talk.

---

## 📌 Panoramica del Talk

Negli scenari di sviluppo software moderni in cui i modelli linguistici (LLM) e gli agenti autonomi generano codice a ritmi senza precedenti, l'approccio tradizionale **Human in the Loop** diventa rapidamente il collo di bottiglia: l'essere umano non è in grado di revisionare il codice alla stessa velocità con cui viene prodotto.

Il talk affronta il passaggio cruciale verso l'**automazione completa del Software Development Life Cycle (SDLC)**, ponendosi una domanda fondamentale:  
*Come possiamo garantire la qualità e la sicurezza del software quando deleghiamo l'intero ciclo agli agenti IA?*

Non si tratta di riporre una "cieca fiducia" nei modelli, ma di comprendere i loro limiti intrinseci (sicofanzia, allucinazioni, bias cognitivi, *Context Rot* e *Lost in the Middle*) e superare l'illusione del cosiddetto **"Test Theater"** — la tendenza degli agenti a scrivere test tautologici che validano semplicemente ciò che il codice già fa, senza reale valore di verifica.

La soluzione proposta si basa sui principi della cibernetica e dell'**Agent Harness Engineering**: bilanciare il **feedforward inferenziale** (istruzioni e prompt) con **feedback computazionali deterministici** (tipizzazione statica rigorosa, vincoli architetturali, linter, coverage e soprattutto **Mutation Testing**).

---

## 🧭 I Due Piani del Controllo

L'ingegnerizzazione dell'harness per agenti si struttura su due piani:

1. **Piano dell'Indirizzo (Feedforward)**: ciò che viene fornito all'agente prima che agisca (regole, contesto, skill, contratti).
   - *Limiti del solo feedforward inferenziale*: non garantisce il rispetto delle regole, genera effetti non locali (*stratificazione semantica*, e.g. "no-fluff"), e degrada con l'aumentare dei token di contesto.
2. **Piano della Retroazione (Feedback)**: ciò che osserva e valida il risultato dopo l'azione (compilatore, linter architetturali, test suite, mutation testing).
   - *Feedback computazionale*: metriche oggettive e vincolanti (complessità ciclomatica, soglie di copertura, mutation score con Stryker) per sconfiggere il gaming delle metriche (Legge di Goodhart) e il test theater.

Un harness deterministico efficace integra questi piani in un sistema coerente in cui l'indirizzo computazionale/inferenziale e la retroazione computazionale si rinforzano a vicenda.

---

## 📂 Contenuto del Repository

All'interno di questo repository sono disponibili le slide della presentazione:

- [`devfest-2026.pdf`](./devfest-2026.pdf): versione PDF delle slide proiettate durante il DevFest Pescara 2026.
- [`devfest-2026.pptx`](./devfest-2026.pptx): file originale della presentazione Microsoft PowerPoint.

---

## 💻 La Demo: "Il Terminale dell'Operatore"

Durante la sessione è stata condotta una demo in diretta che mette a confronto lo sviluppo parallelo con agenti AI (orchestratore e sub-agenti eseguiti su tab [Herdr](https://github.com) con git worktrees e modello `gemini-3.8-flash-high`) su un'applicazione React a tema Matrix (*"Il Terminale dell'Operatore"*):

I sorgenti completi e i prompt utilizzati sono consultabili nei due repository dedicati:

1. 🔴 **[demo-pescara-2026-demo-without-gates](https://github.com/morriconeluca/demo-pescara-2026-demo-without-gates)**  
   *Scenario senza Quality Gates computazionali:* gli agenti sviluppano basandosi esclusivamente sul feedforward del prompt e sulle configurazioni standard di React + Vite, evidenziando i rischi di instabilità, mancanza di verifiche oggettive e test deboli.
   - Contiene il file [`PROMPT.md`](https://github.com/morriconeluca/demo-pescara-2026-demo-without-gates/blob/main/PROMPT.md) usato per la demo.

2. 🟢 **[devfest-pescara-2026-demo-with-gates](https://github.com/morriconeluca/devfest-pescara-2026-demo-with-gates)**  
   *Scenario con Harness Deterministico (5 Quality Gates):* gli agenti sono governati da gate sequenziali obbligatori prima del merge:
   - **Gate 1:** Formattazione (Prettier) e Type-checking rigoroso TypeScript (`tsc --noEmit`).
   - **Gate 2:** ESLint con conformità architetturale FAF (`@morriconeluca/eslint-plugin-faf`) e strict typing.
   - **Gate 3:** Vitest con unit, integration e fitness test architetturali (coverage ≥ 95% lines, ≥ 90% branches).
   - **Gate 4:** **Stryker Mutation Testing** per eliminare il *Test Theater* (mutation score ≥ 80% per file).
   - **Gate 5:** Build di produzione Vite con React Compiler.
   - Contiene il file [`PROMPT.md`](https://github.com/morriconeluca/devfest-pescara-2026-demo-with-gates/blob/main/PROMPT.md) orchestrato con la skill `solve-problem` e l'esecuzione automatica dei gate.

---

## 👤 Autore

**Luca Morricone**  
- GitHub: [@morriconeluca](https://github.com/morriconeluca)
- Speaker al DevFest Pescara 2026
