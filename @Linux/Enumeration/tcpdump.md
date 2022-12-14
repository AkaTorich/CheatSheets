# tcpdump: show all traffic verbose  
tcpdump -vv  
  
# tcpdump: show only icmp protocol  
tcmpdump -p icmp  
  
# tcpdump: get current interfaces  
ip -o l show | awk -F': ' '{print $2}'  
  
# tcpdump: show current traffic on interface  
tcpdump -i interfaceName  
  
# tcpdump: filter traffic  
tcpdump -i interfaceName host ipAddress  
  
# tcpdump: filter traffic, by source/destination IP address, -n no hostname resolve  
tcpdump -i interfaceName -n src ipAddress  
tcpdump -i interfaceName dst ipAddress  
  
# tcpdump: filter traffic, by network  
tcpdump net 1.2.3.4/24  
  
# tcpdump: filter by port  
tcpdump port 443  
tcpdump src port 80  
  
# tcpdump: filter by protocol  
tcpdump icmp  
  
# tcpdump: filter by packet size (greater/less)  
tcpdump greater 128  
  
# tcpdump: write to file  
tcpdump -w fileName  
  
# tcpdump: isolate SYN flags (more: tcp-rst, tcp-urg, tcp-ack, tcp-fin)  
tcpdump 'tcp[tcpflags] == tcp-syn'  
  
  
# tcpdump: show connections to a specific ip  
tcpdump -i interfaceName -tttt dst ipAddress and not net 192.168.1.0/24  
  
# tcpdump: capturing traffice on port 22-23  
tcpdump -nvvX -s0 -i interfaceName tcp portrange 22-23  
  
# tcpdump: capture traffic to specific IP exluding specific subnet  
tcpdump -I interfaceName -tttt dst ipAddress and not net 1.1.1.0/24  
  
# tcpdump: capturing traffic B/W local-192.1  
tcpdump net 192.1.1  
  
# tcpdump: capturing traffic for <seconds>  
dumpcap -I interfaceName -a duration:<sec> -w file fileName.pcap  
  
# tcpdump: replay packets (FUZZ or DOS)  
tcpreplay --topspeed --loop=0 --intf=interfaceName <.pcap_file_to_replay> -- mbps=10|100|1000