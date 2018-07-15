This ansible playbook creates Virtual Machine in Azure and also attaches managed disk.

# How to run the playbook:
ansible-playbook azure_vm.yml -vvv --vault-password-file=./.pass

##### NOTE: 
A password is needed to run this playbook, please create the password as "justdoitnow" as the admin password is hashed out for security reasons.
please refrain from seeing the admin password


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
