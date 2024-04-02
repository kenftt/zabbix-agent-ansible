# zabbix-agent-ansible
Ansible playbooks and configuration templates to deploy and configure a Zabbix Agent on Linux. 

## Prerequisites

- Ansible 2.9 or later.
- Access to one or more Linux servers where Zabbix Agent will be installed.
- A configured Zabbix server to accept and process data from agents.

## Getting started
### 1. Clone the Repository
```bash
git clone https://github.com/kenftt/zabbix-agent-ansible.git
cd zabbix-agent-ansible
```

### 2. Configure Ansible inventory
Edit the ``` hosts.ini ``` file to list your target servers with their IP addresses or hostnames.

### 3. Secure SSH keys and Sudo password with Ansible Vault

#### a. Generate SSH key pair
If not already done, generate an SSH key pair with RSA encryption and a bit length of 4096:
```bash
ssh-keygen -t rsa -b 4096
```
#### b. Copy public key to target host
Copy the public key to the target host (zabbix-host) using ssh-copy-id:

```bash
ssh-copy-id <username>@zabbix-host
```
Replace `<username>` with the appropriate username on the remote host if different.
#### c. Manage Sudo password with Ansible Vault

Create a file named `secret.yml` using Ansible Vault to store the sudo password:
```bash
ansible-vault create secret.yml
```
Inside `secret.yml`, add the following YAML content, replacing `<YourSudoPassword>` with the actual sudo password:
```yaml
ansible_become_password: <YourSudoPassword>
```
Remember to keep the `secret.yml` file secure and do not expose it to unauthorized users.

### 4. Run Playbook with Ansible Vault
```bash
ansible-playbook -i hosts.ini install-zabbix-agent.yml --ask-vault-pass
```
This command will prompt you to enter the vault password (`secret.yml`) before executing the playbook.
