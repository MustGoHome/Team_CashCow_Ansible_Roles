# 🪸 Role: prometheus

## ⚠️ Requirements

- Apache `/server-status` 경로 사전 설정 필요

## 🔧 Role Variables

- **prometheus_account**: `prometheus`
- **exporter_packages**: Node exporter 다운로드 URL
- **exporter_service**: `node-exporter`
- **base_dir**: `node_exporter-1.10.2.linux-amd64`
- **exporter_directory**: `/usr/local/prometheus-{{ exporter_service }}`
- **exporter_port**: `9100`
- **mysql_user**: `prometheus`
- **mysql_pass**: `centos`
- **option_key**: `0` # 0=node exporter, 1=mysql exporter, 2=apache exporter, 3=prometheus server
- **targets**:
  - name: node_exporter
    ip: 192.168.10.30
    port: 9100
    app_label: '[node] mariadb.example.com'
  - name: mysql_exporter
    ip: "192.168.10.30"
    port: 9104
    app_label: '[mysql] mariadb.example.com'
  - name: mysql_exporter
    ip: 192.168.10.10
    port: 9100
    app_label: '[node] web.example.com'
  - name: apache_exporter
    ip: 192.168.10.10
    port: 9117
    app_label: '[apache] web.example.com'

## 🔐 Secrets

- None defined

## ▶️ Example Playbook

```yaml
---
- name: 'Install node exporter'
  hosts: node-exporter
  tasks:
    - name: 'Role - prometheus'
      ansible.builtin.include_role:
        name: prometheus
      vars:
        exporter_packages: https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz
        exporter_service: node-exporter
        base_dir: node_exporter-1.10.2.linux-amd64
        exporter_port: 9100
        option_key: 0

- name: 'Install mysql exporter'
  hosts: mysql-exporter
  tasks:
    - name: 'Role - prometheus'
      ansible.builtin.include_role:
        name: prometheus
      vars:
        exporter_packages: https://github.com/prometheus/mysqld_exporter/releases/download/v0.18.0/mysqld_exporter-0.18.0.linux-amd64.tar.gz
        exporter_service: mysql-exporter
        base_dir: mysqld_exporter-0.18.0.linux-amd64
        exporter_port: 9104
        mysql_user: prometheus
        mysql_pass: centos
        option_key: 1

- name: 'Install apache exporter'
  hosts: apache-exporter
  tasks:
    - name: 'Role - prometheus'
      ansible.builtin.include_role:
        name: prometheus
      vars:
        exporter_packages: https://github.com/Lusitaniae/apache_exporter/releases/download/v0.11.0/apache_exporter-0.11.0.linux-amd64.tar.gz
        exporter_service: apache-exporter
        base_dir: apache_exporter-0.11.0.linux-amd64
        exporter_port: 9117
        option_key: 2

- name: 'Install prometheus server'
  hosts: prometheus-server
  vars_files:
    - ./exporter_target.yml
  tasks:
    - name: 'Role - prometheus'
      ansible.builtin.include_role:
        name: prometheus
      vars:
        exporter_packages: https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz
        exporter_service: prometheus
        base_dir: prometheus-3.5.0.linux-amd64
        exporter_directory: /usr/local/prometheus
        exporter_port: 9090
        option_key: 3

- name: 'Install redis exporter'
  hosts: redis-exporter
  tasks:
    - name: 'Role - prometheus'
      ansible.builtin.include_role:
        name: prometheus
      vars:
        exporter_packages: https://github.com/oliver006/redis_exporter/releases/download/v1.80.0/redis_exporter-v1.80.0.linux-amd64.tar.gz
        exporter_service: redis-exporter
        base_dir: redis_exporter-v1.80.0.linux-amd64
        exporter_port: 9121
        option_key: 4
```
