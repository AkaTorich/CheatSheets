```shell-session
SysRq@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

root /bin/bash
sync /bin/sync
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

# awk: print everything  
awk '{print}' <file>  
awk '{print $0}' <file>  
  
# awk: print n-th column   
awk '{print $n}' <file>  
  
# awk: add line counters to file  
awk '{++counter} {print counter "\t" $0}' <file>  
  
# awk: search for IPv4 address  
awk '/[0-9].[0-9].[0-9].[0-9]/' <file>  
  
# awk: search for IPv6 address  
awk '/[a-zA-Z0-9]:[a-zA-Z0-9]/ || /[a-zA-Z0-9]::[a-zA-Z0-9]/' <file>  
  
# awk: search for mail address  
awk '/[@]/' <file>  
  
# awk: filter mail address on n th column  
# example  
# username: test    password: password123   mail: test@example.com  
awk '/[@]/ {print $6}' <file>  
  
# awk: pattern matching  
awk '/pattern/' <file>  
  
# awk: match character set  
echo -e "Call\nTall\nBall" | awk '/[CT]all/'  
  
# awk: match exclusive character set  
echo -e "Call\nTall\nBall" | awk '/[^CT]all/'  
  
# awk: zero or one occurrence  
echo -e "Colour\nColor" | awk '/Colou?r/'  
  
# awk: zero or more occurrence  
echo -e "ca\ncat\ncatt" | awk '/cat*/'  
  
# awk: for loop  
awk 'BEGIN {for (i=1; i<10; ++i) print i}'