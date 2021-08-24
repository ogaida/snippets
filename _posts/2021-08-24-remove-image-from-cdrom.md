---
title:  "Entfernen CDROMs aus allen VMS"
categories:
  - powercli
  - powershell
author: Oliver Gaida
version: 1
---

```powershell
  $vcenter = "my.vcenter.local"
$credFile = ".${vcenter}.cred"

# siehe https://www.vgemba.net/vmware/powershell/Saving-PowerCLI-Credentials/
if (!(Test-Path $credFile -PathType leaf)){
  $credential = Get-Credential
  $credential | Export-Clixml -Path $credFile
}else{
  $credential = Import-Clixml -Path $credFile
}

$out=(Connect-VIServer -Server $vcenter -Protocol https -force -Credential $credential)

foreach ($vm in get-vm){
  Get-CDDrive -vm $vm |Where-Object {$_.IsoPath -or $_.HostDevice -or $_.RemoteDevice } |Set-CDDrive -NoMedia -Confirm:$false
}
```
