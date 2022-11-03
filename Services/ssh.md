```bash
доступ может быть как только по юзернейму и адресу так и ключем авторизации как указано ниже  
root@buben:~# ssh -i root_id_rsa root@passage.htb  
  
  
ssh -p 2222  kristi@10.10.10.247 -oHostKeyAlgorithms=+ssh-rsa #if error about key  
  
IF sign_and_send_pubkey: no mutual signature supported  
ssh hype@10.10.10.79 -o PubkeyAcceptedKeyTypes=+ssh-rsa  
  
#########################################################  
Have you ever tried to SSH into a server and revieved the following error?  
  
Well that’s probably becuase you are using a bit of kit with legacy software or firmware.  
  
Then when you try to SSH and you add diffie-hellman-group1-sh1 you get the following back?  
  
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 root@192.168.2.1  
  
Unable to negotiate with 192.168.2.1 port 22: no matching host key type found. Their offer: ssh-rsa  
  
No worries, we can fix that:  
  
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa root@192.168.2.1  
  
but we could go even wilder:  
  
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1 -oHostKeyAlgorithms=+ssh-dss,ssh-rsa root@192.168.2.1  
  
I’ve not read the specs but there’s obviously a range of cipher configuirations you can set with:  
  
-oKexAlgorithms  
  
-oHostKeyAlgorithms  
  
You can check the config by running:  
  
ssh -Q cipher # ciphers u can use  
ssh -Q mac # MAC types  
ssh -Q key # Public key  
ssh -Q kex # Key Exchange Algos
```
`$ ssh username@192.168.1.101`
_Unable to negotiate with 192.168.1.101 port 22: no matching host key type found. Their offer: ssh-rsa,ssh-dss_
USE 
`$ ssh username@192,168.1.101 -oHostKeyAlgorithms=+ssh-dss`