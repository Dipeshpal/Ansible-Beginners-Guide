# Ansible Beginners Guide

### Get Started
1. First Create atleast two virtual machine (Linux Recommended) in your computer
2. Connect both virtual machine with main machine (your computer) by using SSH [Putty](https://www.putty.org/)
3. Install ansble on VM 1 (Virtual Machine 1). (Installation Guide)[https://www.edureka.co/blog/install-ansible/]
  ```
    yum install ansible -y
  ```
4. Once done, now go to following directory in VM 1
```
[root@localhost ansible]# pwd
/etc/ansible
[root@localhost ansible]# tree
.
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
6. 
