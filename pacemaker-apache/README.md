# 🍁 Role: pacemaker-apache

## 🔧 Role Variables
- **cluster_host**:  
  - `web01.hb05.local`  
  - `web02.hb05.local`
- **cluster_vm**:  
  - `web01`  
  - `web02`
- **vcenter_ip**: `172.16.6.74`
- **vcenter_port**: `443`
- **vcenter_user**: `administrator@hb05.local`
- **ssl_insecure**: `1`
- **iscsi_device**: `/dev/sdb`
- **iscsi_directory**: `/data`
- **cluster_vip**: `172.16.6.123`
- **cluster_nic**: `ens192`
- **cluster_group**: `apache_group`
- **cluster_apache_port**: `80`

## 🔐 Secrets
- **vcenter_password**: `Soldesk1.`

## ▶️ Example Playbook
```yaml
- name: "Configuring apache cluster"
  hosts: web
  vars_files:
    - ./vcenter_password.yml
  tasks:
    - name: "Role - pacemaker-apache"
      ansible.builtin.include_role:
        name: pacemaker-apache
