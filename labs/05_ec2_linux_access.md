# Lezione 5 — Lab (30 minuti): EC2 Linux (avvio istanza e accesso via SSH o Session Manager)

## Obiettivo
- Creare una EC2 “low cost” secondo le regole dell’account accademico
- Capire Security Group e chiavi
- Connettersi in modo controllato

## Output atteso (a fine lab)
- Un’istanza EC2 avviata con naming chiaro (e tag se richiesti dal docente).
- Accesso riuscito (Session Manager oppure SSH).
- Lo studente sa spiegare:
   - cosa fa un Security Group
   - perché non si apre SSH a `0.0.0.0/0`

## Durata
30 minuti (timebox)

## Prerequisiti
- Accesso AWS con permessi EC2
- (Opzionale) PC con client SSH

## Prerequisiti strumenti (comuni)
Vedi: `labs/00_prerequisiti_strumenti_git_cli.md`

## Link ufficiali (approfondimento)
- EC2 (overview): https://aws.amazon.com/ec2/
- EC2 key pairs: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html
- Security Groups (VPC): https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html
- Session Manager: https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html

## Scelta didattica (per stare nei 30 minuti)
Preferire **AWS Systems Manager Session Manager** (evita porte in ingresso e gestione chiavi).

SSH resta **opzionale** (solo se Session Manager non è disponibile).

## Pre-check (2 minuti)
- Regione: confermare la regione corretta del corso.
- Naming: usare uno schema coerente (es. `lab-ec2-student01`).
- Cost governance: ricordare che a fine lab c’è **terminate** obbligatorio.

## Struttura (minuti)
- 0–3: Pre-check
- 3–15: Parte A (creazione istanza)
- 15–23: Parte B (connessione)
- 23–25: Parte C (concetti rapidi)
- 25–30: Cleanup obbligatorio

## Parte A — Creazione istanza (Console) (12 minuti)
1. Aprire **EC2** → **Instances** → **Launch instances**.
2. Nome: `lab-ec2-student01`.
3. AMI: Amazon Linux (o equivalente) approvata per l’account accademico.
4. Instance type: scegliere una taglia piccola (es. `t3.micro` o equivalente) in base a policy/quote dell’account.
5. Key pair:
   - **Session Manager**: key pair **non necessaria**.
   - **SSH (opzionale)**: creare/selezionare una key pair.
6. Network settings:
   - VPC default
   - Subnet a scelta
   - Auto-assign public IP: **Disabled** (se usi Session Manager)
   - Auto-assign public IP: **Enabled** (solo se usi SSH)
7. Security group:
   - Session Manager: nessuna regola inbound (lasciare vuoto)
   - SSH (opzionale): consentire **solo** `TCP 22` dal vostro IP (non 0.0.0.0/0)
8. Storage: default.
9. Launch.

### Esempio regola Security Group (SSH)
- Type: SSH
- Protocol: TCP
- Port range: 22
- Source: My IP (consigliato)

### Esercizio (5 minuti)
Chiedi agli studenti di indicare cosa succede se:
- apro SSH verso `0.0.0.0/0`
- lascio SSH aperto per ore/giorni

Risposta attesa: aumento superficie d’attacco (scanner automatici, brute force) e rischio incidenti.

## Parte B — Connessione (15 minuti)
### Opzione principale: Session Manager
1. EC2 → selezionare istanza → **Connect** → **Session Manager**.
2. Avviare sessione.
3. Eseguire comandi:
   - `uname -a`
   - `whoami`

Output atteso (indicativo):
- `whoami` → utente tipo `ssm-user` o simile

### Opzione alternativa (solo se serve): SSH
1. Recuperare Public IPv4/DNS dell’istanza.
2. Connettersi (esempio):
   - `ssh -i <chiave.pem> ec2-user@<public-ip>`
3. Eseguire comandi:
   - `uname -a`
   - `df -h`

Output atteso (indicativo):
- `df -h` mostra almeno un filesystem root `/`.

## Parte C — Concetti da verificare (10 minuti)
- Differenza tra **Security Group** e firewall locale
- Perché limitare l’accesso SSH al proprio IP

### Mini-quiz (3 minuti)
1) Il Security Group è stateless o stateful? (risposta attesa: stateful)
2) Se cambio rete (IP diverso), cosa può succedere alla connessione SSH? (risposta: l’IP non è più autorizzato)

## Checkpoint (2 minuti)
- Istanza in stato `running`
- Accesso riuscito (Session Manager o SSH)

## Troubleshooting (rapido)
- **SSH timeout**: controllare Security Group (porta 22 dal proprio IP), public IP associato, subnet/public routing.
- **Permission denied (publickey)**: key pair sbagliata o permessi file `.pem` errati.
- **Session Manager non disponibile**: l’istanza potrebbe non essere configurata per SSM o mancano permessi; usare SSH (se consentito) o chiedere setup docente.

## Cleanup (obbligatorio) (5 minuti)
1. EC2 → Instances → selezionare `lab-ec2-student01` → **Terminate**.
2. Verificare che non restino volumi EBS inutilizzati.

### Verifica cleanup (checklist)
- Nessuna istanza `running` o `stopped` rimasta.
- Nessun volume EBS “orphan” non necessario.

## Se avanza tempo (facoltativo, 2 minuti)
- Spiega in 1 frase la differenza tra “stop” e “terminate”.
