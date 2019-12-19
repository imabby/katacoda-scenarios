
#### Inspecting a container

Docker inspect provides detailed information on constructs controlled by Docker.
By default, docker inspect will render results in a JSON array.

FIrst lets recreate our container but this time in dettached mode: `docker run -p 8000:8000 -d --name mycontainer myimage:mytag`{{execute}}

Now lets inspect our container: `docker inspect mycontainer`{{execute}}

This will list the complete information of the container. Most of the elements are pretty easy to understand but a few of them may not be as obvious. You will get a pretty long output here.

For the most part, you can pick out any field from the JSON in a fairly straightforward manner: 
`docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mycontainer`{{execute}}

#### Viewing container logs

**Note: this command is only functional for containers that are started with the json-file or journald logging driver.**

The `docker logs` command shows information logged by a running container. The information that is logged and the format of the log depends almost entirely on the container's endpoint command.

By default, `docker logs` shows the command's output just as it would appear if you ran the command interactively in a terminal. UNIX and Linux commands typically open three I/O streams when they run, called STDIN, STDOUT, and STDERR. STDIN is the command’s input stream, which may include input from the keyboard or input from another command. STDOUT is usually a command’s normal output, and STDERR is typically used to output error messages. By default, docker logs shows the command’s STDOUT and STDERR. To read more about I/O and Linux, see the Linux Documentation Project article on I/O redirection.

Running `docker logs mycontainer`{{execute}} will show the logs for our Python web app.

You can use the `--follow` flag to continue streaming the new output from the container’s STDOUT and STDERR.
`docker logs --follow mycontainer`{{execute}}

Press <kbd>Ctrl</kbd>+<kbd>C</kbd> to return to shell.

#### Running commands in a running container

The `docker exec` command runs a new command in a running container.

The command started using docker exec only runs while the container’s primary process (PID 1) is running, and it is not restarted if the container is restarted.

COMMAND will run in the default directory of the container. If the underlying image has a custom directory specified with the WORKDIR directive in its Dockerfile, this will be used instead.

COMMAND should be an executable, a chained or a quoted command will not work. Example: `docker exec -ti my_container "echo a && echo b"` will not work, but `docker exec -ti my_container sh -c "echo a && echo b"` will.

Run `docker exec mycontainer "echo Hello World"`{{execute}}, this will output "Hello World" to the terminal.

You can also start Bash session in the running container using the following:
`docker exec -ti mycontaier /bin/bash`{{execute}}

This will let you peek around inside the container and run commands if needed. You can kind of think of it like running SSH if that helps make sense to you.

Type `exit`{{exectue}} to leave the Bash session.

