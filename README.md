# FYP_Inventories
FYP, Configuration storage repository


ansible-playbook playbooks/jenkins-server.yml -i inventories/hosts_local

Jenkins.instance.pluginManager.plugins.each{
  plugin -> 
    println ("  - name: ${plugin.getShortName()}")
    println ("    version: '${plugin.getVersion()}'")
}


# Ansible Site (Local)
This Repository defines the service configuration for a local instance of Jenkins.

## Requirements

- `ansible` (2.5.x+)

## Roles needed from bitbucket

- name: 'fyp-jenkins'
  src: ''
  version: '1.0.0'
  scm: git

- name: 'fyp-configuration'
  src: ''
  version: '1.0.0'
  scm: git

## Usage

A linux machine with access to the required server will be needed to run this ansible.

### For Deployment to local machine

* A vagrant private key is used for authentication rather then a username and password

* Ensure the inventories/assured/host_local file points to the correct location for the vagrant machines private key

* Uncomment the Jenkins user in inventories/assured/group_vars/jenkins_server/vars.yml so that ansible generates the first user.

#### Deploy Full Jenkins instance and configure
Running this playbook will build jenkins from scratch, install/update plugins and then configure and deploy jobs
```
ansible-playbook playbooks/jenkins-server.yml -i inventories/hosts_local --ask-vault-pass
```