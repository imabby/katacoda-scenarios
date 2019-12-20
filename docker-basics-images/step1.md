
Below are some basic commands that you may need to be aware of as they are used throughout the scenarios.
I've included links to the corresponding docker documentation.

#### Listing Images

`docker images`{{execute}}

Running the command above will show all local top-level images, their repository and tags, and their size. Intermediate layers are not shown by default. The list is ordered by the most recently created images.

The SIZE is the cumulative space taken up by the image and all its parent images. This is also the disk space used by the contents of the Tar file created when you docker save an image.

An image will be listed more than once if it has multiple repository names or tags. This single image (identifiable by its matching IMAGE ID) uses up the SIZE listed only once.

The docker images command takes an optional [REPOSITORY[:TAG]] argument that restricts the list to images that match the argument. If you specify REPOSITORYbut no TAG, the docker images command lists all images in the given repository.
`docker images ubuntu`{{execute}}

https://docs.docker.com/engine/reference/commandline/images/

#### Listing Containers

`docker ps`{{execute}}

Lists all **running** containers. If you want to see all the containers, use the `-a` flag:
`docker ps -a`{{execute}}

https://docs.docker.com/engine/reference/commandline/ps/