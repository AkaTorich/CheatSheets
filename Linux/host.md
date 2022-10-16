#for search for IP  
host DOMAIN  
#for search for emails  
host -t mx DOMAIN  
#for search for text  
host -t txt DOMAIN  
#for search for subdomains  
host -t a DOMAIN  
#for search for dns  
host -t ns DOMAIN  
#DNS zone transfer  
host -l DOMAIN ns1.DOMAIN  
#enumerate domains from ips  
for ip in $(cat list.txt); do host $ip.DOMAIN; done  
#reverse lookup  
for ip in $(seq 1 256); do host IP.$ip; done | grep -v "not found"