# 🪶 Role: apache

## 🔧 Role Variables
- **apache_listen**: `80`
- **apache_name**: `"apache.example.com:{{ apache_listen }}"`
- **web_dir**: `/data`

## ▶️ Example Playbook
```yaml
---
- name: 'Configuring apache'
  hosts: web01.hb05.local
  tasks:
    - name: 'Role - apache'
      ansible.builtin.include_role:
        name: apache