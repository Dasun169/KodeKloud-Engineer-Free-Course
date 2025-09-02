# Task 07

## Question

The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following: Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

---

## Explanation

You are on the Jump Host as user thor.
The company has scripts on the Jump Host that need to connect to all App Servers automatically.
To avoid typing passwords every time, you must configure password-less SSH authentication.
Requirement: thor@jump_host must be able to SSH into each App Server using its respective sudo user:
tony@stapp01
steve@stapp02
banner@stapp03
This is achieved using SSH key-based authentication.

---

## Steps to Perform

### Step 1: Switch to thor (if not already on Jump Host)

```bash
ssh thor@jump_host.stratos.xfusioncorp.com
# password: mjolnir123
```

### Step 2: Generate SSH Key Pair (as thor)

```bash
ssh-keygen -t rsa -b 2048
```

Press Enter for default file (/home/thor/.ssh/id_rsa)
Don’t set a passphrase (just press Enter twice).

This creates:
Private key → /home/thor/.ssh/id_rsa
Public key → /home/thor/.ssh/id_rsa.pub

### Step 3: Copy Key to App Server 1

```bash
ssh-copy-id tony@stapp01.stratos.xfusioncorp.com
# password: Ir0nM@n
```

### Step 4: Copy Key to App Server 2

```bash
ssh-copy-id steve@stapp02.stratos.xfusioncorp.com
# password: Am3ric@
```

### Step 5: Copy Key to App Server 3

```bash
ssh-copy-id banner@stapp03.stratos.xfusioncorp.com
# password: BigGr33n
```

### Step 6: Test Password-less Login

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
ssh steve@stapp02.stratos.xfusioncorp.com
ssh banner@stapp03.stratos.xfusioncorp.com
```

You should log in without being asked for a password.
