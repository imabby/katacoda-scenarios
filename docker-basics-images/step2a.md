#### Short Overview
A Docker image is like a snapshot of a Virtual Machine.

#### Long Overview


A Docker image includes everything needed to run executable code and is made up of multiple layers. Each layer representing an instruction in the image’s Dockerfile. For example, the Dockerfile below would create three layers. The `FROM` statement creates a layer from the ubuntu image. The `COPY` line add files from your local machine and the `CMD` line specifies what command to run inside the container.

```
FROM ubuntu:latest
COPY . /my-app
CMD sh /my-app/my-app
```

The layers are stacked on top of each other and each layer is only a set of differences from the layer before it. Developers can also reuse images layers for different images. This can decrease disk usage, and speed up `docker build` by allowing each step to be cached.

When a new container is created from an image, a writable layer is also created. This layer is called the container layer, and it hosts all changes made to the running container. This layer can store newly written files, modifications to existing files and newly deleted files. The writable layer allows customization of the container. Changes made to the writable layer are saved on that layer. Multiple containers can share the same underlying base image and have their own data state thanks to the writable layer.