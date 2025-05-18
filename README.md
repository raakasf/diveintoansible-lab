# Dive Into Ansible Course Lab

* [Udemy](https://www.udemy.com/course/diveintoansible/?referralCode=28BBB7A1DCCD01BBA51F)

```bash
docker compose up
```

## Lecture 9

Ansible configuration are chosen in this order, starting with the highest priority

```bash
ANSIBLE_CONFIG=~/example.cfg
/home/ansible/testdir/ansible.cfg
/home/ansible/ansible.cfg
/etc/ansible/ansible.cfg
```

## Lecture 10

```bash
ANSIBLE_HOST_KEY_CHECKING=False ansible all -m ping
# or add in ansible.cfg
host_key_checking = False
ansible centos -m ping
ansible ubuntu -m ping
ansible '*' -m ping
ansible all -m ping -o
ansible centos --list-hosts
# Using regex ~
ansible ~.*3 --list-hosts
# To change user, add to hosts file
ansible_user=root
ansible all -m command -a 'id' -o
# In hosts file, add
ansible_become=true ansible_become_pass=password
# This is the same as the one above
ansible all -a 'id' -o
# We can specify post in hosts file as
ansible_port=2222
# or
cento1:2222
# We can specify a control host too
[control]
ubuntu-c ansible_connection=local

# We can use [2:3] format to specify hosts
[centos]
centos1 ansible_user=root ansible_port=2222
centos[2:3] ansible_user=root
[ubuntu]
ubuntu[1:3] ansible_become=true ansible_become_pass=password

# We can use this to extract common vars
[centos:vars]

#Using this we can define children
[linux:children]
centos
ubuntu

# We can define vars for all like this but host specific vars take precedence
[all:vars]
ansible_port=1234
# We can also do 
[linux:vars]
ansible_port=1234

ansible linux -m ping -e 'ansible_port=22' -o
```
