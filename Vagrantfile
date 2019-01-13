# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

configk8s = YAML.load_file('config.yaml')
$private_nic_type = configk8s.fetch('net').fetch('private_nic_type')
$box_name = configk8s.fetch('box-name') # "williamyeh/ubuntu-trusty64-docker"

Vagrant.configure(2) do |config|
    config.vm.define "master" do |master|
        m = configk8s.fetch('master')
        master.vm.box = $box_name
        master.vm.guest = :ubuntu
        master.vm.network configk8s.fetch('net').fetch('network_type'), ip: m.fetch('base-address'), nic_type: $private_nic_type    
        master.vm.provider :virtualbox do |v|
            v.cpus = m.fetch('cpus')
            v.memory = m.fetch('memory')
            v.name = "master"
        end
    end
end
