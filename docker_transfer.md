# Nextcloud & PostgreSQL Docker Migration Guide (Windows 11)

This repository contains the configuration and documentation for running **Nextcloud** with a **PostgreSQL 16** backend inside Docker Desktop on Windows 11. It also includes an exact workflow for migrating your named Docker volumes safely between two physical machines.

## 🚀 Environment Stack
* **OS:** Windows 11 (with WSL2 backend)
* **Runtime:** Docker Desktop
* **App Container:** `nextcloud:latest`
* **DB Container:** `postgres:16-alpine`

## 📦 Docker Volumes Used
* `nextcloud_data` — Stores Nextcloud application configuration, code, and user-uploaded assets.
* `nextcloud_postgres` — Stores the persistent PostgreSQL database system files and transaction logs.

---

## 🚚 Step-by-Step Migration Guide

Follow these instructions to move your entire Nextcloud instance—complete with user settings, files, and database metadata—from your **Old PC** to your **New PC**.

### Phase 1: Source System Backup (Old PC)

1. **Stop the active containers** to prevent database writes and avoid data corruption during the backup process. Open **PowerShell** and run:
   ```powershell
   docker compose down
   ```
   *(Alternatively, run `docker stop <nextcloud-container>` and `docker stop <postgres-container>`).*

2. **Export the data volumes** using a lightweight, temporary container (`busybox`). This reads data inside the isolated WSL2 filesystem and compresses it into standard `.tar` archives on your Windows Desktop. Run these commands in **PowerShell**:
   ```powershell
   # Back up Nextcloud core application and user data files
   docker run --rm -v nextcloud_data:/volume -v \${HOME}\Desktop:/backup busybox tar cvf /backup/nextcloud_data.tar -C /volume .

   # Back up Postgres SQL server database assets
   docker run --rm -v nextcloud_postgres:/volume -v \${HOME}\Desktop:/backup busybox tar cvf /backup/nextcloud_postgres.tar -C /volume .
   ```

3. **Collect your artifacts**. You will now find `nextcloud_data.tar` and `nextcloud_postgres.tar` on your desktop.

### Phase 2: Transfer 
Move your two `.tar` backup files alongside your `docker-compose.yml` configuration script over to your new PC via an external storage drive, network share, or safe file-sharing medium.

### Phase 3: Target System Restore (New PC)

1. Ensure **Docker Desktop** is installed and actively running on your new Windows 11 machine.
2. Place `nextcloud_data.tar` and `nextcloud_postgres.tar` onto the **Desktop** of the new PC.
3. Open **PowerShell** and create empty container volumes targeting the exact original naming framework:
   ```powershell
   docker volume create nextcloud_data
   docker volume create nextcloud_postgres
   ```
4. Extract the compressed tarballs into your newly established volumes using the helper runtime container:
   ```powershell
   # Restore Nextcloud Application data
   docker run --rm -v nextcloud_data:/volume -v \${HOME}\Desktop:/backup busybox tar xvf /backup/nextcloud_data.tar -C /volume

   # Restore Postgres Database data
   docker run --rm -v nextcloud_postgres:/volume -v \${HOME}\Desktop:/backup busybox tar xvf /backup/nextcloud_postgres.tar -C /volume
   ```

### Phase 4: Spin Up and Re-verify
1. Navigate to the directory hosting your `docker-compose.yml` configuration script on the new PC.
2. Initialize your application environment in detached mode:
   ```powershell
   docker compose up -d
   ```

---

## 🛠 Troubleshooting: Trusted Domains Error

Because your new PC runs on a different local IP address or local hostname, Nextcloud might block your access with an **"Access through untrusted domain"** security error. 

To resolve this instantly, add your new host IP address to Nextcloud's internal system architecture configuration:

```powershell
docker exec --user www-data <YOUR_NEXTCLOUD_CONTAINER_NAME> php occ config:system:set trusted_domains 2 --value="YOUR_NEW_PC_IP"
```
*Replace `<YOUR_NEXTCLOUD_CONTAINER_NAME>` with the active container name and `YOUR_NEW_PC_IP` with your new computer's local network IP.*
