# Lezione 8 — Lab (30 minuti): RDS (introduzione) — creare un DB e connettersi in modo controllato

## Obiettivo
- Capire cosa gestisce RDS (e cosa resta a carico vostro)
- Creare una piccola istanza RDS in scenario didattico
- Collegarsi da un client (o simulare connessione)

## Output atteso (a fine lab)
- Istanza RDS creata (o simulata) con **Public access = No**.
- Security Group configurato per consentire accesso solo dal client previsto.
- Cleanup completato (DB eliminato).

## Durata
30 minuti (timebox)

## Prerequisiti strumenti (comuni)
Vedi: `labs/00_prerequisiti_strumenti_git_cli.md`

## Link ufficiali (approfondimento)
- RDS (overview): https://aws.amazon.com/rds/
- RDS User Guide: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html
- RDS security overview: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurity.html

## Avvertenze costi
RDS può generare costi se lasciato attivo. Seguire il **cleanup**.

Regola: se ti fermi a metà lab, **cancella comunque** la risorsa prima di uscire.

## Prerequisiti
- Accesso AWS con permessi RDS
- Un client DB sul PC (opzionale) oppure usare EC2 come client

## Scelta engine
Consigliato: **MySQL** o **PostgreSQL** (in base a familiarità).

## Nota per stare nei 30 minuti
- La creazione completa di un DB RDS può richiedere più di 30 minuti.
- In questo lab facciamo un approccio **inspection/simulation-first**:
   - oppure il docente crea il DB prima della lezione e gli studenti lo ispezionano,
   - oppure arriviamo fino alla schermata di configurazione e verifichiamo i parametri **prima** di creare.

## Struttura (minuti)
- 0–5: Concetti + costi
- 5–20: Configurazione guidata (senza aspettare `Available`)
- 20–27: Checkpoint (public access, SG, endpoint/porta)
- 27–30: Cleanup (se avete creato risorse)

## Parte A — Configurazione (simulation-first) (15 minuti)
1) Aprire **RDS** → **Create database**.
2) Modalità: **Standard create**.
3) Engine: MySQL/PostgreSQL.
4) Template: scegliere il template più adatto al laboratorio (spesso **Dev/Test** o equivalente), secondo regole dell’account accademico.
5) Impostazioni:
   - DB instance identifier: `lab-rds-student01`
   - Master username/password: definire e custodire (non in chat pubbliche)
6) Connettività:
   - VPC: default
   - Public access: **No** (obbligatorio in questo lab)
   - Security group: nuovo o esistente; consentire porta DB solo dal security group del client (es. EC2)
7) Prima di creare: fai lo screenshot (o annota) delle scelte chiave.

Se il docente vi chiede di creare davvero il DB:
- cliccare **Create database** e poi passare subito alla Parte B (senza aspettare).

### Esempio “regola corretta” Security Group (concetto)
Se il client è una EC2 con un suo Security Group `sg-client-ec2`:
- Inbound sul SG del DB:
   - MySQL: TCP 3306 (oppure Postgres: TCP 5432)
   - Source: **sg-client-ec2** (non 0.0.0.0/0)

Messaggio chiave:
> "Il DB non deve essere raggiungibile da Internet; deve essere raggiungibile solo dal client autorizzato."

## Parte B — Verifica (senza aspettare) (10 minuti)
Per stare nei tempi, **non aspettiamo** che il DB diventi `Available`.

1) Se il DB esiste già (preparato dal docente): apri la risorsa e trova **endpoint/porta**.
2) Controlla (o descrivi) che **Public access = No**.
3) Spiega in 2 frasi: perché l’accesso pubblico è rischioso e perché si usa Security Group.

### (Opzionale) Connessione rapida (solo se DB pronto e c’è tempo)
- Usare una EC2 come client nella stessa VPC.
- Connettersi usando l’endpoint RDS (comandi indicativi):
  - MySQL: `mysql -h <endpoint> -P 3306 -u <utente> -p`
  - PostgreSQL: `psql "host=<endpoint> port=5432 user=<utente> dbname=postgres"`

## Checkpoint
- Hai identificato dove si imposta `Public access` e perché deve essere `No`.
- Hai identificato la porta (3306/5432) e la regola SG corretta (source = SG client, non `0.0.0.0/0`).

## Troubleshooting (rapido)
- **Stato non diventa Available**: attendere; RDS può impiegare diversi minuti.
- **Connessione fallisce**: controllare SG (porta corretta, source SG del client), stessa VPC/subnet reachability.
- **Password/utente**: verificare che le credenziali siano quelle del master create in fase A.

## Cleanup (obbligatorio) (3–10 minuti)
Se avete creato davvero un DB:
1) RDS → Databases → selezionare `lab-rds-student01` → **Delete**.
2) Snapshot finale: seguire indicazioni docente (spesso: disattivare in lab per velocità/costi).
3) Eliminare eventuali security group creati ad-hoc se non più usati.

## Debrief (5 minuti)
- Quali parti sono “gestite da AWS” in RDS e quali restano al cliente?
- Perché "Public access: Yes" è rischioso in un DB?
