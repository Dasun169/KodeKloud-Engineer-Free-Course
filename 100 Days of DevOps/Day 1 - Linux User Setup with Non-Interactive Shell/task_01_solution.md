# Task 01 - Create User with Non-Interactive Shell on App Server 3

## Question

To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell.  
Your task is to create a user named **kirsty** with a non-interactive shell on **App Server 3**.

---

## Steps to Perform

### 1. Login via Jump Host

```bash
ssh thor@jump_host.stratos.xfusioncorp.com
# password: mjolnir123
```

### 2. Connect to App Server 3

```bash
ssh banner@stapp03.stratos.xfusioncorp.com
# password: BigGr33n
```

### 3. Create User with Non-Interactive Shell

```bash
sudo useradd -s /sbin/nologin kirsty
```

### 4. Verify User Creation

```bash
getent passwd kirsty
```

### Expected Output

```bash
kirsty:x:1001:1001::/home/kirsty:/sbin/nologin
```

## Explanation of Commands

### Command 1

```bash
sudo useradd -s /sbin/nologin kirsty
```

- sudo → run as superuser
- useradd → create new user
- -s /sbin/nologin → assigns a non-interactive shell, so user can’t log in (used for services/agents).

### Command 2

```bash
getent passwd kirsty
```

- getent → fetch system database entries
- passwd → user account database
- kirsty → check this user’s details (username, UID, home, shell).

## Shell Types

- Interactive shell → /bin/bash → allows login & typing commands.
- Non-interactive shell → /sbin/nologin → blocks login, but user still exists for system tasks.
