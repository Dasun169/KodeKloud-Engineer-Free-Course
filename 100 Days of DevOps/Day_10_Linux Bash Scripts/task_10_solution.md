# Task 10

## Question

The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter, and they need to create a bash script named ecommerce_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).

a. Create a zip archive named xfusioncorp_ecommerce.zip of /var/www/html/ecommerce directory.
b. Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.
c. Copy the created archive to Nautilus Backup Server server in /backup/ location.
d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

Note:
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. You can install it either manually or through the bash script as needed.

---

## Explanation

This task requires creating a bash script named ecommerce_backup.sh on App Server 2 under /scripts/ to automate website backups. The website is located at /var/www/html/ecommerce.

The script should:
Compress the website into a zip file named xfusioncorp_ecommerce.zip.
Store the zip locally in /backup/ on App Server 2. This is temporary storage cleared weekly.
Copy the backup to Nautilus Backup Server (stbkp01) under /backup/ for long-term storage.
Ensure passwordless copying using SSH keys so the script can run automatically without prompting for a password.
Additionally, the script must check whether the zip package is installed, installing it if missing.

In short, this task automates the backup process: compressing website files, saving them locally, transferring them securely to a backup server, and allowing unattended execution. This ensures both short-term and long-term backup availability while enabling full automation and operational efficiency.

---

## Steps to Perform

### 1. Make sure directories exist On stapp02:

```bash
sudo mkdir -p /scripts
sudo mkdir -p /backup
```

### 2. Create the script /scripts/ecommerce_backup.sh

Run:

```bash
sudo vi /scripts/ecommerce_backup.sh
```

Type this line by line inside vi (press i to insert):

```bash
#!/bin/bash
# Variables
SRC_DIR="/var/www/html/ecommerce"
BACKUP_DIR="/backup"
BACKUP_NAME="xfusioncorp_ecommerce.zip"
REMOTE_USER="clint"
REMOTE_HOST="stbkp01.stratos.xfusioncorp.com"
REMOTE_DIR="/backup"
```

### Step 1: Ensure zip is installed

```bash
if ! command -v zip &> /dev/null
then
    echo "zip not found, installing..."
    sudo yum install -y zip || sudo apt-get install -y zip
fi
```

### Step 2: Create local backup

```bash
echo "Creating backup..."
zip -r "${BACKUP_DIR}/${BACKUP_NAME}" "$SRC_DIR"
```

### Step 3: Copy to Backup Server

```bash
echo "Copying backup to Nautilus Backup Server..."
scp -o StrictHostKeyChecking=no "${BACKUP_DIR}/${BACKUP_NAME}" ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}/

if [ $? -eq 0 ]; then
    echo "Backup successfully copied to ${REMOTE_HOST}:${REMOTE_DIR}"
else
    echo "Backup copy failed!"
    exit 1
fi
```

Save and exit:
Press Esc → type :wq → press Enter.

### 3. Set permissions

```bash
sudo chmod +x /scripts/ecommerce_backup.sh
sudo chown steve:steve /scripts/ecommerce_backup.sh
```

### 4. Enable passwordless SSH (important)

Run on stapp02 as steve

```bash
ssh-keygen -t rsa -b 2048
ssh-copy-id clint@stbkp01.stratos.xfusioncorp.com
```

Test:

```bash
ssh clint@stbkp01.stratos.xfusioncorp.com
```

➡️ It should log in without asking password.

### 5. Run the script

On stapp02:

```bash
/scripts/ecommerce_backup.sh
```

Check:

```bash
ls -l /backup/xfusioncorp_ecommerce.zip   # on stapp02
```

and on backup server:

```bash
ls -l /backup/xfusioncorp_ecommerce.zip   # on stbkp01
```

✅ Done! You now have an automated backup script for App Server 2.
