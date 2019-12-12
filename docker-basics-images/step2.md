### Dockerfiles

To build an image you must first create a `Dockerfile`. This `Dockerfile` is a text file that lists all the commands required to build an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.

#### Creating a dockerfile
In the terminal, create a file with the name "Dockerfile".
```
touch Dockerfile
```

Most `Dockerfiles` will usually start with a base image (for example, ubuntu, centos). You can create a base image from sctrach but with so many images available you shouldn't need to. Check out [Docker Hub|https://hub.docker.com/] to see available images.

To add a base image we use the `FROM` command, followed by the image name.
```
# Filename: Dockerfile
FROM python:3-alpine
```

#### Copying the code
Now we need to copy our source code form our local machine to the image.

First, we must use the `WORKDIR` instruction to set the working directory for our app. 
Next we copy the files from our local machine using the `COPY` instruction. The first argument specifies the source file/path and the second is the destination in the image. The `COPY` instruction below will copy all files in the `sourcecode` folder to the `/usr/src/app` folder inside the image.

```
FROM python:3-alpine
WORKDIR /usr/src/app
COPY ./sourcecode .
```

#### Exposing ports
Exposing a port in a `Dockerfile` lets Docker know which ports the container will be listening to. For example, for a web server you may want to expose port 80 or port 443.

```
FROM python:3-alpine
WORKDIR /usr/src/app
COPY ./sourcecode .
EXPOSE 8000
```

#### Running a command
Next we want to run pip to install our dependencies. We can do this using the `RUN` instruction. This instruction will execute any commands in a new layer on top of the current image.

```
FROM python:3-alpine
WORKDIR /usr/src/app
COPY ./sourcecode .
EXPOSE 8000
RUN pip install -qr requirements.txt
```

#### CMD instruction
The `CMD` instruction sets the default for an executing container. This lets Docker know how to run the application we packaged in the image. The `CMD` instruction uses the following format `CMD ["executable","param1","param2"]`.
There can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take effect.

```
FROM python:3-alpine
WORKDIR /usr/src/app
COPY ./sourcecode .
EXPOSE 8000
RUN pip install -qr requirements.txt
CMD ["python3", "./server.py"]
```

#### Building the image

Once you've written and saved the Dockerfile we can then build the image. The following command will create the image using the instructions in the `Dockerfile`.

```
docker build .
```

Running `docker images` should now show the newly created image. As you can see the image was created without a repository and tag.
This can make it difficult to know which image is which. We could use `docker tag` to tag our newly created image but this introduces a another step. To make things easier we can tag the image when we build them using `-t tagname` parameter.
```
docker build -t myapp .
```

Running `docker images` should now show you image with the `myapp` name and the `latest` tag. The latest tag is added automatically if now tag is given. The following will build the image again but with the `version1` tag. 

```
docker build -t myapp:version1 .
```
