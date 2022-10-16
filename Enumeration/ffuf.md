##### Enum local ports
```bash
$ for i in $(seq 1 65536); do echo $i >> ports; done

$ ffuf -u http://staging.love.htb/beta.php -timeout 1 -d 'file=http://127.0.0.1:FUZZ&read=Scan+File' -w ports.lst -H 'Content-Type: application/x-www-form-urlencoded'
```
##### Enum Subdomains
```bash
$ ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://sneakycorp.htb/ -H “Host: FUZZ.sneakycorp.htb” -fs 185
```
