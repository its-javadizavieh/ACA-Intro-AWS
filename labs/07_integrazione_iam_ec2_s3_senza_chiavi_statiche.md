# Lezione 7 — Lab (30 minuti): Integrazione IAM + EC2 + S3 (senza chiavi statiche)

## Obiettivo
- Creare un **ruolo IAM** per EC2 con permessi minimi su S3.
- Associare il ruolo a una EC2.
- Verificare accesso a S3 **senza** configurare access key statiche.

## Durata
30 minuti (timebox)

## Prerequisiti strumenti (comuni)
Vedi: `labs/00_prerequisiti_strumenti_git_cli.md`

## Link ufficiali (approfondimento)
- IAM roles: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html
- Using IAM roles with EC2: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html
- IAM policy examples: https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html

## Prerequisiti
- Permessi IAM (creazione ruoli/policy) e permessi EC2.
- Una EC2 attiva (puoi usare quella della Lezione 5: `labs/05_ec2_linux_access.md`) oppure crearne una.
- Un bucket S3 con un oggetto `hello.txt` (puoi usare/ricreare la Lezione 6: `labs/06_s3_bucket_policy.md`).

Nota didattica (per stare nei 30 minuti):
- **Percorso consigliato**: il docente prepara in anticipo il ruolo `LabEc2S3ReadOnly` (e la policy), gli studenti lo **associano** e fanno la verifica.
- Se la classe ha tempo e permessi: usare il percorso “Completo” (creazione policy+ruolo).

## Regole
- Vietato usare access key statiche sul filesystem della EC2.
- Permessi minimi: non usare policy “Admin”.

---

## Struttura (minuti)
- 0–5: Parte A (verifica prerequisiti: EC2 + S3)
- 5–12: Parte D (associa ruolo alla EC2)
- 12–25: Parte E (verifica da EC2, senza chiavi statiche)
- 25–30: Debrief + checkpoint

## Parte A — Prerequisiti rapidi (5 minuti)
1) Verifica che esista un bucket `lab-s3-...`.
2) Verifica che contenga `hello.txt`.
3) Verifica che esista una EC2 `running`.

Esercizio (2 minuti):
- Scrivi il nome bucket e la regione:
  - Bucket: __________
  - Regione: __________

---

## Percorso completo (solo se avete tempo e permessi)

## Parte B — Creare la policy minima (S3 read) (8 minuti)

Permessi minimi tipici per leggere un oggetto da S3:
- `s3:ListBucket` sul bucket
- `s3:GetObject` sugli oggetti

### Policy di esempio (da adattare)
Sostituisci `REPLACE_BUCKET_NAME` con il nome del tuo bucket.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListBucket",
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": "arn:aws:s3:::REPLACE_BUCKET_NAME"
    },
    {
      "Sid": "ReadObjects",
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::REPLACE_BUCKET_NAME/*"
    }
  ]
}
```

Nota (rapida): in produzione si restringe spesso anche con condizioni/prefissi.

---

## Parte C — Creare il ruolo IAM per EC2 (7 minuti)
1) IAM → Roles → Create role.
2) Trusted entity: **AWS service**.
3) Use case: **EC2**.
4) Allegare la policy creata (o una policy equivalente autorizzata dal docente).
5) Nome ruolo: `LabEc2S3ReadOnly`.
6) Creare ruolo.

Checkpoint:
- Ruolo creato e visibile in IAM.

---

## Parte D — Associare il ruolo alla EC2 (7 minuti)

### Caso 1: EC2 già esistente
1) EC2 → Instances → seleziona istanza.
2) Actions → Security → Modify IAM role.
3) Seleziona `LabEc2S3ReadOnly`.

### Caso 2: nuova EC2
Durante “Launch instance”, seleziona il ruolo (IAM role) nelle impostazioni avanzate.

Checkpoint:
- L’istanza risulta associata al ruolo.

---

## Parte E — Verifica da EC2 (senza chiavi statiche) (13 minuti)

1) Connettiti alla EC2 (Session Manager o SSH).
2) Verifica che **non** ci siano credenziali statiche configurate:
   - Non eseguire `aws configure`.

### Se AWS CLI non è presente (solo se serve)
- Controlla: `aws --version`
- Se manca, installa (una delle due, in base alla distro):
  - Amazon Linux (yum): `sudo yum install -y awscli`
  - Amazon Linux 2023 (dnf): `sudo dnf install -y awscli`

### Comandi di test (consigliati)
1) Verifica identità (se disponibile):
- `aws sts get-caller-identity`

2) Lista oggetti:
- `aws s3 ls s3://REPLACE_BUCKET_NAME/`

3) Leggi l’oggetto:
- `aws s3 cp s3://REPLACE_BUCKET_NAME/hello.txt -`

Output atteso:
- Il contenuto di `hello.txt` viene stampato a schermo.

## Checkpoint (fine lab)
- L’istanza EC2 legge `hello.txt` da S3 senza `aws configure`.
- Lo studente sa dire in 1 frase perché il ruolo è più sicuro della access key.

---

## Debrief (5 minuti)
- In 1 frase: perché un ruolo EC2 è più sicuro delle access key statiche?

---

## Troubleshooting (rapido)
- `AccessDenied` su `aws s3 ls`: manca `s3:ListBucket` sul bucket.
- `AccessDenied` su `aws s3 cp ... hello.txt`: manca `s3:GetObject` sugli oggetti.
- `Unable to locate credentials`: il ruolo non è associato alla EC2, oppure CLI non sta usando IMDS.

---

## Cleanup
- Se hai creato risorse solo per questo lab:
  - termina la EC2 (se non serve più)
  - svuota/elimina bucket (se non serve più)
  - elimina ruolo/policy (se l’ambiente non è condiviso)

Nota:
- In ambienti didattici condivisi, il docente può chiedere di **non eliminare** ruoli/policy fino a fine corso.
