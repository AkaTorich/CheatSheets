# nikto: use another port number  
nikto -h example.com -port 443,8080  
  
# nikto: write output to file  
nikto -o /absolute/path/report.html -Format htm -host 192.168.0.102  
  
# nikto: basic authentication  
nikto -id id:password -h 192.168.0.102  
  
# nikto: choose specific Tuning  
# 0 - File Upload  
# 1 - Interesting File / Seen in logs  
# 2 - Misconfiguration / Default File  
# 3 - Information Disclosure  
# 4 - Injection (XSS/Script/HTML)  
# 5 - Remote File Retrieval - Inside Web Root  
# 6 - Denial of Service  
# 7 - Remote File Retrieval - Server Wide  
# 8 - Command Execution / Remote Shell  
# 9 - SQL Injection  
# a - Authentication Bypass  
# b - Software Identification  
# c - Remote Source Inclusion  
nikto -Tuning 012 -h example.com  
  
# nikto: run nikto with all tunings except DOS  
nikto -Tuning x 6 -h example.com