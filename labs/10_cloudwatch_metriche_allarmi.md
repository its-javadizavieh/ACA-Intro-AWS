# Lezione 10 — Lab: CloudWatch (metriche e allarmi) (NON valutato)

## Obiettivo
- Fare pratica con **CloudWatch**: metriche, allarmi e interpretazione degli stati.
- Capire cosa significa `OK` / `ALARM` / `INSUFFICIENT_DATA`.
- Applicare disciplina di **cleanup** (anche per gli allarmi).

Regola importante:
- Questo lab **non entra nella verifica/quiz** e non influisce sul punteggio.

## Durata
60 minuti (seconda ora della Lezione 10)

## Prerequisiti
- Accesso Console AWS.
- Una EC2 già esistente dalla Lezione 5 (consigliata) oppure una EC2 disponibile in account.

## Link ufficiali (AWS) — per ripasso a casa
- What is Amazon CloudWatch?: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html
- CloudWatch Metrics (concetti): https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html
- CloudWatch Alarms (concetti): https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html
- Stati di un allarme (OK/ALARM/INSUFFICIENT_DATA): https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html

---

## Parte A — Warm-up (5 minuti)
Checklist mentale (da dire ad alta voce):
1) Sono nella **regione giusta**?
2) Ho selezionato l’**istanza giusta** (InstanceId)?
3) Sto guardando la metrica corretta (es. **CPUUtilization**)?
4) Alla fine: elimino l’allarme creato?

---

## Parte B — Metriche: dove le trovo (10 minuti)
Obiettivo:
- Aprire CloudWatch e trovare le metriche di una EC2.

Passi:
1) Vai in **CloudWatch** → **Metrics** → **EC2**.
2) Scegli **Per-Instance Metrics**.
3) Seleziona l’istanza corretta (InstanceId) e guarda **CPUUtilization**.

Output atteso:
- Lo studente sa trovare il grafico CPU dell’istanza giusta.

---

## Parte C — Creare un allarme (20 minuti)
Obiettivo:
- Creare un allarme su CPU per una EC2 e capirne la logica.

Passi:
1) CloudWatch → **Alarms** → **Create alarm**
2) Seleziona metrica: **EC2 → Per-Instance Metrics → CPUUtilization** (istanza corretta)
3) Imposta soglia didattica:
   - Esempio: `CPUUtilization > 50%` per **1** periodo
4) Configura nome allarme: `lab-cw-cpu-alarm-<pair>`
5) (Opzionale) Notifiche: se non avete SNS/email, lasciare solo allarme “visuale”
6) Crea l’allarme

Output atteso:
- Allarme creato e visibile nella lista.

---

## Parte D — Generare carico e osservare lo stato (15 minuti)
Obiettivo:
- Vedere cambiare (se possibile) grafico e/o stato dell’allarme.

Opzione A (consigliata): se hai accesso alla EC2 via Session Manager/SSH
1) Genera carico CPU per 60–120 secondi (esempio):
   - `yes > /dev/null &` (ferma con `kill %1`)
2) Torna su CloudWatch e osserva il grafico.

Opzione B: se non puoi generare carico
- Spiega cosa succede quando la metrica supera la soglia e perché serve tempo per i dati.

Output atteso:
- Lo studente interpreta correttamente `OK` / `ALARM` / `INSUFFICIENT_DATA`.

---

## Parte E — Troubleshooting (10 minuti)
Se l’allarme resta sempre `OK` o sempre `INSUFFICIENT_DATA`:
1) Controlla la metrica selezionata e la dimensione (InstanceId corretto).
2) Controlla periodo e “evaluation periods” (serve tempo per raccogliere dati).
3) Verifica che la EC2 sia **running**.
4) Se hai generato carico, verifica che il grafico CPU sia effettivamente salito.

---

## Parte F — Debrief (5 minuti)
- In 1 frase: perché un allarme è utile in produzione?
- Qual è stato l’errore più comune? (istanza sbagliata / periodo / dati insufficienti)

---

## Cleanup (obbligatorio)
- Ferma/termina risorse create solo per la lezione.
- Elimina allarmi CloudWatch creati per prove.
- Svuota/elimina bucket di test se non serve.

Checklist finale:
- Nessun allarme “di prova” rimasto.
