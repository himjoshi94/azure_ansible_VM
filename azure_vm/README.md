Role Name
=========

This role provisions a Virtual Machine in Azure and attaches managed disk(s).

Requirements
------------

While working on this, I have discovered that lot of python modules were required. The requirements-azure.txt is needed by the Azure module

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

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
