# Ansible playbooks for KVM configuration, VMs creation and provision

## NOTE! In my case i used Nested Virtualization with hyper V and playbooks contain some specific configurations and lot of them run localy.

# REQUIREMENTS
- Ansible 2.8

# Usage
- Use ```initial.yaml``` playbook for KVM host provision. Can run localy or from remote host.
- ```vm_create.yaml``` - create new VM. Playbook run bash script with cloud-init configuration. Check [vm_conf.j2](./templates/vm_conf.j2)
### NOTE! put your public key to vm_conf.j2 in cloud-init ```ssh_authorized_keys``` block.
- ```vm_provision.yaml``` - install Wordpress in installed VMs.

# My case usge:

- Create VM in hyperV --> Enable nested virtualization for this VM --> Proxy configure --> Install Ansible 2.8
- Run ```initial.yaml``` for install KVM and common software:
```
ansible-playbook initial.yaml --connection=local
```

After that you get installed KVM and Nginx on your host

- Generate ssh key and put in [vm_conf.j2](./templates/vm_conf.j2) (cloud-init ```ssh_authorized_keys``` block)

- VM Create:
```
ansible-playbook vm_create.yaml --connection=local
```

Script will ask you IP address for your VM. 
KVM IP range for VMs: from 192.168.122.2 to 192.168.122.254

### NOTE! Your VMS will be named by IP

- Install Wordpress in your VM:
```
ansible-playbook -i '<your_vm_ip>,' vm_provision.yaml
```

- In same way create and provision second VM

- In host were installed KVM and Nginx create configuration for Nginx Load Balancer: 
```
upstream loadbalance {
    ip_hash;
    server <first_vm_ip>:8000;
    server <second_vm_ip>:8000;
}

server {
    location / {
        proxy_pass http://loadbalance;
    }
}
```





