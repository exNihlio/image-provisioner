# image-provisioner

A simple Ansible playbook to quickly provision VMs in a KVM/QEMU environment.

## Assumptions

You have Ansible installed on your KVM host

## Usage

1. Create a `cloud-init` `user-data` and `meta-data` file. Read about `cloud-init` [here](https://cloudinit.readthedocs.io/en/latest/)

2. Create the following directories or change them in the playbook to suit your environment.
- `/data/vm_storage/cloud-init`
- `/data/vm_storage/cloud-init/isos`
- `/data/vm_storage/images/base`

At a minimum you should have storage for your cloud images, a directory for your `cloud-init` files and a directory
for your installed VMs.

3. Download a qcow2 cloud image for the operating system of your choice.

4. Move the cloud image to `/data/vm_storage/images/base`

5. Change the `base_disk` disk variable to match the image you downloaded.

6. Ensure the `disk_path` variable matches the directory for your installed VMs.

7. Run the playbook as follows:
`ansible-playbook image_provisioner.yml --extra-vars="host_name=HOSTNAME full_host_name=FQDN memory=MEMORY vcpus=VCPUS network=NETWORK disk_size=DISK_SIZE"`

8. If everything works, this will rysnc and resize the disk image, mount your cloud-init data, install it with `virt-install` and delete the old cloud-init data. 
