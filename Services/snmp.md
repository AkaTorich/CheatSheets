sudo nmap -sU --open -p 161 TARGETORRANGE -oG opn-snmp.txt  
cat > community << EOF  
public  
private  
manager  
EOF  
for ip in $(sec 1 254); do echo TARGET.$ip; done > ips  
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