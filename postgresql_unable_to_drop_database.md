SQL Error [55006]: ERROR: database "lp" is being accessed by other users
  Detail: There is 1 other session using the database.

occurs when you're trying to perform an operation on a database that requires exclusive access (such as dropping, altering, 
or renaming the database), 
but there is still an active connection or session using it.

Here’s how to resolve it:
1. Check Active connections

```
SELECT pid, usename, application_name, client_addr, state, query 
FROM pg_stat_activity 
WHERE datname = 'lp';
```
This will give you a list of active connections to the lp database.

2. Terminate Active sessions
```
SELECT pg_terminate_backend(pid) 
FROM pg_stat_activity 
WHERE datname = 'lp' AND pid <> pg_backend_pid();
```
This will terminate all sessions except the one you're currently using.

3. Retry the Operation
