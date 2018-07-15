Role Name
=========

This role provisions a Virtual Machine in Azure and attaches managed disk(s).

Requirements
------------

While working on this, I have discovered that lot of python modules were required. The requirements-azure.txt is needed by the Azure module

Role Variables
--------------

All the cloud, instance and network level variables are added in defaults/main.yml. The credentials are stored in vars/main.yml. This playbook is compatible when the variables are passed in command line with extra vars

Dependencies
------------
```
|   `-- vars
|       `-- main.yml
```

The above main.yml has been made as a cipher using ansible-vault encrypt as it contains the password for the Azure account

Playbook
----------------
The playbook just calls the role and also we can use delegate_to to target the play to run in the localhost
    - hosts: localhost
      roles:
         - { role: 'azure_vm'}

License
-------
BSD

Reference
-------
The below playbook was used and this installs all the azure cli modules that were required
https://galaxy.ansible.com/azure/azure_modules


Author Information
------------------
Himanshu Joshi
himanshjoshi2@gmail.com
