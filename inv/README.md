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

#### Create an RDP connection with the virtual machine.Open up PowerShell and run this script.

```
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "MYdatadisk" -Confirm:$false
```

## Automation using Ansible
#### Inventory Structure 
![image](https://user-images.githubusercontent.com/41265279/42834617-ba362fac-8a14-11e8-8076-20020dacc283.png)


#### Connection oriented vars (group_vars)
![image](https://user-images.githubusercontent.com/41265279/42834751-237fbcc6-8a15-11e8-9978-90cf09f4f73a.png)

#### Ansible Command
```
ansible -m win_ping win_azure -i inv/hosts --ask-pass
```

## Troubleshooting
