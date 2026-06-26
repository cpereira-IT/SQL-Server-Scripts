
# Restore Database with RECOVERY (SQL Server)

This repository contains a SQL Server script that completes a database restore operation by bringing the database online using the `WITH RECOVERY` option.

---

## 📌 Purpose

The `WITH RECOVERY` option is used as the **final step** in a database restore sequence. It instructs SQL Server to:

- Roll back any uncommitted transactions.
- Complete the restore process.
- Bring the database online.
- Make the database available for users and applications.

---

## 📂 Script Included

| Script | Description |
|---------|-------------|
| `Restore_Database_With_Recovery.sql` | Completes the restore process and brings the database online. |

---

## 📜 Script

```sql
USE master;
GO

RESTORE DATABASE NextlyDigiBank_MetaDB
WITH RECOVERY;
GO
```

---

## 🚀 When to Use

Use this script when:

- The database is in the **Restoring** state.
- All Full, Differential, and Transaction Log backups have already been restored.
- You want to complete the restore process and make the database accessible.

---

## 🔄 Typical Restore Process

### Step 1 – Restore Full Backup

```sql
RESTORE DATABASE NextlyDigiBank_MetaDB
FROM DISK = 'D:\Backup\Full.bak'
WITH NORECOVERY;
```

### Step 2 – Restore Differential Backup (Optional)

```sql
RESTORE DATABASE NextlyDigiBank_MetaDB
FROM DISK = 'D:\Backup\Diff.bak'
WITH NORECOVERY;
```

### Step 3 – Restore Transaction Log Backup(s)

```sql
RESTORE LOG NextlyDigiBank_MetaDB
FROM DISK = 'D:\Backup\Log1.trn'
WITH NORECOVERY;
```

### Step 4 – Complete the Restore

```sql
RESTORE DATABASE NextlyDigiBank_MetaDB
WITH RECOVERY;
```

---

## ⚠️ Important Notes

- `WITH NORECOVERY` keeps the database in the **Restoring** state.
- Use `WITH RECOVERY` **only after** all required backups have been restored.
- Once `WITH RECOVERY` is executed, no additional transaction log backups can be restored unless the restore process is restarted.

---

## ✅ Requirements

- Microsoft SQL Server
- Appropriate permissions to restore databases (`sysadmin` or `dbcreator` with restore permissions)

---

## 👨‍💻 Author

**Cresjowell Pereira**

**Role:** Senior System Administrator L1

---

## 📄 License

This project is shared for learning and reference purposes.
