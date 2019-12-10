## Images

A Docker image includes everything needed to run the executable codea and is made up of multiple layers. Each layer representing an instruction in the image’s Dockerfile. For example, the Dockerfile below would create three layers. The FROM statement creates a layer from the ubuntu image. The `COPY` line add files from your local machine and the `CMD` line specified what command to run inside the container.

```
FROM ubuntu:latest
COPY . /my-app
CMD sh /my-app/my-app
```

The layers are stacked on top of each other and each layer is only a set of differences from the layer before it. Developers can also reuse images layers for different images. This can decrease disk usage, and speed up docker build by allowing each step to be cached.

When a new container is created from an image, a writable layer is also created. This layer is called the container layer, and it hosts all changes made to the running container. This layer can store newly written files, modifications to existing files and newly deleted files. The writable layer allows customization of the container. Changes made to the writable layer are saved on that layer. Multiple containers can share the same underlying base image and have their own data state thanks to the writable layer.

The command `docker images` will show all local top level images, their repository and tags, and their size. Intermediate layers are not shown by default.

The SIZE is the cumulative space taken up by the image and all its parent images. This is also the disk space used by the contents of the Tar file created when you docker save an image.

An image will be listed more than once if it has multiple repository names or tags. This single image (identifiable by its matching IMAGE ID) uses up the SIZE listed only once.

-