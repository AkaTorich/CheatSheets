# target description  
# DNAT - Destination Network Address Translation (Destinationadress and -ports)  
# SNAT - Source Network Address Translation (Sourceaddress and -ports)  
# MASQUERADE - Route between networks  
# DROP - drop packets  
# Reject - drop packets with icmp respsonse (INPUT OUTPUT FORWARD)  
  
# iptables: debugging  
watch iptables -t nat -L -v -n  
  
# iptables: traffic redirection  
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.1.1.1:80  
  
# iptables: traffic redirection with local source  
iptables -t nat -A OUTPUT -p tcp -m owner --gid-owner burp -j DNAT --to 127.0.0.1:8080  
  
# iptables: remove rules  
iptables -t nat -L --line-numbers