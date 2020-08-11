# Ansible Role: Jenkins-Slave

Installs jenkins slave jnlp service on Debian/Ubuntu or Windows/Windows Core.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
# jenkins master
jenkins_master_url: http://127.0.0.1:8080
jenkins_master_username: admin
jenkins_master_password_or_token: admin

# jenkins slave
jenkins_slave_username: jenkins
jenkins_slave_password: jenkins
jenkins_slave_node_name: "{{ inventory_hostname_short }}"
jenkins_slave_java_opts: ""

# linux server
jenkins_slave_home: /opt/jenkins
# windows server
jenkins_slave_home: C:/Jenkins
```

`jenkins_master_url` is the URL of your jenkins site.

`jenkins_master_username` is the login username of your jenkins user.

`jenkins_master_password_or_token` is the login password or api token of your jenkins user.

`jenkins_slave_username` is the jenkins slave account username on jenkins slave machine.

`jenkins_slave_password` is the jenkins slave account password on jenkins slave machine.

`jenkins_slave_node_name` is the node name of this jenkins slave. Default is the hostname defined in inventory file.

`jenkins_slave_java_opts` is the java options when run jenkins slave service.

`jenkins_slave_home` in linux server default is `/opt/jenkins`, in windows server default is `C:/Jenkins`.

## Dependencies

None.

## Inventory example

```
[jenkins_slave_linux]
jenkins-slave-linux-01 ansible_host=192.168.56.11 ansible_user='vagrant' ansible_password='vagrant' jenkins_slave_node_name=jenkins-slave-linux-01

[jenkins_slave_windows]
jenkins-slave-windows-01 ansible_host=192.168.56.12 ansible_user='vagrant' ansible_password='vagrant' jenkins_slave_node_name=jenkins-slave-windows-01

[jenkins_slave:children]
jenkins_slave_linux
jenkins_slave_windows

[jenkins_slave_linux:vars]
ansible_port=22
ansible_python_interpreter=/usr/bin/python3
jenkins_slave_home=/opt/jenkins

[jenkins_slave_windows:vars]
ansible_port=5985
ansible_connection=winrm
ansible_winrm_scheme=http
jenkins_slave_home=C:/Jenkins
```

## Example Playbook

this role don't install java package, so you need install java first.

requirements.yml
```
- name: java
  src: <repo_url>
  version: <branch_name>
  scm: git

- name: jenkins-slave
  src: <repo_url>
  version: <branch_name>
  scm: git
```

playbook.yml
```
- hosts: jenkins_slave
  vars:
    jenkins_master_url: http://192.168.56.21/jenkins
    jenkins_master_username: admin
    jenkins_master_password_or_token: 1194d76e992c37e2a546e238fb528872b0
    jenkins_slave_username: jenkins
    jenkins_slave_password: Q1w2e3r4
  roles:
    - java
    - jenkins-slave
```