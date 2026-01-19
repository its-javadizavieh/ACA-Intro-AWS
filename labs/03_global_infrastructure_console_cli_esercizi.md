# Lezione 3 — Lab (30 minuti): Global Infrastructure + Console/CLI (senza creare risorse)

## Obiettivo
- Saper scegliere una regione con criteri reali.
- Saper orientarsi nella Console.
- Capire quando usare CLI (concetto) e i rischi delle credenziali.

## Durata
30 minuti (timebox)

## Materiale
- Console AWS (anche solo demo docente) oppure screenshot

## Link ufficiali (AWS) — per ripasso a casa
- Infrastruttura globale (mappa): https://infrastructure.aws/
- Servizi per regione: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/
- AWS Management Console (getting started): https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html
- AWS CLI (introduzione): https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html
- Gestione credenziali (best practice): https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds.html
- CloudWatch Alarms (panoramica): https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html

---

## Struttura (minuti)
- 0–10: Scelta regione (3 casi)
- 10–22: Scavenger hunt Console (solo navigazione)
- 22–28: Console vs CLI (tabella)
- 28–30: Mini-debrief

## Esercizio 1 — Scelta regione (3 casi)
Per ogni caso, scegli una regione e motiva con 2 criteri tra: latenza, compliance, disponibilità servizi, costi.

1) Applicazione interna per azienda in Italia, dati non sensibili.
2) Applicazione pubblica globale (utenti ovunque) con contenuti statici.
3) Dati sensibili con vincolo di residenza (es. “dati in UE”).

Output atteso:
- Regione scelta + motivazione breve e coerente.

---

## Esercizio 2 — “Scavenger hunt” Console (solo navigazione)
Senza creare risorse, trova dove si trovano (menu/ricerca):
1) Il selettore regione
2) IAM Users
3) EC2 Instances
4) S3 Buckets
5) CloudWatch Alarms

Regola:
- Non cliccare “Create” o “Launch”.

---

## Esercizio 3 — Console vs CLI (tabella)
Completa la tabella con 2 pro e 2 contro:

| Strumento | Pro | Contro |
|---|---|---|
| Console | ________ | ________ |
| CLI | ________ | ________ |

Soluzione attesa (indicativa):
- Console: facile per imparare / visuale; contro: meno ripetibile.
- CLI: automazione/ripetibilità; contro: gestione credenziali/curva di apprendimento.

---

## Mini-debrief (5 minuti)
- Qual è l’errore più comune quando “non trovo una risorsa”? (risposta attesa: regione sbagliata)
- Perché è pericoloso copiare/incollare credenziali in documenti o chat?

## Checkpoint (consegna rapida)
- 3 regioni scelte con 2 criteri ciascuna.
- Tabella Console vs CLI completata.
