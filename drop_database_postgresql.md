1. Connect to postgresql server with command : 
```
psql -h <host> -U <postgres_user>
```
2. Drop single database command:
   ```
    drop database <database_name>; 
   ```
4. Drop multiple databases using wildcards. in this example I will delete all databases with prefix 'fix'. 
  ```
  SELECT 'DROP DATABASE ' || quote_ident(datname) || ';'
  FROM pg_database
  WHERE datname LIKE 'fix%' AND datistemplate=false;
```
the command above will produce multiple lines of delete database command. in here I have 4 databases with prefix 'fix'
```
DROP DATABASE fix2;
DROP DATABASE fix3;
DROP DATABASE fix4;
DROP DATABASE fix5;
```
5. Delete all databases except few ones in postgres
```
SELECT 'DROP DATABASE ' || quote_ident(datname) || ';'
FROM pg_database
WHERE datname not in ('postgres','dbtest') AND datistemplate=false;
```   
