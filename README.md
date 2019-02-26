# Ansible Beginners Guide

## In this project we will setup virtual machine (Server and Client), Create Ansible roles, write ansible playbook and deploy it on client machine.

[Read more about ansible](https://docs.ansible.com/)

## Getting Started-

### 1. Setup Virtual Machines (Server and Client) and Establishing connections-
1. First Create atleast two virtual machine (Linux Recommended) in your computer
2. Connect both virtual machine with main machine (your computer) by using SSH [Putty](https://www.putty.org/)
  
     <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/1.PNG" align="center" height="408" width="608" ></a>
  
      You can directly use VM1 as server to control client (VM2) or You can establish connection with your VMs to your main machine by using putty.
  
3. Install ansible on VM 1 (Virtual Machine 1). [Installation Guide](https://www.edureka.co/blog/install-ansible/)
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
     <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/2.PNG" align="center"></a>

5. Now first of all edit "hosts" file with any editor
   * Note the ip of virtual machine 2 and add it on the bottom of hosts file
   * You can direcly paste ip or you can add multiples ip address by grouping them. Example-
   
   i) Add ip address directly
   ```
    192.168.248.129
   ```
   ii) Add group of ip address (You can also create multiple groups). You can add any name you want.
   ```
    [app_group]
    192.168.248.129
    192.168.248.130
    192.168.248.131
   ```
    <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/3.PNG" align="center"></a>

5. Now test whether connection is established or not from virtual machine 1.
    ```
      ansible app_group -m ping
    ```
    If connection established you will get success ping
    
7. NOTE: (Optional)

   'If you want to create your own "hosts" file in some other directory then you need to uncomment "Inventory" in "ansible.cfg" file and add your hosts file directory.'
   
   `ansible.cfg-`
   
    <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/4.PNG" align="center"></a>

   ```
   You can also specify your hosts file location in command instead of "ansible.cfg" file.
   Command- "ansible app_group -i /root/custom_hosts -m ping
   ```
### 2. Create Ansible Roles-
       We create ansible roles.
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
### 3. Create Playbook-
2. Now create following files under tasks, files, handlers and meta directory. These files can be found in above project. You need to edit and create only fillowing files-
     You can clone this project and use these files or codes-
   * Create main.yml, configure.yml, install.yml, service.yml in "tasks" directory
   * create main.yml in "handler" directory
   * Create httpd.original, index.html in files directory
   * Create main.yml in "meta" directory
   `Once you create all these files, your project should look like these.
    ```
    [root@localhost roles]# tree apache
    apache
    |-- defaults
    |   `-- main.yml
    |-- files
    |   |-- httpd.original
    |   `-- index.html
    |-- handlers
    |   `-- main.yml
    |-- meta
    |   `-- main.yml
    |-- README.md
    |-- tasks
    |   |-- configure.yml
    |   |-- install.yml
    |   |-- main.yml
    |   `-- service.yml
    |-- templates
    |-- tests
    |   |-- inventory
    |   `-- test.yml
    `-- vars
        `-- main.yml

    ```
3. Now use this playbook (created in step 2) by creating "runsetup.yml" in ansible dirctory
   ```
   ---
    - hosts: app_group
      roles:
      - apache
   ```
   And your ansible directrory should look like this-
   ```
      ansible
      |-- ansible.cfg
      |-- hosts
      |-- main.yml
      |-- roles
      |   `-- apache
      |       |-- defaults
      |       |   `-- main.yml
      |       |-- files
      |       |   |-- httpd.original
      |       |   `-- index.html
      |       |-- handlers
      |       |   `-- main.yml
      |       |-- meta
      |       |   `-- main.yml
      |       |-- README.md
      |       |-- tasks
      |       |   |-- configure.yml
      |       |   |-- install.yml
      |       |   |-- main.yml
      |       |   `-- service.yml
      |       |-- templates
      |       |-- tests
      |       |   |-- inventory
      |       |   `-- test.yml
      |       `-- vars
      |           `-- main.yml
      `-- runsetup.yml

      10 directories, 17 files
   ```
   
### 4. Deploy on Client Machine-

1. Now deploy runsetup, run following command-
   ```
   ansible-playbook runsetup.yml
   ```
   <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/5.PNG" align="center"></a>

2. Done, now you can check whether everything is working or not?
   * Go to VM 2 (Suppose ip of VM 2 is 192.168.0.3)
   * Open terminal and run following commands.
   
   Check httpd installed or not
   ```
   rpmquery httpd
   ```
   verify service is started or not?
   ```
   systemctl status httpd
   ```
   <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/6.PNG" align="center"></a>

   Access index.html (Webpage)
   ```
   elinks http://192.168.0.3
   ```
   <a href="url"><img src="https://github.com/Dipeshpal/Ansible-Beginners-Guide/blob/master/Raw%20Images/7.PNG" align="center"></a>


3. That's it for Ansible Getting Started
