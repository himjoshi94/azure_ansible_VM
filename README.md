This ansible playbook creates Virtual Machine in Azure and also attaches managed disk.

# How to run the playbook:
ansible-playbook azure_vm.yml -vvv --vault-password-file=./.pass

As part of the assignment I was told to create 100G disk, but with the trial account there was a limitation of creating more disk spaces.

##### Output
![screenshot 6](https://user-images.githubusercontent.com/41265279/42764530-7a4fb4e4-8933-11e8-98d1-a5162e482437.png)


##### NOTE: 
A password is needed to run this playbook, please contact the owner of this playbook to execute as the password is hashed out.


## Directory Structure:
```
|-- azure_vm
|   |-- defaults
|   |   `-- main.yml
|   |-- files
|   |   `-- requirements-azure.txt
|   |-- handlers
|   |   `-- main.yml
|   |-- meta
|   |   `-- main.yml
|   |-- README.md
|   |-- tasks
|   |   |-- dependencies.yml
|   |   |-- drive_sql.yml
|   |   |-- drive_webapp.yml
|   |   |-- launch_vm.yml
|   |   |-- main.yml
|   |   |-- network.yml
|   |   `-- subnet.yml
|   |-- templates
|   |-- tests
|   |   |-- inventory
|   |   `-- test.yml
|   `-- vars
|       `-- main.yml
|-- azure_vm.yml
`-- README.md
```

## TAGS
 - dependencies
 - network
 - volume_webapp
 _ volume_sql
 - complete

dependencies - installs only dependencies
network - create a virtual network driver, subnet and security group
volume_* - creates and attaches respective disk drives.
complete - used to run the complete functionality of the playbook

##### Example for tags
ansible-playbook azure_vm.yml -vvv --vault-password-file=./.pass  --tags "network"
