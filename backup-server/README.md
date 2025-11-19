# ☘️ Role: backup-server

## ▶️ Example Playbook
```yaml
---
- name: "Set borgbackup server"
  hosts: backupserver
  vars_files:
    - bakcup_password.yml
  tasks:
    - name: "Role - backup-server"
      ansible.builtin.include_role:
        name: backup-server
