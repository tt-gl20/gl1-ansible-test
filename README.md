# ansible-create-file-simple-task


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
- 4 VirtualBox vm-s (IP: 192.168.1.35-38)

## Run playbook


```bash
export ANSIBLE_HOST_KEY_CHECKING=False
```

Simple run playbook:

```bash
ansible-playbook   -u ubuntu -i inventory  --private-key=../your-own-key-file  playbook.yml
```
or (for user/password):
```
ansible-playbook -i inventory playbook.yml --extra-vars "ansible_user=ubuntu ansible_password=..."
```

## Output 


```
PLAY [invoke the role for /etc/iaac for hosts group iaas] **************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************
ok: [192.168.1.36]
ok: [192.168.1.35]
ok: [192.168.1.37]
ok: [192.168.1.38]

TASK [create-iaac-file : creating a empty file /etc/iaac with rigths 0500] *********************************************************************************************************************
changed: [192.168.1.36]
changed: [192.168.1.35]
changed: [192.168.1.37]
changed: [192.168.1.38]

PLAY [invoke the role for /etc/iaac for hosts group iaas] **************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************
ok: [192.168.1.36]
ok: [192.168.1.35]
ok: [192.168.1.37]
ok: [192.168.1.38]

TASK [read-issue-content : define content of /etc/issue as variable] ***************************************************************************************************************************
changed: [192.168.1.36]
changed: [192.168.1.35]
changed: [192.168.1.37]
changed: [192.168.1.38]


TASK [read-issue-content : printing hostnames together with registered variables] **************************************************************************************************************
ok: [192.168.1.35] => {
    "msg": "Printing hostname: node1 192.168.1.35 together with registered variable Ubuntu 18.04.2 LTS \\n \\l"
}
ok: [192.168.1.36] => {
    "msg": "Printing hostname: node2 192.168.1.36 together with registered variable Ubuntu 18.04.2 LTS \\n \\l"
}
ok: [192.168.1.37] => {
    "msg": "Printing hostname: node3 192.168.1.37 together with registered variable Ubuntu 18.04.2 LTS \\n \\l"
}
ok: [192.168.1.38] => {
    "msg": "Printing hostname: node4 192.168.1.38 together with registered variable Ubuntu 18.04.2 LTS \\n \\l"
}

PLAY RECAP *************************************************************************************************************************************************************************************
192.168.1.35               : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.1.36               : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.1.37               : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
192.168.1.38               : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```