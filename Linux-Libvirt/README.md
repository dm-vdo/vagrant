# Linux Libvirt Vagrantfile

This file has been used on up to date releases of Fedora.

# Package Requirements

The following packages should be installed via the Fedora repositories:

* ansible
* libvirt
* libvirt-devel
* rsync
* vagrant
* virt-mananger

The following packages will likely get pulled in automatically and should be removed before proceeding:

* rubygem-fog-core
* vagrant-libvirt

# Vagrant Plugins

The following vagrant plugins should be installed before trying to start the virtual machines in the Bunsen environment:

* vagrant-hostmanager
* vagrant-libvirt

# sudoers

It is required that the user who is launching the virtual machines has full sudoers privileges.  If the user does not have a NOPASSWD: spec in their sudoers, they will be prompted periodically during the launch phase of the VMs because of the various updates to /etc/hosts.

# Known Issues

* Running Vagrant-Libvirt on RHEL, or any of its derivatives, has been known to run into problems.  It is likely easier to utilize a Virtualbox-based vagrant environment for this reason.

