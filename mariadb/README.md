# 🪶 Role: mariadb

## 🔧 Role Variables
- **mariadb_port**: `3306`
- **mariadb_datadir**: `/data`

## 🔐 Secrets
- **root_password**: `centos`

## ▶️ Example Playbook
```yaml
---
- name: "Configuring mariadb"
  hosts: database
  vars_files:
    - ./root_password.yml
  tasks:
    - name: "Role - mariadb"
      ansible.builtin.include_role:
        name: mariadb
