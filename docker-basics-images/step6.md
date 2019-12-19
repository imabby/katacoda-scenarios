Let's start our Python web app using Docker Compose.

#### Creating a docker-compose.yml file

Create a new Dockerfile via the CLI: `touch docker-compose.yml`{{execute}}

Next, open the Dockerifle in the editor: `docker-compose.yml`{{open}}

A docker-compose file must contain the `version` and `services` keywords as a minimum. So lets add those in now:
<pre class="file" data-filename="docker-compose.yml" data-target="append">version: '3'
services:</pre>

#### Create a service

Now we need to create a service. This is as simple as adding the following to our docker-compose file:
<pre class="file" data-filename="docker-compose.yml" data-target="append"> myservice:</pre>

#### Setting the container name

When we used the `docker run` command we specified a name for our container. We can do the same in our compose file:
<pre class="file" data-filename="docker-compose.yml" data-target="append"> container_name: mycomposer</pre>

If we do not specify a container name, Docker will automatically generate one based on the folder the file is in and the service name.
For example, if the following was in a folder called `mycomposers` then the container name would be mycomposers_myservice_1.
```
version: '3'
services:
 myservice:
 ...
```

#### Specify the image to use

Now we need to to provide either a build or an image from the Docker registry. You cannot have both.

* A custom Docker image will be built based on the Dockerfile provided by the build path OR
* Docker hub will supply all the necessary commands and setup to make the image build and run successfully.

Since we have already built our image we can specify it using the image repository and tag:
<pre class="file" data-filename="docker-compose.yml" data-target="append"> image: myimage:mytag</pre>

If the image does not exist, Compose attempts to pull it, unless you have also specified build, in which case it builds it using the specified options and tags it with the specified tag.

#### Bind the required ports

Since we are running a web application, we will need to expose port 8000 for us to view the web page.
To do this we simply list the ports we want to expose and bind them to a local port. Similar to what we did previously in our `docker run` command. 

Add the following to bind port 8001 on our local machine to port 8000 of the host:
<pre class="file" data-filename="docker-compose.yml" data-target="append"> ports:
 - 8001:8000</pre>

We are using port 8001 here because we still have our previous container running binding port 8000. If we try to run another container on this port will get an error. Try it if you don't believe me!!

#### Running Docker Compose

Once the docker-compose file has been written we can now run it with the command: `docker-compose up`{{execute}}

Using the link below you should be able to view the webpage:<br>
https://[[HOST_SUBDOMAIN]]-8001-[[KATACODA_HOST]].environments.katacoda.com/

When you're ready press <kbd>Ctrl</kbd>+<kbd>C</kbd>, this will stop the container.