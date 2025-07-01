`psql [OPTION]... [DBNAME [USERNAME]]
- All arguments are optional. First unnamed argument is the name of the database
- Second is the db user name.
## Connecting to a Database
- `psql` is an example of a client application.
- In order to connect to a database you need to know the following:
	- host name of server (default localhost)
	- port number of server (decided at compile time, usually 5432)
	- what database user name you want to connect as (defaults to OS user name) 
	- the name of the database you want to connect to (defaults to database user name)
- a `~/.pgpass` file can be used to avoid having to type in passwords

### Useful links 
- [psql official documentation](https://www.postgresql.org/docs/current/app-psql.html)
