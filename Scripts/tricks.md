find . -type f -exec md5sum {} \; | awk '{print $1' | sort | uniq -c | grep ' 1 ' | awk '{print $2}' > hashes  
  
find . -type f -exec md5sum {} \; | grep -f hashes  
  
diff -y file1 file2