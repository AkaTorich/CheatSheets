apt install ocl-icd-libopencl1 nvidia-cuda-toolkit

hashcat --stdout -a 3 Morris19?d?d?s > /root/jail.words  
^Generate passlist  
  
# hashcat: crack nt hashes with rule-based dictionary attack  
hashcat -m 1000 hashFile -w 3 -a 0 -r OneRule.rule wordlist1.txt [wordlist2.txt [...]]  
  
# hashcat: common hash types  
1000: nt  
3000: lm  
2100: dccs  
5600: ntlmv2  
7300: ipmi  
13100: kerberoast (etype 23)  
19700: kerberoast (etype 18)  
  
# hashcat: show output  
hashcat -m 1000 hashFile --show  
  
# hashcat: include username in output and show special chars  
hashcat -m 1000 hashFile --show --username --outfile-autohex-disable