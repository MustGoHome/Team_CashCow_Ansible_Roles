# 🪴 Role: pacemaker-mariadb

## 🔧 Role Variables
- **cluster_host**:  
  - `db01.hb05.local`  
  - `db02.hb05.local`
- **cluster_vm**:  
  - `db01`  
  - `db02`
- **vcenter_ip**: `172.16.6.74`
- **vcenter_port**: `443`
- **vcenter_user**: `administrator@hb05.local`
- **ssl_insecure**: `1`
- **iscsi_device**: `/dev/sdb`
- **iscsi_directory**: `/data`
- **cluster_vip**: `172.16.6.126`
- **cluster_nic**: `ens192`
- **cluster_group**: `mariadb_group`

## 🔐 Secrets
- **vcenter_password**: `Soldesk1.`

## ▶️ Example Playbook
```yaml
---
- name: "Configuring mariadb cluster"
  hosts: db01.hb05.local
  vars_files:
    - ./vcenter_password.yml
  tasks:
    - name: "Role - pacemaker-mariadb"
      ansible.builtin.include_role:
        name: pacemaker-mariadb
    
    - name: "Update directory owner"
      ansible.builtin.file:
        path: "/data"
        state: directory
        owner: mysql
        group: mysql
        recurse: yes
