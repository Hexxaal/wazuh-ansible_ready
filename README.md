# Wazuh Single-Node Docker Ansible Project

## Overview
This Ansible project deploys Wazuh in single-node Docker using the wazuh-docker repo (v4.12.0) and configures HTTPS with a Cloudflare Origin CA certificate.

## Vault Setup
Encrypt your Cloudflare Origin CA certs and key with your existing vault password file:
```bash
ansible-vault encrypt_string '<your PEM certificate>' --name 'cloudflare_origin_cert' --vault-password-file /home/dimitri/.vault_pass.txt
ansible-vault encrypt_string '<your PEM private key>' --name 'cloudflare_origin_key' --vault-password-file /home/dimitri/.vault_pass.txt
```
This will update `group_vars/all/vault.yml` with encrypted variables.

## Usage
1. Install dependencies:
   ```bash
   ansible-galaxy collection install community.docker
   ```
2. Run the playbook:
   ```bash
   ansible-playbook playbook.yml --vault-password-file /home/dimitri/.vault_pass.txt
   ```

## Variables
- `wazuh_repo_dest`: Path where wazuh-docker is cloned (default `/opt/wazuh-docker`).
- `cloudflare_origin_cert` & `cloudflare_origin_key`: Certificate and key injected via Vault.
