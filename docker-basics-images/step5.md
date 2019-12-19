Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. 

Using Compose is basically a three-step process:
* Define your app’s environment with a Dockerfile so it can be reproduced anywhere.
* Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.
* Run `docker-compose up` and Compose starts and runs your entire app.

In short, Docker Compose works by applying many rules declared within a single docker-compose.yml configuration file.
Almost every rule replaces a specific Docker command so that in the end we just need to run:
`docker-compose up`

A docker-compose.yml looks like this:
```
version: '3'
services:
  myservice
    image:myimage:latest
    ports:
      ...
    volumes:
      ...
```

#### Version

There are currently three versions of the Compose file format:
* Version 1, the legacy format. This is specified by omitting a version key at the root of the YAML.
* Version 2.x. This is specified with a version: '2' or version: '2.1', etc., entry at the root of the YAML.
* Version 3.x, the latest and recommended version, designed to be cross-compatible between Compose and the Docker Engine’s swarm mode. This is specified with a version: '3' or version: '3.1', etc., entry at the root of the YAML.

See https://docs.docker.com/compose/compose-file/ for more information

#### Services

First of all, services refer to containers' configuration.

In the case of our Python web app we ran the following command:
`docker run -p 8000:8000 -d --name mycontainer myimage:mytag`

In docker compose this would translate to:
```
version: '3'
services:
  mycomposer:
    container_name: mycontainer
    image: myimage:mytag
    ports:
      - 8000:8000
```

#### Volumes

Volumes are physical areas of disk space shared between the host and a container, or even between containers. In other words, a volume is a shared directory in the host, visible from some or all containers.

There are three types of volumes: anonymous, named, and host ones. Docker manages both anonymous and named volumes, automatically mounting them in self-generated directories in the host. 

* A host volume lives on the Docker host's filesystem and can be accessed from within the container. To create a host volume:
```
services: 
  mycomposer:
    volumes: 
      - /path/on/host:/path/in/container
```

* An anonymous volume is useful for when you would rather have Docker handle where the files are stored. It can be difficult, however, to refer to the same volume over time when it is an anonymous volumes. To create an anonymous volume:
```
services: 
  mycomposer:
    volumes: 
      - /path/on/host
```

* A named volume is similar to an anonymous volume. Docker manages where on disk the volume is created, but you give it a volume name. To create a named volume:
```
services: 
  mycomposer:
    volumes: 
      - somevolumename:/path/on/host

volumes:
  somevolumename: 
```

While anonymous volumes were useful with older versions of Docker (pre 1.9), named ones are the suggested way to go nowadays. Host volumes also allow us to specify an existing folder in the host.

We can mount a volume in read-only mode by appending :ro to the rule, like for the /home folder (we don't want a Docker container erasing our users by mistake).

#### Building an Image

If we have a Dockerfile, we may need to build the image first before runing the container.
We can do this using the build keyword:
```
services: 
  mycomposer:
    build: /path/to/dockerfile/
```

You can also specify an URL if needed.:
```
services: 
  mycomposer:
    build: https://github.com/my-company/my-project.git
```

#### Exposing Ports

Similar to using the `-p 8000:8000` flag in the `docker run` command. We can use the `expose` keyword to bind the required ports:
```
version: '3'
services:
  mycomposer:
    image: myimage:mytag
    ports:
      - 8000:8000
```

#### Dependencies

Often, we need to create a dependency chain between our services, so that some services get loaded before (and unloaded after) other ones. We can achieve this result through the depends_on keyword:
```version: '3'
services:
  mycomposer:
    image: myimage:mytag
    depends_on:
      - myothercontainer
```

We should be aware, however, that Compose will not wait for the zookeeper service to finish loading before starting the kafka service: it will simply wait for it to start.

#### Environment Variables

Working with environment variables is easy in Compose. We can define static environment variables, and also define dynamic variables with the ${} notation:
```version: '3'
services:
  mycomposer:
    image: myimage:mytag
    environment:
      DB: mydb
      USER: "${USER}"
```

There are different methods to provide those values to Compose.

For example, one is setting them in a .env file in the same directory, structured like a .properties file, key=value:
```
POSTGRES_VERSION=alpine
USER=foo
```

Otherwise, we can set them in the OS before calling the command:
```
export POSTGRES_VERSION=alpine
export USER=foo
docker-compose up
```
We can mix the approaches, but let's keep in mind that Compose uses the following priority order, overwriting the less important with the higher ones:
* Compose file
* Shell environment variables
* Environment file
* Dockerfile
* Variable not defined

#### Starting Up

We've seen that we can create and start the containers, the networks, and the volumes defined in the configuration with up:
`docker-compose up`

After the first time, however, we can simply use start to start the services:
`docker-compose start`

Compose can also run in the background as a daemon when launched with the -d option:
`docker-compose up -d`

#### Shutting Down

To safely stop the active services, we can use stop, which will preserve containers, volumes, and networks, along with every modification made to them:
`docker-compose stop`

To reset the status of our project, instead, we simply run down, which will destroy everything with only the exception of external volumes:
`docker-compose down`