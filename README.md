# Ansible Beginners Guide

### Get Started
1. First Create atleast 2 virtual machine (Linux Recommended) in your computer
2. Connect both virtual machine with main machine (your computer) by using SSH [Putty](https://www.putty.org/)
3. Once done, now go to following directory
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
4. Now first of all edit "hosts" file with any editor
   * Note the ip of virtual machine 2 and add it on the bottom of hosts file
   * You can direcly paste ip or you can add multiples ip address by grouping them. Example-
   
   i) Add ip address directly
   ```
    192.168.0.2
   ```
   ii) Add group of ip address 
   ```
    [any_name_you_want]
    192.168.0.2
    192.168.0.3
   ```
