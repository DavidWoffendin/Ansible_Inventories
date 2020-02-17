# FYP_Inventories
FYP, Configuration storage repository


ansible-playbook playbooks/jenkins-server.yml -i inventories/hosts_local

Jenkins.instance.pluginManager.plugins.each{
  plugin -> 
    println ("  - name: ${plugin.getShortName()}")
    println ("    version: '${plugin.getVersion()}'")
}