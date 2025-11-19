# 🐧 Role: pacemaker

## 🔧 Role Variables
- **cluster_host**:  
  - `web01.hb05.local`  
  - `web02.hb05.local`

## 🔐 Secrets
- **hacluster_password**: `redhat`

## ▶️ Example Playbook
```yaml
---
- name: "Configure pacemaker cluster"
  hosts: web
  vars_files:
    - cluster_password.yml
  tasks:
    - name: "Role - pacemaker"
      ansible.builtin.include_role:
        name: pacemaker

- name: "Configure database cluster"
  hosts: database
  vars_files:
    - cluster_password.yml
  tasks:
    - name: "Role - pacemaker"
      ansible.builtin.include_role:
        name: pacemaker
      vars:
        cluster_host:
          - db01.hb05.local
          - db02.hb05.local
