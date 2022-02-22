# vagrant

This is a sample Vagrantfile to put together a "bunsen-ready" environment.

# Instructions

For the best experience, it is best to bring the environment up serially rather than in parallel.

`vagrant up --no-parallel --provision`

The `--no-parallel` flag makes sure the VMs are initialized one at a time.

The `--provision` flag is used to ensure that Fedora 35+ hosts get the necessary packages for Bunsen provisioning installed.

# Needs

- Each host needs to be able to reach each other by name as specified in the Bunsen inventory file.

- How to generate a box containing an image to use. (refer to bento project and using the `packer` utility)

- What are the storage configuration requirements to set up machines appropriately?
  - Based on experience, there needs to be a disk that is large enough to contain both /u1 and vdo_scratch.  Ideally that will be configurable down the road, but we should at least write down this piece as a consideration.

