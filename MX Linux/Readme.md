Absolutely 👍
Below is a **very detailed, practical `README.md`** you can keep in your repo or personal notes.
It is written so that **future-you** (or anyone else) can reinstall Wealthfolio **from scratch** on **MX Linux (Debian-based)** and **Windows 11**, with **or without data restoration**.

You can copy–paste this directly into a `README.md`.

---

# Wealthfolio – Fresh Install & Reinstallation Guide

**MX Linux (Debian-based) & Windows 11**

This document explains how to **install, build, run, back up, and restore Wealthfolio** from scratch on both **MX Linux** and **Windows 11**.

Wealthfolio is a **local-first desktop application** built with **Tauri (Rust backend + React frontend)**.
It is **not a web app** and **cannot be hosted** on a server.

---

## Table of Contents

1. Overview & Architecture
2. System Requirements
3. Fresh Install on MX Linux
4. Running Wealthfolio (Linux)
5. Backing Up Data (Linux)
6. Reinstalling on MX Linux
7. Installing on Windows 11
8. Restoring Data on Windows
9. Common Pitfalls & FAQs
10. Recommended Safety Practices

---

## 1. Overview & Architecture

**Wealthfolio is local-first**:

* No cloud backend
* No remote sync
* No user accounts
* All data stored locally

### Tech stack

* **Frontend:** Vite + React
* **Backend:** Rust (Tauri)
* **Database:** SQLite
* **Market data:** Yahoo Finance (default)

---

## 2. System Requirements

### MX Linux / Debian 12+

* Node.js **20.x**
* pnpm **10.x**
* Rust (via `rustup`)
* System libraries for Tauri

### Windows 11

* Prebuilt installer **OR**
* Node.js 20+, pnpm, Rust, Visual Studio Build Tools

---

## 3. Fresh Install on MX Linux (Debian-based)

### 3.1 Install system dependencies

```bash
sudo apt update
sudo apt install -y \
  build-essential \
  pkg-config \
  libwebkit2gtk-4.1-dev \
  libglib2.0-dev \
  libgtk-3-dev \
  libayatana-appindicator3-dev \
  librsvg2-dev \
  libssl-dev \
  curl \
  wget \
  file
```

---

### 3.2 Install Node.js (v20)

Recommended: official NodeSource or nvm.

Verify:

```bash
node -v
```

Expected:

```
v20.x.x
```

---

### 3.3 Install pnpm

```bash
npm install -g pnpm
pnpm -v
```

Expected:

```
10.x.x
```

---

### 3.4 Install Rust (required for Tauri)

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
```

Verify:

```bash
cargo --version
```

---

### 3.5 Clone the repository

```bash
git clone https://github.com/Fanu2/wealthfolio.git
cd wealthfolio
```

---

### 3.6 Install dependencies

```bash
pnpm install
```

---

## 4. Running Wealthfolio (Linux)

### 4.1 Development mode (desktop app)

```bash
pnpm tauri dev
```

**Important:**

* Ignore `http://localhost:1420` in your browser
* Use the **desktop window**, not the browser
* Onboarding **only works in the desktop app**

First run may take **10–15 minutes** (Rust compilation).

---

### 4.2 Build production binaries (optional)

```bash
pnpm tauri build
```

Outputs:

* `.AppImage`
* `.deb`
* `.rpm`

---

## 5. Backing Up Data (Linux)

### 5.1 Data locations (Linux)

```text
~/.local/share/wealthfolio/
~/.config/wealthfolio/
```

These contain:

* SQLite database
* Accounts
* Transactions
* Settings

---

### 5.2 Create a backup archive

```bash
tar -czf wealthfolio-backup-$(date +%F).tar.gz \
  ~/.local/share/wealthfolio \
  ~/.config/wealthfolio
```

Store this file on:

* External drive
* Another computer
* Encrypted cloud storage

---

## 6. Reinstalling on MX Linux

1. Reinstall OS / clean system
2. Follow **Section 3** again
3. Install & run Wealthfolio once, then close it
4. Restore backup:

```bash
tar -xzf wealthfolio-backup-YYYY-MM-DD.tar.gz -C ~/
```

5. Start Wealthfolio:

```bash
pnpm tauri dev
```

Your data will reappear automatically.

---

## 7. Installing on Windows 11

### Option A (Recommended): Prebuilt installer

1. Download `.exe` or `.msi` from GitHub Releases
2. Install normally
3. Run Wealthfolio once, then close it

---

### Option B (Build from source – advanced)

Requires:

* Node.js 20+
* pnpm
* Rust
* Visual Studio Build Tools (C++ workload)

```powershell
pnpm install
pnpm tauri build
```

---

## 8. Restoring Data on Windows 11

### 8.1 Data locations (Windows)

```text
C:\Users\<YourName>\AppData\Local\wealthfolio\
C:\Users\<YourName>\AppData\Roaming\wealthfolio\
```

---

### 8.2 Restore steps

1. Extract `wealthfolio-backup.tar.gz`
2. Copy:

   * Linux `share/wealthfolio` → `AppData\Local\wealthfolio`
   * Linux `config/wealthfolio` → `AppData\Roaming\wealthfolio`
3. Overwrite if prompted
4. Launch Wealthfolio

---

## 9. Common Pitfalls & FAQs

### ❌ “Continue does nothing in browser”

Expected behavior.
Onboarding **only works in Tauri desktop app**.

---

### ❌ “AppImage doesn’t run”

Likely **glibc version mismatch**.
Use Tauri build or prebuilt Windows/Linux installers.

---

### ❌ “Data disappeared”

Check:

* Correct data directory
* Backup restored **after** first app run
* No downgrade in app version

---

### ⚠️ Version compatibility

* Upgrading Wealthfolio → safe
* Downgrading Wealthfolio → **not safe**

