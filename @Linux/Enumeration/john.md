/usr/sbin/keepass2john MyPasswords.kdbx  
  
# john: generate password list with permutations  
john --stdout --wordlist=wordListFile.txt --rules > newListName.txt  
  
# john: recognize hash algorithm and tries to crack it  
john hashFile  
  
# john: show results  
john hashFile --show   
  
# john: generate password list with permutations  
john --stdout --wordlist=wordListFile.txt --rules > newListName.txt  
  
# john: place where session will be stored  
$JOHN/john.pot  
  
# john: ignore specific user or expired shells  
john --show --shells=-expired,specificUser mypasswd  
  
# john: check if any root (UID 0) accounts got cracked  
john --show --users=0 mypasswd  
  
# john: display root account  
john --show --users=root mypasswd  
  
# john: check for privileged groups  
john --show --groups=0,1 mypasswd  
  
#john cracks MD5  
john hashFile --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-MD5