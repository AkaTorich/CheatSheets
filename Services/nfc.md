kali@kali:~$ mkdir home  
kali@kali:~$ sudo mount -o nolock TARGET:/home ~/home/  
make user with this group  
kali@kali:~$ sudo sed -i -e 's/1001/1014/g' /etc/passwd  
^login like user whith this group to read files  
  
  
showmount -e 10.10.10.34  
mount -t nfs -o vers=3 10.10.10.34:/var/nfsshare /mnt/jail/nfsshare  
  
nmap -sV -p 111 --script=rpcinfo TARGET