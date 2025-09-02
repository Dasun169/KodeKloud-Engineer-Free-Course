# Task 08

## Question

During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.
Install ansible version 4.7.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

---

## Explanation

You are on the jump host (main server).
The DevOps team wants to use Ansible (a tool for automation/configuration).
They want version 4.7.0 specifically.
You must install it using pip3 (Python package manager).
After installation, the ansible command should be available globally (so any user on the system can run it).

---

## Steps to Perform

### 1. Update system packages (optional but good practice)

```bash
sudo yum update -y     # On RHEL/CentOS
```

### 2. Install Python3 and pip3 if not already installed

```bash
# For CentOS/RHEL
sudo yum install -y python3 python3-pip
```

### 3. Install Ansible 4.7.0 using pip3

```bash
sudo pip3 install ansible==4.7.0
```

### 4. Verify installation

```bash
ansible --version
```

### 5. Make Ansible globally available

```bash
sudo ln -s /usr/local/bin/ansible /usr/bin/ansible
```
