# Lezione 6 — Lab (30 minuti): S3 (bucket, upload e bucket policy — accesso controllato)

## Obiettivo
- Creare un bucket S3
- Caricare un file
- Capire cosa fa una bucket policy (introduzione)

## Output atteso (a fine lab)
- Bucket creato con Block Public Access attivo.
- Oggetto `hello.txt` caricato.
- Bucket policy applicata e dimostrata (DeleteObject negato).
- Cleanup completo (bucket eliminato).

## Durata
30 minuti (timebox)

## Prerequisiti strumenti (comuni)
Vedi: `labs/00_prerequisiti_strumenti_git_cli.md`

## Link ufficiali (approfondimento)
- S3 (overview): https://aws.amazon.com/s3/
- Bucket policies: https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html
- Block Public Access: https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html

## Prerequisiti
- Accesso AWS con permessi S3

## Struttura (minuti)
- 0–8: Parte A (creazione bucket)
- 8–12: Parte B (upload)
- 12–20: Parte C (bucket policy + test)
- 20–30: Cleanup obbligatorio

## Parte A — Creare un bucket (8 minuti)
1. Aprire **S3** → **Create bucket**.
2. Nome: `lab-s3-<iniziali>-<numero>` (deve essere globale/unico).
3. Regione: quella scelta per il corso.
4. **Block Public Access:** lasciare attivo (consigliato).
5. Creare.

### Suggerimento per nomi globalmente unici
Esempio:
- `lab-s3-ab-20260107-01`
Se il nome risulta “già esistente”, cambiare numero o aggiungere data.

## Parte B — Upload e test (4 minuti)
1. Aprire bucket → **Upload**.
2. Caricare un file di testo `hello.txt` (contenuto libero).
3. Verificare che l’oggetto sia presente.

### Esempio contenuto `hello.txt`
Scrivi 3 righe:
1) Nome studente/coppia
2) Regione usata
3) Data

## Parte C — Bucket policy (dimostrazione guidata) (8 minuti)
Scopo: vedere un esempio concreto in cui un **Deny** blocca un’azione.

1. Aprire bucket → tab **Permissions**.
2. Aprire **Bucket policy**.
3. (30 secondi) Cosa sono `Principal`, `Action`, `Resource`.
4. Inserire una policy **di esempio didattico** che *nega* l’eliminazione degli oggetti a chiunque (effetto dimostrativo):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyDeleteObject",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::REPLACE_ME/*"
    }
  ]
}
```

5. Sostituire `REPLACE_ME` con il nome del bucket.
6. Salvare.
7. Provare a cancellare `hello.txt` dalla Console: deve fallire con accesso negato.

Tempo target: 8 minuti

## Checkpoint
- Bucket creato e file caricato
- DeleteObject negato (dimostrazione riuscita)

## Troubleshooting (rapido)
- **Non riesco a salvare la bucket policy**: controllare ARN e che `REPLACE_ME` sia stato sostituito.
- **Riesco ancora a cancellare**: la policy potrebbe non essere stata salvata o stai cancellando da un percorso non coperto; ricontrollare `Resource`.

## Cleanup (obbligatorio) (10 minuti)
1. Rimuovere la bucket policy (tab Permissions).
2. Eliminare gli oggetti dal bucket.
3. Eliminare il bucket.

## Debrief (3 minuti)
- Bucket policy vs IAM policy: qual è “attaccata alla risorsa” e qual è “attaccata all’identità”?
