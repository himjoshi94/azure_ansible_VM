## Requirements
### Server Side
- python2-winrm
### Client Side
- enabling winrm
- changing the winrm config

__Please run the below command from cmd.exe as administrator__
```
 winrm set winrm/config/service/auth @{Basic="true"}
 winrm set winrm/config/service @{AllowUnencrypted="true"
```

## On typing the below command 
__winrm get winrm/config__ the output has to show as below
```
   Service : Basic - true
   Service : AllowUnencrypted="true"
```

## Powershell commands
#### Intializing volumes and creation of disk letters
#### Creating disk
```
$diskConfig = New-AzureRmDiskConfig -Location southeastasia -CreateOption Empty -DiskSizeGB 20
$dataDisk = New-AzureRmDisk -ResourceGroupName himanshu_RG -DiskName MYdatadisk -Disk $diskConfig
```

#### Calling VM
```
$vm = Get-AzureRmVM -ResourceGroupName himanshu_RG -Name hj
```

#### Attaching the disk to VM 
``` 
$vm = Add-AzureRmVMDataDisk -VM $vm -Name MYdatadisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

#### Updating
```
Update-AzureRmVM -ResourceGroupName himanshu_RG -VM $vm 
```
![image](https://user-images.githubusercontent.com/41265279/42839554-b95ed112-8a21-11e8-8e71-7939d6749c69.png)

#### Create an RDP connection with the virtual machine.Open up PowerShell and run this script.

```
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "MYdatadisk" -Confirm:$false
```

#### Output

![image](https://user-images.githubusercontent.com/41265279/42839309-fc516b20-8a20-11e8-8338-090fe13a9ba9.png)

## Automation using Ansible
#### Inventory Structure 
![image](https://user-images.githubusercontent.com/41265279/42834617-ba362fac-8a14-11e8-8076-20020dacc283.png)


#### Connection oriented vars (group_vars)
![image](https://user-images.githubusercontent.com/41265279/42834751-237fbcc6-8a15-11e8-9978-90cf09f4f73a.png)

#### Testing Ansible connection with Windows
```
ansible -m win_ping win_azure -i inv/hosts --ask-pass
```

#### Executing the win_* modules 
```
ansible-playbook -i inv/hosts ansible_powershell.yml --ask-pass
```
or

```
ansible-playbook -i inv/hosts ansible_powershell.yml -k
```

#### win_shell play
![image](https://user-images.githubusercontent.com/41265279/42839227-ac87efc4-8a20-11e8-80f8-3291100f2014.png)




