# ansible-ec2-nginx


Simple Ansible task, description:
```
Prerequisites

    4 linux machines (VMs, instances in Digital Ocean, GCP, AWS EC2, dosen't matter);
    Python installed (2.7 or 3.5+);
    established password-less connection from one machine (controller) to others;

ps: one of machine (controller) can be a Windows 10 machine with WSL/WSL2
Task

    Create a inventory file with four groups, each provisioning VM should be in separate group and group named iaas what should include childrens from two first groups;
    Create reusable roles for that:

    creating a empty file /etc/iaac with rigths 0500, this role should be idempodent
    define content of /etc/issue as variable

    Create playbook for:

    invoke the role for /etc/iaac for hosts group iaas
    invoke the role for defining variable for all hosts
    print in registered variables
    printing hostnames together with registered variables will be a plus.

    Create a repo in your GitHub account and commit code above

Optional:

    use ansible_user and ansible_password for ssh connection and store passwords for each VM in encrypred way (add vault password to README.md in this case)
```

Requirements
------------

The below requirements are needed on the host that executes this module.

- ansible 2.9.12
- python >= 2.6

## Run playbook


```bash
export ANSIBLE_HOST_KEY_CHECKING=False
```

Simple run playbook:

```bash
ansible-playbook   -u ubuntu -i inventory  --private-key=../your-own-key-file  playbook.yml
ansible-playbook -i inventory playbook.yml --extra-vars "ansible_user=ubuntu ansible_password=..."
```

## Get 

Enter 