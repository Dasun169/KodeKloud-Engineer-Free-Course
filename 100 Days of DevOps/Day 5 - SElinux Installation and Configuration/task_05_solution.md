# Task 05

## Question

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 1 in the Stratos Datacenter:

Install the required SELinux packages.
Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

---

## Steps to Perform

### Step 1: Connect to App Server 1 from jump server

```bash
ssh tony@stapp01.stratos.xfusioncorp.com
# password: Ir0nM@n
```

### Step 2: Install SELinux Packages

```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```

### Step 3: Edit SELinux Config File

```bash
sudo vi /etc/selinux/config
```

Press i (to enter insert mode).
Find the line:
SELINUX=enforcing

Change it to:
SELINUX=disabled
Press Esc, then type:
:wq
and hit Enter (to save and exit).
