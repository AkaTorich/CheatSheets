`sudo nmap -sU --open -p 161 192.168.1.101 `
cat > community << EOF  
public  
private  
manager  
EOF  
`for ip in $(sec 1 254); do echo TARGET.$ip; done > ips`
onesixtyone -c community -i ips  
#enum  
snmpwalk -c public -v1 -t 10 TARGET  
#enum windows users  
snmpwalk -c public -v1 TARGET 1.3.6.1.4.1.77.1.2.25  
#enum windows prrocesess  
snmpwalk -c public -v1 TARGET 1.3.6.1.2.1.25.4.2.1.2  
#enum open TCP ports  
snmpwalk -c public -v1 TARGET 1.3.6.1.2.1.6.13.1.3  
#enum Instaled software  
snmpwalk -c public -v1 TARGET 1.3.6.1.2.1.25.6.3.1.2  
  
#decode answer  
import binascii  
s='50 40 73 73 77 30 72 64 40 31 32 33 21 21 31 32 33 1 3 9 17 18 19 22 23 25 26 27 30 31 33 34 35 37 38 39 42 43 49 50 51 54 57 58 61 65 74 75 79 82 83 86 90 91 94 95 98 103 106 111 114 115 11 9 122 123 126 130 131 134 135'  
print(binascii.unhexlify(s.replace(' ','')))  
#decode answer 2  
echo '50 40 73 73 77 30 72 64 40 31 32 33 21 21 31 32 33 1 3 9 17 18 19 22 23 25 26 27 30 31 33 34 35 37 38 39 42 43 49 50 51 54 57 58 61 65 74 75 79 82 83 86 90 91 94 95 98 103 106 111 114 115 11 9 122 123 126 130 131 134 135' | xargs | xxd -ps -r | echo ''

### Resources 

`https://blog.cedrictemple.net/239-faire-des-requetes-snmp-en-ligne-de-commande-sous-linux/`

  

### Identification & Scans 

`nmap -vv -sV --version-intensity=5 -sU -Pn -p 161,162 --script=snmp-netstat,snmp-processes IP`

  

### Snmpwalk 

`snmpwalk -c public -v1 IP 1 > snmpwalk.txt  
```
Windows RUNNING PROCESSES   1.3.6.1.2.1.25.4.2.1.2 
Windows INSTALLED SOFTWARE  1.3.6.1.2.1.25.6.3.1.2 
Windows SYSTEM INFO     1.3.6.1.2.1.1.1 
Windows HOSTNAME        1.3.6.1.2.1.1.5 
Windows DOMAIN          1.3.6.1.4.1.77.1.4.1 
Windows UPTIME          1.3.6.1.2.1.1.3 
Windows USERS           1.3.6.1.4.1.77.1.2.25 
Windows SHARES          1.3.6.1.4.1.77.1.2.27 
Windows DISKS           1.3.6.1.2.1.25.2.3.1.3 
Windows SERVICES        1.3.6.1.4.1.77.1.2.3.1.1 
Windows LISTENING TCP PORTS 1.3.6.1.2.1.6.13.1.3.0.0.0.0 
Windows LISTENING UDP PORTS 1.3.6.1.2.1.7.5.1.2.0.0.0.0   

Linux   RUNNING PROCESSES   1.3.6.1.2.1.25.4.2.1.2 
Linux   SYSTEM INFO     1.3.6.1.2.1.1.1 
Linux   HOSTNAME        1.3.6.1.2.1.1.5 
Linux   UPTIME          1.3.6.1.2.1.1.3 
Linux   MOUNTPOINTS     1.3.6.1.2.1.25.2.3.1.3 
Linux   RUNNING SOFTWARE PATHS  1.3.6.1.2.1.25.4.2.1.4 
Linux   LISTENING UDP PORTS 1.3.6.1.2.1.7.5.1.2.0.0.0.0 
Linux   LISTENING TCP PORTS 1.3.6.1.2.1.6.13.1.3.0.0.0.0   
```
Community: 
admin 
manager 
public 
private`

### OneSixtyOne 

`# Scanning using onesixtyone (get existing communities) $ onesixtyone -c <dictCommunity.txt> -i <ip.txt>`