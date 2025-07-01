This tutorial is designed to be pastable line by line (or in the specified blocks) into a terminal session.
```bash
# Run postgres docker container with password "password".
# Setting the password using -e (for environment) is critical, or the container won't start.
# Using -d (for detach) detaches the container, and returns the container id for use in the next step.
POSTGRES_CONTAINER_ID=$(docker run -d -e POSTGRES_PASSWORD=password postgres:17)
# To access the command line tools, we need to exec into the container using `bash`, because
#   they will not be installed on our host machine. To do this, we need to use the container
#   id saved in the previous step. The general syntax is
# docker exec -it <container_id_or_name> bash.
# Using `exec -it [container] bash` is very common with docker.
docker exec -it $POSTGRES_CONTAINER_ID bash
# At this point, your prompt sohuld look like:
#
#  root@<alphanumeric_string>:/#
#
# This means we are inside the docker container, logged in as the root user.
```

```bash
# Next, we call the interactive text frontend for postgres, psql. `psql` can be run most simply as follows: 
psql 
# You should get an error at this point; role "root" does not exist. By default, psql logs #   in with a username matching the current OS user; because we exec'ed into the docker 
#   container, this means that psql is picking up the root user from the container, rather
#   than the surrounding environment.
# By default, the postgres:17 docker image creates a user called postgres. To log in as 
#   that user, we use the -U command line argument.
psql -U postgres
# Now, your output should look something like this:
#
#   psql (17.5 (Debian 17.5-1.pgdg120+1))
#   Type "help" for help.
#   
#   postgres=#
#
# This means we are inside psql.
```

```psql
-- Run this command first if you are pasting in blocks:
\pset pager off
-- This just ensures we don't enter a mode which requires user interaction, which would break our script.
-- In psql, some commands are as follows:
\? -- show help on backslash commands; I recommend skimming the output to see what commansd are available.
\conninfo -- gives useful connection info
-- Notice that the database name is also postgres. This is because once the (database) 
-- user name is determined, if the database name is not specified, it defaults to that user -- name.
-- If you're running psql inside the docker instance, you will also see that the connection 
-- is "via socket"; that means that in this case docker is using Unix domain sockets 
-- instead of TCP/IP for interprocess communication.

```