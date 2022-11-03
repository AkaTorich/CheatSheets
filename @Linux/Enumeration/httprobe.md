##### Check list domains for work 
github tomnomnom/httprobe
```bash
 cat $url/recon/finalassets.lst  |httprobe -s -p https:443 | sed 's/https\?:\/\///' | tr -d ':443' >> $url/recon/alive.lst #Enums open 443 port
```