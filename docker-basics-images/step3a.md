A container is an instance of an image. We can create, run, stop, or delete a container using the Docker CLI. We can connect a container to more than one networks, or even create a new image based on its current state.

Since images are read-only, Docker adds a read-write file system over the read-only file system of the image to create a container. 

Docker also creates a network interface so that the container can talk to the local host, attaches an available IP address to the container, and executes the process that you specified to run your application when defining the image.

Once you’ve successfully created a container, you can then run it in any environment without having to make changes.

