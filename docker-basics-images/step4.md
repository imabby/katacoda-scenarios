
#### Inspecting a container

Docker inspect provides detailed information on constructs controlled by Docker.
By default, docker inspect will render results in a JSON array.

First, let's recreate our container but this time in detached mode: 
`docker run -p 8000:8000 -d --name mycontainer myimage:mytag`{{execute}}

Now let's inspect our container: `docker inspect mycontainer`{{execute}}

This will list all the information about the container. Most of the elements are pretty easy to understand but a few of them may not be as obvious. You will get a pretty long output here.

You can also pick out most fields from the JSON in a fairly straightforward manner: 
`docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mycontainer`{{execute}}

#### Viewing container logs

**Note: this command is only functional for containers that are started with the json-file or journald logging driver.**

The `docker logs` command shows information logged by a running container. The information that is logged and the format of the log depends almost entirely on the container's endpoint command.

By default, `docker logs` shows the command's output just as it would appear if you run the command interactively in a terminal. 

View the logs for our Python web app: `docker logs mycontainer`{{execute}}

You can also use the `--follow` flag to stream the output from the container:
`docker logs --follow mycontainer`{{execute}}

Press <kbd>Ctrl</kbd>+<kbd>C</kbd> to return to shell.

#### Running commands in a running container

The `docker exec` command runs a new command in a running container.

The command started using docker exec only runs while the container’s primary process (PID 1) is running, and it is not restarted if the container is restarted. It will also run in the default directory of the container. If the underlying image has a custom directory specified with the WORKDIR directive in its Dockerfile, this will be used instead. The command given should be an executable, a chained or a quoted command will not work. 

For Example:
`docker exec -ti my_container "echo a && echo b"` 
will not work, but: 
`docker exec -ti my_container sh -c "echo a && echo b"` 
will.

Let print out "Hello World" using our running container: `docker exec mycontainer echo Hello World`{{execute}}

You can also start a bash session. This will let you peek around inside the container and run commands if needed. You can kind of think of it like running SSH if that helps make sense to you.
Lets opena bash session on our container: `docker exec -ti mycontainer /bin/sh`{{execute}}

When your ready run `exit`{{exectue}} to leave the Bash session.
