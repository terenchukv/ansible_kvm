# Ansible playbooks for KVM configuration, VMs creation and provision

## NOTE! In my case i used Nested Virtualization with hyper V and playbooks contain some specific configurations and lot of them run localy.

# REQUIREMENTS
- Ansible 2.8

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





