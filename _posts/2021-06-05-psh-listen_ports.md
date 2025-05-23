---
title: "powershell - show listen ports of processes"
category: powershell
author: Oliver Gaida
version: 2
---

# powershell - show listen ports of processes

```powershell
Get-NetTCPConnection -State Listen | Select-Object -Property *, `
	@{'Name' = 'ProcessName';'Expression'={(Get-Process -Id $_.OwningProcess).Name}} `
	| select ProcessName,LocalAddress,LocalPort
```

Output:

```
ProcessName              LocalAddress  LocalPort
-----------              ------------  ---------
services                 ::                49755
jhi_service              ::1               49673
spoolsv                  ::                49672
svchost                  ::                49668
svchost                  ::                49667
svchost                  ::                49666
wininit                  ::                49665
lsass                    ::                49664
System                   ::                47001
telegraf                 ::                 9273
svchost                  ::                 7680
Veeam.EndPoint.Service   ::                 6183
System                   ::                 5986
System                   ::                 5357
svchost                  ::                 3389
System                   ::                  445
System                   ::                  443
svchost                  ::                  135
services                 0.0.0.0           49755
spoolsv                  0.0.0.0           49672
svchost                  0.0.0.0           49668
svchost                  0.0.0.0           49667
svchost                  0.0.0.0           49666
wininit                  0.0.0.0           49665
lsass                    0.0.0.0           49664
AppleMobileDeviceService 127.0.0.1         27015
Veeam.EndPoint.Service   0.0.0.0            9395
Veeam.EndPoint.Service   0.0.0.0            6184
Veeam.EndPoint.Service   0.0.0.0            6183
mDNSResponder            127.0.0.1          5354
svchost                  0.0.0.0            5040
svchost                  0.0.0.0            3389
System                   192.168.56.1        139
System                   192.168.2.106       139
svchost                  0.0.0.0             135
```

Explaination:

- `Get-NetTCPConnection -State Listen` gets the listen processes without processnames
- `@{'Name' = 'ProcessName';'Expression'={(Get-Process -Id $_.OwningProcess).Name}}` adds an output attribute with the name `ProcessName` with the value of the inner Command `(Get-Process -Id $_.OwningProcess).Name`, which is the desired processname.
- `$_` is the current object-instance of the tcp-connection 


# special command to list uniq services with count which connect to a remote port 1433

```powershell
Get-NetTCPConnection | where-object { $_.RemotePort -eq '1433' } `
	| Select-Object -Property *, `
	@{'Name' = 'ProcessName';'Expression'={(Get-Process -Id $_.OwningProcess).Name}} `
	| select ProcessName, RemoteAddress `
	| Group-Object -property ProcessName, RemoteAddress -NoElement `
	| Select-Object -Property Count, Name `
	| sort-object -property Count
```