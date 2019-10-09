# Ansible playbooks for KVM configuration, VMs creation and provision

## NOTE! In my case i used Nested Virtualization with hyper V and playbooks contain some specific configurations and lot of them run localy.

# REQUIREMENTS
- Ansible 2.8

# USAGE
- For initial host configuration and common software installation use ```kvm_initial``` plybook
```
ansible-playbook -i hosts kvm_initial.yaml
```

- For VM`s deploy and provisionig use ```init.yaml```
```
ansible-playbook -i hosts kvm_init.yaml
```





