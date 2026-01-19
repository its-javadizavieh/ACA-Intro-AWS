# Lezione 2 — Lab (30 minuti): Setup account, MFA (concetto) e alert costi (Budget)

## Obiettivo
- Impostare regole minime di sicurezza *account-level* (concetti)
- Attivare un alert di spesa per evitare sorprese

## Output atteso (a fine lab)
- Budget mensile creato con soglie 80% e 100% **oppure** scheda “anti-costi” completata (variante).
- Lo studente sa spiegare in 2 frasi:
   - perché il root non si usa tutti i giorni
   - cosa cambia con MFA

## Durata
30 minuti (timebox)

## Prerequisiti
- Accesso Console AWS.
- Se l’account è gestito dall’istituto: è possibile che Billing/Budgets non sia visibile (in quel caso usare la Variante).

Nota (account accademico):
- Il Free Tier potrebbe non essere rilevante.
- Billing può essere centralizzato: anche in quel caso, budget/alert e soprattutto cleanup restano buone pratiche.

## Regole prima di iniziare (1 minuto)
- Non usare credenziali reali in chat/screenshot.
- Non cliccare “Create” a caso fuori lab.
- Alla fine: checkpoint completato (Budget o Variante).

## Prerequisiti strumenti (comuni)
Vedi: `labs/00_prerequisiti_strumenti_git_cli.md`

## Link ufficiali (approfondimento)
- AWS Budgets: https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html
- AWS Billing and Cost Management (overview): https://docs.aws.amazon.com/cost-management/latest/userguide/what-is-costmanagement.html
- AWS Free Tier (solo informativo): https://aws.amazon.com/free/

## Esempio (da dire in aula)
"In un laboratorio il rischio #1 non è solo la sicurezza: è lasciare risorse accese. Un budget con alert è una cintura di sicurezza: non evita tutto, ma ti avvisa presto."

## Struttura (minuti)
- 0–5: Parte A (root + MFA, concetti)
- 5–22: Parte B (Budget) **oppure** Variante (se Billing non disponibile)
- 22–27: Esercizio convenzioni lab (naming + controlli)
- 27–30: Checkpoint + domande

## Parte A — Root user e MFA (concetti) (5 minuti)
1) Root user = “super-admin” dell’account; uso solo per attività eccezionali.
2) MFA (Multi-Factor Authentication): cosa è e perché è raccomandata.
3) (Opzionale demo docente) Dove si configura MFA per root.

### Mini-esercizio (2 minuti)
Completa la frase:
- "Se qualcuno ruba la mia password, con MFA attivo…" (risposta attesa: serve anche il secondo fattore)

### Domande rapide (1 minuto)
- Quali operazioni useresti ancora con il root? (esempi: gestione billing, chiusura account, casi eccezionali)

## Parte B — Budget di spesa (pratica) (17 minuti)
> Se non vedi Billing/Budgets: vai subito alla Variante.

1) Aprire **Billing and Cost Management**.
2) Andare in **Budgets** → **Create budget**.
3) Selezionare **Cost budget**.
4) Impostare:
   - Periodo: **Monthly**
   - Importo: **5 EUR/USD** (valore didattico)
5) Notifiche:
   - Email del docente o email di gruppo (decidere in classe)
   - Soglie: **80%** e **100%**
6) Creare il budget.

### Esempio valori “didattici”
- Budget: 5 EUR/mese
- Soglia 1: 80% (4 EUR)
- Soglia 2: 100% (5 EUR)

### Esercizio (5 minuti)
In coppia, definite una **convenzione** di naming e un “cartellino” di controllo per i lab:
- Regione unica del corso: ___________
- Prefisso risorse: `lab-<gruppo>-<servizio>`
- Regola: prima di uscire dall’aula, controllare: EC2 attive? RDS attive? bucket S3 vuoti?

## Variante (se Billing non disponibile) (17 minuti)
Compila una scheda: “Come evito costi inattesi su AWS?” con 5 azioni concrete.

### Esempi di azioni concrete (spunti)
- Imposto budget/alert appena creato l’account.
- Metto tag/nomi coerenti alle risorse.
- Evito di provare servizi non richiesti dal corso.
- Faccio cleanup a fine lab (termino EC2, elimino bucket, elimino RDS).
- Controllo Cost Explorer / Billing a fine giornata.

## Checkpoint (cosa verificare)
- Esiste un budget attivo oppure è stata prodotta la scheda variante.

## Troubleshooting (rapido)
- **Non vedo Billing/Budgets**: l’account potrebbe non avere permessi; passare alla Variante.
- **Account gestito dall’istituto**: spesso Billing è centralizzato; usare la Variante e concentrarsi su cleanup e naming.

## Cleanup
Nessuna risorsa da eliminare (il budget può restare attivo).

## Debrief (3 minuti)
- Qual è la risorsa che “dimenticata” costa di più in laboratorio? (spesso EC2/RDS)
- Quale abitudine personale adotterai da oggi per evitare costi inattesi?
