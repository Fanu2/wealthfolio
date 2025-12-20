
# 📦 Wealthfolio Backup & Restore Guide

This document explains **how to safely back up and restore Wealthfolio data** across systems, including **MX Linux** and **Windows 11**.

Wealthfolio is a **local-first application** — all your data lives **on your computer**, not in the cloud.

---

## ⚠️ IMPORTANT CONCEPTS (READ FIRST)

* Wealthfolio **does NOT auto-sync**
* Reinstalling the app **does NOT restore data**
* Uninstalling **may delete local data**
* Backups are **your responsibility**

> Treat Wealthfolio like a local accounting ledger.

---

## 🧠 What is backed up?

Your backup contains:

* Accounts (Cash, Equity, MF, etc.)
* Transactions
* Holdings
* Snapshots & performance history
* Settings & preferences
* Goals and allocations

It does **NOT** contain:

* App binaries
* Market data cache (re-fetched automatically)

---

## 📁 Backup Locations

### 🐧 MX Linux / Linux

Default data directory:

```bash
~/.local/share/wealthfolio/
```

Typical contents:

```
wealthfolio/
├── db.sqlite
├── snapshots/
├── settings.json
├── logs/
```

---

### 🪟 Windows 11

Default data directory:

```text
C:\Users\<your-username>\AppData\Roaming\wealthfolio\
```

To open quickly:

1. Press `Win + R`
2. Type:

   ```
   %APPDATA%\wealthfolio
   ```
3. Press Enter

---

## 🔐 How to Take a Backup (SAFE METHOD)

### ✅ Step 1: Close Wealthfolio completely

Make sure the app is **not running**.

---

### ✅ Step 2: Copy the data folder

#### On MX Linux

```bash
cp -r ~/.local/share/wealthfolio ~/Documents/wealthfolio-backup-$(date +%F)
```

Or using file manager:

* Enable **Show Hidden Files**
* Copy the entire `wealthfolio` folder

---

#### On Windows 11

* Navigate to:

  ```
  %APPDATA%\wealthfolio
  ```
* Copy the entire `wealthfolio` folder
* Paste it somewhere safe (Documents / External drive)

---

### ✅ Step 3: (Recommended) Compress the backup

#### Linux

```bash
tar -czvf wealthfolio-backup.tar.gz wealthfolio/
```

#### Windows

* Right-click → **Send to → Compressed (zipped) folder**

---

## ☁️ Where to Store Backups (Recommended)

* External USB drive
* Encrypted cloud storage (Google Drive, OneDrive, etc.)
* Another computer

> ❗ Never keep your **only backup** on the same disk.

---

## 🔄 Restore Backup (Fresh Install or New System)

### ⚠️ Before restoring

* Install Wealthfolio first
* Run it **once**
* Close it completely

This creates the required folder structure.

---

### 🔁 Restore on MX Linux

```bash
rm -rf ~/.local/share/wealthfolio
cp -r wealthfolio ~/.local/share/
```

Ensure permissions:

```bash
chmod -R 700 ~/.local/share/wealthfolio
```

---

### 🔁 Restore on Windows 11

1. Close Wealthfolio
2. Go to:

   ```
   %APPDATA%
   ```
3. Delete the existing `wealthfolio` folder
4. Paste your backed-up `wealthfolio` folder
5. Launch Wealthfolio

---

## ✅ Post-Restore Checklist

After restoring:

* Open Wealthfolio
* Wait 1–2 minutes (market data & snapshots rebuild)
* Verify:

  * Accounts appear
  * Holdings visible
  * MF NAVs load
  * Balance Sheet populates

⚠️ First launch may appear slow — this is normal.

---

## 🧪 Verify Backup Integrity (Optional but Smart)

Check for:

* `db.sqlite` file exists
* Folder size is non-zero
* Date modified matches backup date

---

## 🚫 What NOT to Do

❌ Do not restore while Wealthfolio is running
❌ Do not mix partial folders
❌ Do not edit database manually
❌ Do not rely on reinstall for recovery

---

## 🔁 Backup Frequency (Best Practice)

| Usage              | Backup Frequency |
| ------------------ | ---------------- |
| Active investing   | Weekly           |
| Long-term tracking | Monthly          |
| Major changes      | Before & after   |
| System updates     | Before upgrade   |

---

## 🆘 Recovery Scenarios

### If system crashes

➡ Restore from backup → full recovery

### If app breaks after update

➡ Reinstall → restore backup

### If switching OS (Linux → Windows)

➡ Manual copy → works perfectly

---

## 🧭 Final Notes

* Wealthfolio backups are **portable**
* Linux ↔ Windows restore works
* No export/import needed
* Data format is stable across versions

---

## ✅ TL;DR

> **Backup = copy the `wealthfolio` folder while app is closed**
> **Restore = replace that folder after install**

---

If you want, I can also:

* Create a **one-command backup script**
* Help you automate backups
* Explain **snapshot vs live data**
* Help verify your existing backup

Just tell me 👍

