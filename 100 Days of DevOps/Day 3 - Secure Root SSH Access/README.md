# Task 03 - Disable Direct Root SSH Login on App Servers

## Question

Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.
Your task is to disable direct SSH root login on **all app servers** within the Stratos Datacenter.

---

## Steps to Perform

### 1. Login via Jump Host

```bash
ssh thor@jump_host.stratos.xfusioncorp.com
# password: mjolnir123
```

### 2. Connect to Each App Server

(Example shown for stapp01, repeat for other app servers)

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
# password: Ir0nM@n
```

### 3. Edit SSH Configuration File

Open the SSH daemon config file:

```bash
sudo vi /etc/ssh/sshd_config
```

Find the line:

```bash
#PermitRootLogin yes
```

Modify it to:

```bash
PermitRootLogin no
```

### 4. Save & Exit (in vi editor)

```bash
Esc → :wq → Enter
```

### 5. Restart SSH Service

```bash
sudo systemctl restart sshd
```

### 6. Verify Configuration

```bash
sudo sshd -T | grep permitrootlogin
```

Expected Output:

```bash
permitrootlogin no
```

### ✅ Task Complete

Repeat the same steps for stapp02 and stapp03 to ensure direct root SSH login is disabled across all app servers.
