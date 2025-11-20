# 🧩 Role: borgmatic-client

## 🔧 Role Variables
- **backup_server**: `192.168.10.10`
- **borg_encryption**: `repokey`
- **backup_dir**: `/data`
- **borg_passphrase**: `borg`
- **borg_user**: `borg`
- **borg_group**: `borg`

## 🔐 Secrets
- **user_password**: `centos`

## ▶️ Example Playbook
```yaml
---
- name: 'Set borgmatic client'
  hosts: backup-client
  vars_files:
    - backup_password.yml
  tasks:
    - name: 'Role - borgmatic-client'
      ansible.builtin.include_role:
        name: borgmatic-client