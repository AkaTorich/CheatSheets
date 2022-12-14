# ipconfig: IP configuration  
ipconfig /all  
  
# ipconfig: local DNS cache  
ipconfig /displaydns  
  
# netstat: open connections  
netstat -ano  
  
# netstat: netstat loop  
netstat -anop tcp 1  
  
# netstat: listening ports  
netstat -an| findstr LISTENING  
  
# rout: routing table  
route print  
  
# arp: known MACs  
arp -a  
  
# nslookup: DNS Zone Xfer  
nslookup, set type=any, ls -d domain > results.txt, exit  
  
# nslookup: domain SRV lookup (_ldap, _kerberos, _sip)  
nslookup -type=SRV _www._tcp.url.com  
  
# tpftp: file transfer (TPFTP)  
tftp -I <ip> GET <remotefile>  
  
# netsh: saved wireless profiles  
netsh wlan show profiles  
  
# netsh: disable firewall (Old)  
netsh firewall set opmode disable  
  
# netsh: export wifi plaintext password  
netsh wlan export profiles folder=. key=clear  
  
# netsh: list interfaces IDs/MTUs  
netsh interface ip show interfaces  
  
# netsh: set DNS server  
netsh interface ip set dns local static <ip>  
  
# ip: set IP netsh interface  
ip set address local static <ip> <nmask> <gw> <ID>  
  
# Set interface to use DHCP netsh interface  
ip set address local dhcp