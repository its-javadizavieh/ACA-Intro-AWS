# Prerequisiti — Strumenti (Git + clone repo) e AWS CLI (opzionale)

## Obiettivo (10–15 minuti)
- Mettere tutti gli studenti nelle condizioni di **aprire i materiali** e seguire i lab.
- Installare Git (se manca) e clonare il repository del corso.
- (Opzionale) Installare AWS CLI solo se il docente chiede comandi da terminale.

Regola pratica:
- Se finisci in 5 minuti: aiuta chi è in difficoltà.

---

## 1) Clonare il repository (materiali corso)

Quando avrai il link GitHub del corso, usa:

```bash
git clone <INCOLLA_QUI_URL_REPO>
cd <NOME_CARTELLA_REPO>
```

Se vuoi aggiornare i file in futuro:

```bash
git pull
```

---

## 2) Se Git NON è installato (Windows)

### Opzione A — Installer ufficiale (consigliata)
1) Scarica e installa Git:
- https://git-scm.com/download/win
2) Apri **Git Bash** oppure **PowerShell** e verifica:

```bash
git --version
```

### Opzione B — winget (Windows 10/11)
In PowerShell:

```powershell
winget install --id Git.Git -e
```

Poi verifica:

```powershell
git --version
```

---

## 3) Git su macOS / Linux

### macOS (con Homebrew)
```bash
brew install git
```

### Ubuntu/Debian
```bash
sudo apt update
sudo apt install -y git
```

Verifica:
```bash
git --version
```

---

## 4) AWS CLI (opzionale)

Nota: molti lab si fanno solo da Console. Installa AWS CLI solo se richiesto.

Documentazione ufficiale:
- https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

## Link ufficiali (AWS) — per ripasso a casa
- AWS CLI (welcome/overview): https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html
- Configurare AWS CLI (solo se richiesto dal docente): https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html
- Credenziali AWS (best practice): https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds.html

### Windows
- Segui la guida ufficiale oppure usa winget:

```powershell
winget install --id Amazon.AWSCLI -e
```

### macOS / Linux
- Segui la guida ufficiale (varia per distro).

Verifica:
```bash
aws --version
```

---

## 5) Best practice (student-friendly)
- Non condividere access key / password in chat o documenti.
- Se si usa una EC2 in lab: ricordarsi il **cleanup** (terminate).

## Checkpoint (fine prerequisiti)
- `git --version` funziona.
- Il repo è clonato e apribile in VS Code.
- (Opzionale) `aws --version` funziona.
