# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

CONFIG = YAML.load(File.read('config.yml'))
DEFAULT_IMAGE = 'centos/7'

Vagrant.configure("2") do |config|
  CONFIG['groups'].each do |group_name, group_hash|
    group_hash["vms"].each do |vm|
      config.vm.define vm["name"] do |subconfig|
        subconfig.vm.box = DEFAULT_IMAGE || vm["image"]
        subconfig.vm.hostname = vm["name"]
        vm["ports"].each do |port|
          subconfig.vm.network :forwarded_port, guest: port["guest"], host: port["host"]
        end
        subconfig.vm.provider :virtualbox do |v|
          v.name = "ansible-local-#{group_name}-#{vm["name"]}"
          v.linked_clone = true
          v.cpus = vm['cpus'] || 1
          v.memory = vm['memory'] || 1024

          v.customize [
            'modifyvm',
            :id,
            '--groups',
            "/Ansible/Local/#{group_name}"
          ]
        end

        if Vagrant.has_plugin?('vagrant-vbguest')
          subconfig.vbguest.auto_update = false
        end
      end
    end
  end
end
