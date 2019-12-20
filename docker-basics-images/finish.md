
You have completed this scenario. Please feel free to play around with docker using this environment.

Here are some of the commands we used in this scenario with links to the Docker documention.

#### Listing Images

`docker images`

https://docs.docker.com/engine/reference/commandline/images/

#### Listing Containers

`docker ps`

https://docs.docker.com/engine/reference/commandline/ps/

#### Building an Image

`docker build -t myimage:mytag .`

https://docs.docker.com/engine/reference/commandline/build/

#### Removing an Image

`docker rmi myimage`

https://docs.docker.com/engine/reference/commandline/rmi/

#### Running a Container

`docker run docker/whalesay cowsay Hello there!`

https://docs.docker.com/engine/reference/commandline/run/

#### Starting a Container

`docker start mycontainer`

https://docs.docker.com/engine/reference/commandline/start/

#### Stoping a Container

`docker stop mycontainer`

https://docs.docker.com/engine/reference/commandline/stop/

#### Removing a Container

`docker rm mycontainer`

https://docs.docker.com/engine/reference/commandline/rm/

#### Running commands in a running container

`docker exec -ti mycontainer /bin/sh` 

https://docs.docker.com/engine/reference/commandline/exec/

#### Running a docker-compose file

`docker-compose up` 

https://docs.docker.com/compose/reference/up/

#### Starting a docker-compose file

`docker-compose start` 

https://docs.docker.com/compose/reference/start/

#### Stopping a docker-compose file

`docker-compose stop` 

https://docs.docker.com/compose/reference/stop/

#### Clearing a docker-compose file

`docker-compose down` 

https://docs.docker.com/compose/reference/down/