
To build an image you must first create a `Dockerfile`. This is a text file that lists all the commands required to build an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.

Using the guide below we will create a `Dockerfile` which will create an image that contains a simple Python web app. We will then build the image.

#### Creating a dockerfile

Create a new Dockerfile via the CLI: `touch Dockerfile`{{execute}}

Next, open the Dockerifle in the editor: `Dockerfile`{{open}}

Most Dockerfiles will usually start with a base image (for example, ubuntu, centos). You can create a base image from sctrach but with so many images available you shouldn't need to. Check out [Docker Hub](https://hub.docker.com/) to see available images.

We will add a base image to our `Dockerfile` using the `FROM` instruction, followed by the image name.
<pre class="file" data-filename="Dockerfile" data-target="append">FROM python:3-alpine
</pre>

#### Copying the code

Now we need to copy our source code to the image.

First, we add the `WORKDIR` instruction which will set the working directory for our image. 
Next, we need to copy the source code for our python app to the image using the `COPY` instruction. 

<pre class="file" data-filename="Dockerfile" data-target="append">WORKDIR /usr/src/app
COPY ./assets .
</pre>

Here, the first argument is specifying the source file/path and the second argument is where we want to store the files in the image.

#### Exposing ports

Exposing a port in a `Dockerfile` lets Docker know which ports the container will be listening to. For example, for a web server you may want to expose port 80 or port 443. Add the following to your `Dockerfile`.

<pre class="file" data-filename="Dockerfile" data-target="append">EXPOSE 8000
</pre>

#### Running a command

The `RUN` instruction lets users execute commands in a new layer. For example, to install software packages or run shell scripts. 
We want to tell docker to run pip and install the dependencies for our web app.
<pre class="file" data-filename="Dockerfile" data-target="append">RUN pip install -qr requirements.txt
</pre>

#### Setting the default command

The `CMD` instruction allows you to set the default command for an executing container. This will be executed only if you do not specify a command when running the image. If you run the image with a command, the default command will be ignored. If you list more than one CMD in a `Dockerfile` then only the last CMD will take effect.

The CMD instruction has three forms:
* CMD ["executable","param1","param2"] (exec form, this is the preferred form)
* CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
* CMD command param1 param2 (shell form)

<pre class="file" data-filename="Dockerfile" data-target="append">CMD ["python3", "./server.py"]
</pre>

#### The finished Dockerfile

Your `Dockerfile` should now look like the following:
```
FROM python:3-alpine

WORKDIR /usr/src/app
COPY ./assets .

EXPOSE 8000

RUN pip install -qr requirements.txt

CMD ["python3", "./server.py"]
``` 

For a full explanation of all available instructions, see the following link:<br/>
[https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)

#### Building the image

Once the Dockerfile has been written we can now build the image with the docker command: `docker build .`{{execute}}

If the command completed successfully, we should be able to see the new image with the docker command: `docker images`{{execute}}

#### Tagging the image

As you can see the image was created without any information such as name or version. This can make it difficult to know which image is which. To avoid this we can use Docker tags. Docker tags are similar to GIT tags in that they allow you to alias the ID of your image.

Lets rebuild our image with a new tag: `docker build -t myimage:mytag .`{{execute}} 

Running `docker images`{{execute}}, you should now see an image whose repository is myimage and tag is mytag.

If you don't specify a tag, it is given the `latest` tag by default.<br/>
**The onus is on the developer to tag the images properly such that latest always points to the `latest` stable release of the image.**

See the following link for a very good explanation of tags:<br/>
[https://www.freecodecamp.org/news/an-introduction-to-docker-tags-9b5395636c2a/](https://www.freecodecamp.org/news/an-introduction-to-docker-tags-9b5395636c2a/)
