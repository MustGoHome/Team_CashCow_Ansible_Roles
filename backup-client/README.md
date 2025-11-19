# 🌿 Role: backup-client

## 🔧 Role Variables
- **backup_server**: `172.16.6.76`
- **borg_user**: `borg`
- **borg_group**: `borg`
- **backup_dir**: `/data`

## 🔐 Secrets
- **user_password**: `borg`

## ▶️ Example Playbook
```yaml
---
- name: "Set borgbackup client"
  hosts: backup-client, localhost
  vars_files:
    - backup_password.yml
  tasks:
    - name: "Role - backup-client"
      ansible.builtin.include_role:
        name: backup-client
