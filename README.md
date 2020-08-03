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
jenkins_master_password: admin

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

`jenkins_master_username` is the login username of your jenkins site.

`jenkins_master_password` is the login password of your jenkins site.

`jenkins_slave_username` is the jenkins slave account username on jenkins slave machine.

`jenkins_slave_password` is the jenkins slave account password on jenkins slave machine.

`jenkins_slave_node_name` is the node name of this jenkins slave. Default is the hostname defined in inventory file.

`jenkins_slave_java_opts` is the java options when run jenkins slave service.

`jenkins_slave_home` in linux server default is `/opt/jenkins`, in windows server default is `C:/Jenkins`.

## Dependencies

None.

## Example Playbook

requirements.yml
```
- name: jenkins-slave
  src: <repo_url>
  version: <branch_name>
  scm: git
```

playbook.yml
```
- hosts: servers
  roles:
    - jenkins-slave
```