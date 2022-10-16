#START  
for i in $(ls *.JPG); do keepass2john -k $i MyPasswords.kdbx | sed "s/MyPasswords/%i/g" >> keypass_hashes; done  
  
hashcat -m 13400 -O keypass_hashes ../rockyou.txt #crack hashes  
apt install kpcli #install keypass tool  
kpcli --kdb MyPasswords.kdbx --key IM_FILE1111.JPG #open keypass db  
cd MyPasswrods #in kpcli cd to passwords if not do LS  
show -a -f 0 #show password id 0  
#END