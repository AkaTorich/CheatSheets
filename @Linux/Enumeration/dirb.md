# dirb: bruteforce with basic authentication  
dirb http://target.com -u user:password  
  
# dirb: show not existing pages  
dirb -v http://target.com  
  
# dirb: not recursively  
dirb -r http://target.com  
  
# dirb: use wordlist  
dirb http://target.com /path/to/wordlist