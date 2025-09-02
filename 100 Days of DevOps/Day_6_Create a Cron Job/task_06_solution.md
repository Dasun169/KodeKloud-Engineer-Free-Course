# Task 06

## Question

The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below: a. Install cronie package on all Nautilus app servers and start crond service. b. Add a cron _/5 _ \* \* \* echo hello > /tmp/cron_text for root user.

---

## Steps to Perform

### Step 1: SSH into Each App Server

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
ssh steve@stapp02.stratos.xfusioncorp.com
ssh banner@stapp03.stratos.xfusioncorp.com
```

### Step 2: Install cronie

For each server:

```bash
sudo yum install -y cronie
```

### Step 3: Start and Enable crond Service

```bash
sudo systemctl start crond
sudo systemctl enable crond
sudo systemctl status crond
```

### Step 4: Edit Root’s Crontab

```bash
sudo crontab -e
```

Add the following line at the bottom:(using i,esc,:wq)

```bash
*/5 * * * * echo hello > /tmp/cron_text
```

### Step 5: Verify Cron Job

```bash
sudo crontab -l
```
