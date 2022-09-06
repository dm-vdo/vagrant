# vagrant

This repository contains sample Vagrantfiles for various host environments to put together a "bunsen-ready" environment.

# Instructions

For the best experience, it is best to bring the environment up serially rather than in parallel.

`vagrant up --no-parallel --provision`

The `--no-parallel` flag makes sure the VMs are initialized one at a time.

The `--provision` flag is used to ensure that Fedora 35+ hosts get the necessary packages for Bunsen provisioning installed.

# Requirements

- Each host must be able to reach its peers by name as specified in the Bunsen inventory file.

- Presently using the cloud-base Fedora images are a sufficient starting base.
  - If more customization is needed, check out the [various packer templates for Vagrant in the chef/bento project](https://github.com/chef/bento).

- Disk requirements vary based on the system role.
  - As a minimum guideline, the OS disk on all systems should be at least 40 GiB.
  - For the `FARM` systems, there should be an additional disk attached that is ~280 GiB or larger.
