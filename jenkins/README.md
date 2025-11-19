# 🍂 Role: jenkins

## 🔧 Requirements / Variables
- **source_src**: `https://pkg.jenkins.io/redhat-stable/jenkins.repo`
- **source_dest**: `/etc/yum.repos.d/jenkins.repo`
- **rpm_key**: `https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key`
- **jenkins_port**: `8080`
- **java_path**: `/usr/lib/jvm/java-21-openjdk-21.0.8.0.9-1.el9.x86_64/bin/java`
- **web_server**:  
  - `172.16.6.121`  
  - `172.16.6.122`

## 🔐 Secrets
- **root_password**: `centos`

## ▶️ Example Playbook
```yaml
---
- name: "Configuring jenkins"
  hosts: jenkins
  vars_files:
    - root_password.yml
  tasks:
    - name: "Role - jenkins"
      ansible.builtin.include_role:
        name: jenkins

- name: "Install java"
  hosts: web_server
  tasks:
    - name: "Install packages"
      ansible.builtin.dnf:
        name: java-21-openjdk
        state: present

    - name: "Make java 32 bit an alternative with low priority"
      community.general.alternatives:
        name: java
        path: /usr/lib/jvm/java-21-openjdk-21.0.8.0.9-1.el9.x86_64/bin/java
