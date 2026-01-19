# Lezione 1 — Lab (30 minuti): Fondamenti Cloud & panoramica AWS (senza account)

## Obiettivo
Allenare il linguaggio: cloud, vantaggi/limiti, IaaS/PaaS/SaaS, concetto di “risorsa”.

## Durata
30 minuti (in aula)

## Materiale
- Lavagna o foglio A4

## Link ufficiali (AWS) — per ripasso a casa
- What is Cloud Computing?: https://aws.amazon.com/what-is-cloud-computing/
- Tipi di cloud computing: https://aws.amazon.com/types-of-cloud-computing/
- AWS Pricing (panoramica): https://aws.amazon.com/pricing/
- AWS Free Tier: https://aws.amazon.com/free/

---

## Struttura (minuti)
- 0–10: Esercizio 1 (classifica)
- 10–20: Esercizio 2 (benefici vs trade-off)
- 20–28: Esercizio 3 (tutto è una risorsa)
- 28–30: Debrief + consegna

## Esercizio 1 — Classifica (IaaS / PaaS / SaaS)
Per ogni scenario, scegli il modello e spiega **in una frase** “chi gestisce cosa”.

1) Hai una VM nel cloud e installi tu Nginx e MySQL.
2) Usi un database gestito dove imposti credenziali e rete, ma patch/backup sono automatizzati.
3) Usi una webmail aziendale via browser.

Soluzione attesa (indicativa):
- 1) IaaS
- 2) PaaS/Managed service
- 3) SaaS

---

## Esercizio 2 — Benefici vs Trade-off
Compila la tabella (almeno 2 esempi per colonna):

| Beneficio | Esempio concreto | Trade-off | Esempio concreto |
|---|---|---|---|
| Elasticità | ________ | Lock-in | ________ |
| OPEX | ________ | Costi variabili | ________ |

Suggerimento (se ti blocchi):
- Elasticità: “Black Friday / picchi utenti”.
- Lock-in: “servizio proprietario difficile da migrare”.
- Costi variabili: “dimentico risorse accese”.

---

## Esercizio 3 — “Tutto è una risorsa” (AWS mindset)
Scrivi 5 esempi di “risorsa” in AWS e per ciascuna rispondi:
- Come la nomineresti in un laboratorio?
- Come la elimineresti a fine lab?

Esempio:
- Risorsa: istanza EC2
- Nome: `lab-ec2-pair01`
- Cleanup: terminate

---

## Debrief (5 minuti)
Domande per la classe:
- Quale trade-off del cloud ti sembra più rischioso: lock-in o costi variabili? Perché?
- Qual è una regola di comportamento che adotterai in laboratorio per non creare problemi (sicurezza/costi)?

## Checkpoint (consegna rapida)
- Esercizio 1 completato con 1 frase per scenario.
- Tabella Esercizio 2 con almeno 2 esempi per colonna.
- Lista di 5 risorse con naming + cleanup.
