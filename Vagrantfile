# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true

  config.vm.define "infra" do |infra|
    infra.vm.provision :hosts, :sync_hosts => true
    infra.vm.box = "fedora-34-x86_64"
    infra.vm.provider :libvirt do |libvirt|
      libvirt.memory = 2048

      (1..2).each do |o|
        libvirt.storage :file, :size => '40G', :type => 'raw'
      end
    end
  end
  config.vm.define "resource" do |resource|
    resource.vm.box = "fedora-34-x86_64"
    resource.vm.provider :libvirt do |libvirt|
      libvirt.memory = 2048

      (1..2).each do |o|
        libvirt.storage :file, :size => '40G', :type => 'raw'
      end
    end
  end
  (1..1).each do |prov|
    config.vm.define "farm-#{prov}" do |farm|
      farm.vm.box = "fedora-34-x86_64"
      farm.vm.provider :libvirt do |libvirt|
        libvirt.memory = 2048

        (1..2).each do |o|
          libvirt.storage :file, :size => '280G', :type => 'raw'
        end
      end
    end
  end
end
