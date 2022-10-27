ldapsearch -h TARGETIP  
  
ldapsearch -h TARGETIP -x -s base namingcontexts #server info  
  
ldapsearch -h TARGETIP -x -b "DC=NAMINGTARGET,DC=TARGET" '(objectClass=Person)' #accounts info  
  
ldapsearch -h TARGETIP -x -b "DC=NAMINGTARGET,DC=TARGET" '(objectClass=Person)' sAMAccountName #accounts names info  
  
ldapsearch -h TARGETIP -x -b "DC=NAMINGTARGET,DC=TARGET" '(objectClass=User)' sAMAccountName|grep sAMAccountName|awk '{print $2}' # List of usernames