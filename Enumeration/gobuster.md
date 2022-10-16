    ищет папки на сайте по словарю  
gobuster dir -u https://10.10.10.7/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 50 -k  
#########################################################################  
  
  
переберем директории. Для этого используем быстрый gobuster. В параметрах укаываем, что мы хотим сканировать дирректории (dir),   
указываем сайт (-u), список слов(-w), расширения, которые нас интересуют (-x), количество потоков (-t).  
  
gobuster dir -t 128 -u blunder.htb -w /usr/share/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt -x php,html,txt  
  
  
sudo gobuster dir -u http://10.10.10.206/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 10 -k  
  
gobuster dir -u http://10.10.10.43 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -x php -o scans/gobuster-http-root-medium -t 20  
^Directory bruteforcer  
  
#subdomain bruteforce  
gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://shoppy.htb