---

## 10. Recommended Safety Practices

### ✔ Backups

* Weekly manual backup
* Or daily automated backup (`rsync`, `restic`)

### ✔ Disk encryption

* LUKS (Linux)
* BitLocker (Windows)

### ✔ Treat like a password manager

Local-first = private, but **your responsibility**

---

## Final Notes

* Wealthfolio is **installed**, not deployed
* There is **no cloud sync**
* Desktop app is the **only supported runtime**
* Your data is yours — back it up

 Perfect choices 👍
I’ll give you **both** in a **practical, copy-paste-ready way**:

1️⃣ **A simple backup script (manual + automated)**
4️⃣ **Encrypted automatic backups (recommended, resilient)**

Everything below works on **MX Linux / Debian** and can be adapted to Windows later.

---

# 1️⃣ Simple Backup Script (Fast, Reliable, Zero Dependencies)

This is your **baseline safety net**.
Even if everything else fails, this saves you.

---

## 📁 What it backs up

* Wealthfolio database
* Settings & config

```text
~/.local/share/wealthfolio
~/.config/wealthfolio
```

---

## 📝 Create backup script

```bash
mkdir -p ~/scripts
nano ~/scripts/backup-wealthfolio.sh
```

Paste this **entire script**:

```bash
#!/usr/bin/env bash

set -e

BACKUP_DIR="$HOME/wealthfolio-backups"
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
BACKUP_FILE="$BACKUP_DIR/wealthfolio-backup-$TIMESTAMP.tar.gz"

mkdir -p "$BACKUP_DIR"

tar -czf "$BACKUP_FILE" \
  "$HOME/.local/share/wealthfolio" \
  "$HOME/.config/wealthfolio"

echo "✅ Wealthfolio backup created:"
echo "$BACKUP_FILE"
```

Save and exit.

---

## ▶ Make it executable

```bash
chmod +x ~/scripts/backup-wealthfolio.sh
```

---

## ▶ Run manually (test it now)

```bash
~/scripts/backup-wealthfolio.sh
```

You should see:

```
wealthfolio-backups/wealthfolio-backup-YYYY-MM-DD_HH-MM-SS.tar.gz
```

✅ This alone already protects you from:

* OS corruption
* accidental deletion
* failed upgrades

---

## ⏰ Optional: Run automatically (daily)

```bash
crontab -e
```

Add this line:

```bash
0 19 * * * /home/jasvir/scripts/backup-wealthfolio.sh
```

This runs **every day at 7 PM**.

---

# 4️⃣ Encrypted Automatic Backups (BEST PRACTICE)

This protects you against:

* disk failure
* ransomware
* laptop loss
* theft

We’ll use **restic** (battle-tested, fast, encrypted).

---

## 🔐 Why restic?

* End-to-end encryption
* Versioned backups
* Deduplication
* Corruption detection
* Easy restore

---

## 📦 Install restic

```bash
sudo apt install -y restic
```

---

## 📂 Choose backup location

Examples:

* External drive: `/mnt/backup`
* NAS
* Synced folder (Nextcloud, OneDrive, etc.)

Example:

```bash
mkdir -p /mnt/backup/restic
```

---

## 🔑 Initialize encrypted repository

```bash
restic init --repo /mnt/backup/restic
```

You’ll be prompted for a **password**.

⚠️ **Store this password somewhere safe.**
Without it, backups are unrecoverable.

---

## ▶ Run encrypted backup

```bash
restic -r /mnt/backup/restic backup \
  ~/.local/share/wealthfolio \
  ~/.config/wealthfolio
```

That’s it. Your data is now:

* encrypted
* versioned
* protected

---

## 🔄 Automate encrypted backups (daily)

Create script:

```bash
nano ~/scripts/backup-wealthfolio-restic.sh
```

Paste:

```bash
#!/usr/bin/env bash

export RESTIC_REPOSITORY="/mnt/backup/restic"
export RESTIC_PASSWORD="PUT_YOUR_PASSWORD_HERE"

restic backup \
  "$HOME/.local/share/wealthfolio" \
  "$HOME/.config/wealthfolio"

restic forget --keep-daily 7 --keep-weekly 4 --keep-monthly 6 --prune
```

⚠️ Replace `PUT_YOUR_PASSWORD_HERE`.

Make executable:

```bash
chmod +x ~/scripts/backup-wealthfolio-restic.sh
```

Add to cron:

```bash
crontab -e
```

```bash
0 20 * * * /home/jasvir/scripts/backup-wealthfolio-restic.sh
```

Now you have:

* daily backups
* encryption
* automatic cleanup
* zero manual work

---

## 🧪 Test restore (VERY IMPORTANT)

Never trust backups without testing.

### Restore to temp directory:

```bash
mkdir ~/wealthfolio-restore-test
restic restore latest --target ~/wealthfolio-restore-test
```

Verify files exist:

```bash
ls ~/wealthfolio-restore-test
```

If yes → **your backup system works** ✅

---

## 🧠 Recommended Setup (honest advice)

| Level  | Tool            | Purpose                    |
| ------ | --------------- | -------------------------- |
| Daily  | `tar.gz` script | Fast local recovery        |
| Daily  | restic          | Encrypted, off-disk safety |
| Weekly | External drive  | Disaster recovery          |

This is the same strategy used by:

* developers
* sysadmins
* crypto users

---

## 🔐 Final mental model

> Treat Wealthfolio like a **password manager or crypto wallet**
> Local-first = powerful, but backups are **non-optional**

---

## Want the next step?

I can help you:

* Sync backups to **Windows**
* Restore into **Windows Wealthfolio**
* Create **cross-platform export/import**
* Add **automatic cloud backup**
* Add **dev-mode onboarding bypass**

Just tell me 👍
👍
