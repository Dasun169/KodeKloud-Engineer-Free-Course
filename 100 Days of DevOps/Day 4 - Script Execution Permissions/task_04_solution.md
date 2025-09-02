# Task 04

## Question

In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 3 within the Stratos Datacenter.
Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 3. Additionally, ensure that all users have the capability to execute it.

---

## Steps to Perform

### Step 1: Connect to the Jump Server First

```bash
ssh thor@jump_host.stratos.xfusioncorp.com
```

### Step 2: SSH into App Server 1 (stapp01):

```bash
ssh tony@stapp01
```

### Step 3: The simplest way to add executable permission for all is to use the a+rx mode.

```bash
sudo chmod a+rx /tmp/xfusioncorp.sh
```

### Step 4: Verify the New Permissions

```bash
ls -l /tmp/xfusioncorp.sh
```
