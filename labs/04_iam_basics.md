# Lezione 4 — Lab (30 minuti): IAM basics (utente, gruppo, policy e accesso Console)

## Obiettivo
- Capire la differenza tra **utente**, **gruppo** e **policy**
- Creare un utente con permessi limitati e login alla Console

## Output atteso (a fine lab)
- Esiste un gruppo con permessi predefiniti.
- Esiste un utente “studente” che riesce a fare login.
- Lo studente sa mostrare un errore `AccessDenied` e spiegarlo (permessi insufficienti).

## Durata
30 minuti (timebox)

## Prerequisiti strumenti (comuni)
Vedi: `labs/00_prerequisiti_strumenti_git_cli.md`

## Link ufficiali (approfondimento)
- IAM (introduction): https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html
- IAM best practices: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- Policy reference (JSON elements): https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html

## Prerequisiti
- Accesso AWS con permessi IAM amministrativi (docente o account didattico)

Nota didattica (per stare nei 30 minuti):
- In molti contesti gli studenti **non** hanno permessi IAM admin.
- Percorso consigliato: il docente prepara gli utenti `student01`, `student02`, … e gli studenti fanno login + test `AccessDenied`.

## Step 0 — Regione
IAM è globale, ma decidere comunque una regione per gli altri lab (es. `eu-central-1`).

### Nota didattica
- Anche se IAM è globale, in molti lab successivi (EC2/S3/RDS/CloudWatch) la **regione** conta.
- Regola pratica: prima di iniziare un lab, controllare sempre la regione in alto a destra.

### Convenzione naming consigliata (classe/coppie)
- Gruppo: `StudentsReadOnly`
- Utenti: `student01`, `student02`… oppure `pair01`, `pair02`…

## Struttura (minuti)
- 0–5: Step 0 (regione + regole)
- 5–20: Parte A+B (creazione gruppo+utente) **solo se avete permessi admin**
- 20–27: Parte C (login + test AccessDenied)
- 27–30: Debrief + checkpoint

## Parte A — Creare un gruppo (permessi didattici) (opzionale, 7 minuti)
1. Aprire **IAM** → **User groups** → **Create group**.
2. Nome gruppo: `StudentsReadOnly`.
3. Allegare policy gestita: **ReadOnlyAccess** (solo per scopo didattico).
4. Creare gruppo.

Tempo target: 7 minuti

## Parte B — Creare un utente “studente” (opzionale, 8 minuti)
1. IAM → **Users** → **Create user**.
2. User name: `student01` (o schema per coppie).
3. Selezionare accesso: **AWS Management Console access**.
4. Impostare password iniziale e spuntare **Require password reset**.
5. Aggiungere l’utente al gruppo `StudentsReadOnly`.
6. Creare utente.

Tempo target: 8 minuti

### Esempio: cosa annotare (senza diffondere credenziali)
- Username: `student01`
- Password iniziale: comunicata solo allo studente (o consegnata su foglio)
- Flag: password reset al primo login = **attivo**

## Parte C — Test permessi (7 minuti)
1. Effettuare logout.
2. Accedere con `student01` usando la URL di accesso dell’account.
3. Verificare:
   - È possibile navigare servizi e vedere risorse.
   - Non è possibile creare una risorsa (es. provare ad avviare una EC2: deve negare).

Tempo target: 7 minuti

## Parte D — Debrief (5 minuti)
- Perché **ReadOnlyAccess** non è adatta in produzione?
- Definisci in una frase **least privilege**.

## Checkpoint
- Il login “student01” funziona.
- Un’azione di scrittura fallisce con “AccessDenied”.

## Cleanup (opzionale)
Se non serve più:
- Eliminare `student01`
- Eliminare gruppo `StudentsReadOnly`

## Troubleshooting (rapido)
- **Non trovo la URL di login account**: in IAM spesso è in “Dashboard” (AWS account sign-in URL).
- **Password reset non funziona**: controllare policy password dell’account e che l’utente abbia accesso console abilitato.
- **Errore “not authorized” quando creo gruppo/utente**: l’account usato non ha permessi IAM admin (serve docente/account didattico).

## Debrief (3 minuti)
- Qual è la differenza tra “identità” e “permessi”?
- Quale sarebbe un esempio di permesso minimo per uno studente in un lab specifico?

