Now we have an image lets run it using the `docker run` command. This will create a writeable container, and start it using the specified command.

#### Example
Run the following command: `docker run docker/whalesay cowsay Hello there!`{{execute}}

This should print out the Docker whale ASCII image.

*The first time you run an image, the docker looks for it on your local system. If the image isn’t there, then docker will download it from the hub.*

#### Running our python web app image

Back to our Python web app, let's run our image: `docker run -p 8000:8000 --name mycontainer myimage:mytag`{{execute}}

The command above will run our image in a newly created container. The `-p` flag will make Docker bind port 8000 of the container to TCP port 8000 on the host machine. The `--name` flag will name the container `mycontainer`, this makes it easier to find later. If the `--name` flag is not specified the Docker will automatically generate and assign a name for you.

If all goes well, this should start the image in a new container and print the following:
```
 * Serving Flask app "server" (lazy loading)
 * Environment: production
 WARNING: Do not use the development server in a production environment.
 Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://0.0.0.0:8000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 555-356-043
```

Using the link below you should be able to view the webpage:<br>
Render port 8000: https://[[HOST_SUBDOMAIN]]-8000-[[KATACODA_HOST]].environments.katacoda.com/

When you're ready press <kbd>Ctrl</kbd>+<kbd>C</kbd>, this will stop the container.

#### Reusing a container

Running `docker ps -a`{{execute}}, we can see the myimage container is still in the system but the status column states that it has exited. 

To restart the container we use the `docker start` command. This time instead of specifying the image name we specify the container name that we assigned.

`docker start myconatiner`{{execute}}

This will restart the container but detached from the terminal. Adding the `--attach` flag will force docker to attach the container to the terminal the same as when we ran the `docker run` command.

#### Listing running containers

Now that our container is running in detached mode, we need to know if it is running or has exited. 

Running `docker ps`{{execute}} will show that our container is running and is binding port 8000 to port 8000.

#### Stopping a running container 

Once we have finished with our container we need to stop it.

Using `docker stop mycontainer`{{execute}}, will stop the container but again not remove it. This allows us to start the container again if needed.