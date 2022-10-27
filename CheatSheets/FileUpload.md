# File Upload

If try to upload webshell to victim check how the exploit is done. Check any bad characters

e.g. $XXX is taken as variable in bash, need to use $ to escape

### [](https://github.com/russweir/OSCP-cheatsheet/blob/master/File%20upload.md#webdav)WebDav

upload file:  
curl -T '/path/to/local/file.txt' '[https://example.com/test/](https://example.com/test/)'  
curl --upload-file <file> http://<IP>/test/<filename>

curl -X MOVE --header 'Destination:[http://example.org/new.txt](http://example.org/new.txt)' '[https://example.com/old.txt](https://example.com/old.txt)'  
curl -X COPY --header 'Destination:[http://example.org/new.txt](http://example.org/new.txt)' '[https://example.com/old.txt](https://example.com/old.txt)'

login:  
curl --user 'user:pass' '[https://example.com](https://example.com/)'

Upload bypass:  
[https://www.owasp.org/index.php/Unrestricted_File_Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload)  
[https://soroush.secproject.com/blog/tag/unrestricted-file-upload/](https://soroush.secproject.com/blog/tag/unrestricted-file-upload/)

IIS 6.0 or below Asp > upload as test.txt, copy or move file as test.asp;.txt

Php > upload as pHp / phP / test.php.jpg /

php - phtml, .php, .php3, .php4, .php5, and .inc

asp - asp, .aspx

perl - .pl, .pm, .cgi, .lib

jsp - .jsp, .jspx, .jsw, .jsv, and .jspf

Coldfusion - .cfm, .cfml, .cfc, .dbm

Add:

GIF89a;

### [](https://github.com/russweir/OSCP-cheatsheet/blob/master/File%20upload.md#options)Options

Use options to check for upload method.

upload function. Is put allowed?