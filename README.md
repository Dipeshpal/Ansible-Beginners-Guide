# Ansible Beginners Guide

## Get Started

### 1. Setup Virtual Machines and Establishing connections between them
1. First Create atleast two virtual machine (Linux Recommended) in your computer
2. Connect both virtual machine with main machine (your computer) by using SSH [Putty](https://www.putty.org/)
3. Install ansble on VM 1 (Virtual Machine 1). [Installation Guide](https://www.edureka.co/blog/install-ansible/)
  ```
    yum install ansible -y
  ```
4. Once done, now go to following directory in VM 1
```
[root@localhost etc]# tree ansible
ansible
|-- ansible.cfg
|-- hosts
|-- main.yml
`-- roles

```
5. Now first of all edit "hosts" file with any editor
   * Note the ip of virtual machine 2 and add it on the bottom of hosts file
   * You can direcly paste ip or you can add multiples ip address by grouping them. Example-
   
   i) Add ip address directly
   ```
    192.168.0.2
   ```
   ii) Add group of ip address (You can also create multiple groups). You can add any name you want.
   ```
    [app_group]
    192.168.0.2
    192.168.0.3
   ```
5. Now test whether connection is established or not from virtual machine 1.
  ```
    ansible app_group -m ping
  ```
    `If connection established you will get success ping`
6. NOTE: (Optional)
   ```
    If you want to create your own "hosts" file in some other directory then you need to uncomment "Inventory" in "ansible.cfg" file and add your hosts file directory.
   ```
   ```
   You can also specify your hosts file location in command instead of "ansible.cfg" file.
   Command- "ansible app_group -i /root/custom_hosts -m ping
   ```
### 2. Create Playbook
We will write ansible playbook and create ansible roles.
1. Create ansible roles with ansible-galaxy (ansible-galaxy) will automatically create whole structure for us.
We will create apache roles under default directory. Command-
  ```
  ansible-galaxy init /etc/ansible/roles/apache -offline
  ```
This will create apache roles under roles dirctory. The tree structure is-
```
[root@localhost roles]# tree apache
apache
|-- defaults
|   `-- main.yml
|-- files
|-- handlers
|   `-- main.yml
|-- meta
|   `-- main.yml
|-- README.md
|-- tasks
|   `-- main.yml
|-- templates
|-- tests
|   |-- inventory
|   `-- test.yml
`-- vars
    `-- main.yml
```
