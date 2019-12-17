
To build an image you must first create a `Dockerfile`. This `Dockerfile` is a text file that lists all the commands required to build an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.

Using the guide below we will create a `Dockerfile` which will create an image that contains a simple Python web app. We will then build and run the image.

#### Creating a dockerfile
Create a new Dockerfile via the CLI: `touch Dockerile`{{execute}}

Next, open the Dockerifle in the editor: `Dockerile`{{open}}

Most `Dockerfiles` will usually start with a base image (for example, ubuntu, centos). You can create a base image from sctrach but with so many images available you shouldn't need to. Check out [Docker Hub|https://hub.docker.com/] to see available images.

We will add a base image to our `Dockerfile` using the `FROM` instruction, followed by the image name.
<pre class="file" data-filename="Dockerfile" data-target="append">FROM python:3-alpine
</pre>

#### Copying the code
Now we need to copy our source code form our local machine to the image.

First, we must add the `WORKDIR` instruction to set the working directory for our app. 
Next we will copy the files from our local machine using the `COPY` instruction. The first argument specifies the source file/path and the second is the destination in the image. The `COPY` instruction below will copy all files in the `sourcecode` folder to the `/usr/src/app` folder inside the image.

<pre class="file" data-filename="Dockerfile" data-target="append">WORKDIR /usr/src/app
COPY ./requirements.txt .
COPY ./server.py .
</pre>

#### Exposing ports
Exposing a port in a `Dockerfile` lets Docker know which ports the container will be listening to. For example, for a web server you may want to expose port 80 or port 443. Add the following to your `Dockerfile`.
<pre class="file" data-filename="Dockerfile" data-target="append">EXPOSE 8000
</pre>

#### Running a command
Next we want to tell docker to run pip to install our dependencies. We can do this using the `RUN` instruction. This instruction will execute any commands in a new layer on top of the current image.
<pre class="file" data-filename="Dockerfile" data-target="append">RUN pip install -qr requirements.txt
</pre>

#### CMD instruction
The `CMD` instruction sets the default for an executing container. This lets Docker know how to run the application we packaged in the image. The `CMD` instruction uses the following format `CMD ["executable","param1","param2"]`.
There can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take effect.

<pre class="file" data-filename="Dockerfile" data-target="append">CMD ["python3", "./server.py"]
</pre>

#### Save the Dockerfile

Your `Dockerfile` should now look like the following:
```
FROM python:3-alpine
WORKDIR /usr/src/app
COPY ./requirements.txt .
COPY ./server.py .
EXPOSE 8000
RUN pip install -qr requirements.txt
CMD ["python3", "./server.py"]
``` {{copy}}

Save the file using `Ctrl + O` and exit using `Ctrl + X`.


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
