##### Searching for Configuration Files
Recursively search for files in the current directory with
“pass” in the name, or ending in “.config”:
`> dir /s *pass* == *.config`
Recursively search for files in the current directory that
contain the word “password” and also end in either .xml, .ini,
or .txt:
`> findstr /si password *.xml *.ini *.txt`
#Find all passwords in all files
`> findstr /spin "password" "."`

##### print all files in c:\ to file  
`dir /b /a /s c:\ > cdirs.txt`
  
#finding all passwords like grep  
type cdirs.txt | findstr /i passwd  
  
#show network shares  
net use  
  
#extensions files extensions   
install backup .bak .cmd .vbs .cnf .conf .config   
.ini .xml .txt .gpg .pgp .pi2 .der .csr .cer id_rsa id_dsa  
.ovpn vnc ftp ssh vpn git .kdbx .db  
  
#file interesting files  
unattend.xml  
Unattended.xml  
sysprep.inf  
sysprep.xml  
VARIABLES.DAT  
setupinfo  
setupinfo.bak  
web.config  
SiteList.xml  
.aws\\credentials  
.azure\accessTokens.json  
.azure\azureProfile.json  
gcloud\credentials.db  
gcloud\legacy_credentials  
gcloud\access_tokens.db