## 1.2 Architectural Fundamentals
* PostgreSQL uses a client/server model  
* It consists of cooperating processes  
* A server process, which  
  * manages the database files  
  * accepts connections to the database from the client
  * performs actions on behalf of the client  
  * it is called `postgres`  
* a client (frontend) application) that wants to perform database operations  
  * clients are diverse  
  * most are programmed by the users of postgres  
  * but some are supplied with the postgres distribution.  
  * examples include:  
    * a text-oriented tool  
    * a graphical application  
    * a web server that accesses the database  
    * a specialized db maintenance tool.  
* The client and server can be on different hosts.  
* In this case, they communicate over TCP/IP.
* If they are on the same host, they might communicate over unix domain sockets.
* The postgres server can handle concurrent connections.  
* It does this by forking a new process for each connection.  
* The forked (child) process is responsible for the connection for its entire lifetime.  
* Thus, the supervisor server process is always running, waiting for client connections  
* The client and associated server processes come and go.
**Section Summary**
* Postgres operates using a client/server architecture.  
* The server application is responsible for managing the files of the database, and accepting incoming connections. It performs actions on behalf of the client, including retrieving data and making modifications.  
* The client (frontend) applications make requests of the server, communicating via TCP/IP if on different machines, or bypassing the network stack if on the same machine.  
* The client applications are usually written by users, but some client applications, such as database administration tools, are distributed with Postgres.  
* The server application consists of a supervisor process, which is forked for each incoming connection.  
* The forked child server process manages the client of the associated connection for the lifetime of the connection, with no interference by the server application.  
* Therefore, child server processes and connections are ephemeral, while the supervisor server process is always running.
**Shorter summary**
* The architecture of Postgres follows a client/server model, in which servers manage access to a central resource, namely the database files, and client makes coherent requests of the server in order to have server do data processing.   
* When a client connects to the server, the supervisor server process (called `postgres`) forks itself, and the child process is responsible for managing the client's requests for the lifetime of the connection.  
* Clients communicate with the server using TCP/IP. 
## 1.3 Creating a Database
* A PostgreSQL server can manage many databases.  
* A separate database is typically used for each project or for each user.  
* Creating a database:[^1]
```bash
$ createdb mydb
```
- If this produces no response, then it was successful.
- If you leave off the name, then `createdb` will create a database with the user's name.
- An owner of a databse can destroy it using the following command
```bash
$ dropdb mydb
```
## 1.4 Accessing a Database
- You can access a database by doing the following:
	- Running the Postgres terminal program, called `psql`
	- Usie a graphical frontend (admin tool)
	- Write a custom application using language bindings
- Use [[psql]] to connect to the database. Let's say we're connecting to `mydb`. Then 
```bash
psql mydb
```
- If the prompt ends with `>` (resp. `#`), you are a database (resp. super)user.
	- Being a superuser means you are not subject to access controls.
- Some commands:
	- `\h [commands]` -- SQL help
	- `\q` -- exit psql
- 
[^1]:  It felt weird to me that there are wrappers for functionality programmable through sql. I think the reason these wrappers exist is to adhere to the unix philosophy, and allow tasks to be performed by system administrators utilizing scripts and through interactive sessions.
