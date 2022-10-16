```bash
# wfuzz: -c = color, -z = paylaod, --hc = hide response with code XXX  
wfuzz -c -z file,/path/to/file.txt --hc 404 http://ipAddress/FUZZ  
```
  
```bash
# wufzz: -hs = hide regex switch, -d = POST, FUZZ means insert payload here  
wfuzz -c -z file,/root/Documents/MrRobot/fsoc.dic --hs Invalid -d "param1=FUZZ&param2=someValue" http://ipAddress/wp-login.php  
```  

```bash
wfuzz -c -z file,/usr/share/SecLists/Discovery/Web-Content/raft-large-directories.txt --hc 404 "http://shoppy.htb/FUZZ/"
```
