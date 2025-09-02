# Task 09

## Question

There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.

---

## Explanation

The Nautilus application in the Stratos Datacenter is facing a critical issue.
Symptom: The application cannot connect to the database.
Investigation: The production support team found that the MariaDB service is down on the database server (stdb01).
Your task is to check why MariaDB is down and fix it so that the Nautilus application can connect to the database again.

---

## Steps to Perform

### Step 1: Access the Database Server

```bash
ssh peter@stdb01.stratos.xfusioncorp.com
# password: Sp!dy
```

### Step 2: Check MariaDB Service Status

```bash
sudo systemctl status mariadb
```

Possible outputs:
active (running) → service is fine (the issue might be elsewhere)
inactive (dead) or failed → service is down → proceed to restart

### Step 3: Restart MariaDB Service

```bash
sudo systemctl restart mariadb
```

Check status again:

```bash
sudo systemctl status mariadb
```

### Step 4: Check for Errors

If the service fails to start, check the logs:

```bash
sudo journalctl -xe
sudo tail -n 50 /var/log/mariadb/mariadb.log
```

### Step 5: Understanding the Error

From the log:
[ERROR] mariadbd: Can't create/write to file '/run/mariadb/mariadb.pid' (Errcode: 13 "Permission denied")
[ERROR] Can't start server: can't create PID file: Permission denied

### What this means:

MariaDB tries to create a PID file (/run/mariadb/mariadb.pid) to keep track of its running process.
Errcode 13 "Permission denied" → MariaDB does not have permission to write to this folder.
As a result, the service fails to start.
This is a common permission issue on the /run/mariadb directory.

## Step-by-Step Fix:

### Step 1: Check Ownership and Permissions

```bash
ls -ld /run/mariadb
```

You’ll likely see something like:
drwxr-xr-x 2 mysql root 40 Aug 22 08:00 /run/mariadb
Owner is root → MariaDB runs as mysql user, so it cannot write.

### Step 2: Fix Ownership

Set the correct ownership to mysql:mysql (MariaDB user):

```bash
sudo chown mysql:mysql /run/mariadb
```

Verify:

```bash
ls -ld /run/mariadb
```

Output should now show:

```bash
drwxr-xr-x 2 mysql mysql 40 Aug 22 08:00 /run/mariadb
```

### Step 3: Restart MariaDB

```bash
sudo systemctl restart mariadb
```

Check status:

```bash
sudo systemctl status mariadb
```

It should show:

```bash
Active: active (running)
```
