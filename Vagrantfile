# -*- mode: ruby -*-
# vi: set ft=ruby :

# Using vagrant-hostmanager allows for all of the configured VMs to be
# reachable by name both inside the virtual environment as well as from the
# hypervisor.  There is no DNS or other complicated machinery required to
# enable this functionality; it modifies /etc/hosts on all the configured
# machines based on the 'manage_guest' and 'manage_host' parameters.
#
# vagrant-hostmanager: https://github.com/devopsgroup-io/vagrant-hostmanager
unless Vagrant.has_plugin?("vagrant-hostmanager")
  raise "vagrant-hostmanager is not installed, please install it by running `vagrant plugin install vagrant-hostmanager`"
end

# This is a script to be used on Fedora 35 and newer installations where
# SELinux is enabled (at least to start) and requires the python bindings.
#
# If these packages are not installed, ansible will throw an error "Aborting,
# target uses selinux but python bindings (libselinux-python) aren't
# installed!"
$policycorescript = <<-SCRIPT
source /etc/os-release
if [ "${ID}" = "fedora" ] && [ "${VERSION_ID}" -ge 35 ]; then
  echo "Detected F35+, installing python selinux bindings needed by Ansible"
  sudo dnf install -y python3-policycoreutils python3-libselinux
fi
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.hostmanager.enabled = true
  config.hostmanager.manage_guest = true
  config.hostmanager.manage_host = true
  config.hostmanager.include_offline = true

  config.vm.define "infra" do |infra|
    infra.vm.hostname = "ossbunsen-infra"
    infra.vm.box = "fedora-35-x86_64"
    infra.vm.provider :libvirt do |libvirt|
      libvirt.memory = 2048
    end
  end
  config.vm.define "resource" do |resource|
    resource.vm.hostname = "ossbunsen-resource"
    resource.vm.box = "fedora-35-x86_64"
    resource.vm.provider :libvirt do |libvirt|
      libvirt.memory = 2048
    end
  end
  (1..2).each do |prov|
    config.vm.define "farm-#{prov}" do |farm|
      farm.vm.hostname = "ossbunsen-farm-#{prov}"
      farm.vm.box = "fedora-35-x86_64"
      farm.vm.provider :libvirt do |libvirt|
        libvirt.memory = 2048
        libvirt.storage :file, :size => '280G', :type => 'raw'
      end
    end
  end
  config.vm.provision "shell", inline: $policycorescript
end
