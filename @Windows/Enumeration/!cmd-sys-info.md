# cmd: get OS version  
ver  
  
# cmd: show devices  
sc query state=all  
  
# cmd: show processes & services  
tasklist /svc  
  
# cmd: show all processes & DLLs  
tasklist /m  
  
# cmd: remote process listing  
tasklist /S <ip> /v  
  
# cmd: force process to terminate  
taskkill /PID <pid> /F  
  
# cmd: remote system info  
systeminfo /S <ip> /U domain\user /P Pwd  
  
# cmd: query remote registry, /s=all values  
reg query \\<ip>\<RegDomain>\<Key> /v <Value>  
  
# cmd: search registry for passwords  
reg query HKLM /f password /t REG_SZ /s  
  
# cmd: list drives *must be admin  
fsutil fsinfo drives  
  
# cmd: search for all PDFs  
dir/a /s /b c:\*.pdf*  
  
# cmd: search for patches  
dir /a /b c:\windows\kb*  
  
# cmd: search files for password  
findstr /si password *.txt | *.xml | *.xls  
  
# cmd: directory listing of C:  
tree /F /A c:\ > tree.txt  
  
# cmd: save security hive to file  
reg save HKLM\Security security.hive  
  
# Current user  
echo %USERNAME%