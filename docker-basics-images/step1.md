
### List images

Running the following command will show all local top level images, their repository and tags, and their size. Intermediate layers are not shown by default. The list is ordered by the most recently created images.

```
docker images
```
The SIZE is the cumulative space taken up by the image and all its parent images. This is also the disk space used by the contents of the Tar file created when you docker save an image.

An image will be listed more than once if it has multiple repository names or tags. This single image (identifiable by its matching IMAGE ID) uses up the SIZE listed only once.

### List images by name and tag

The docker images command takes an optional [REPOSITORY[:TAG]] argument that restricts the list to images that match the argument. If you specify REPOSITORYbut no TAG, the docker images command lists all images in the given repository.

For example, to list all images in the "ubuntu" repository, run this command:
```
docker images ubuntu
```

### Formating the output
The formatting option (--format) will pretty print container output using a Go template.
Valid placeholders for the Go template are listed below:

| Placeholder   |      Description      |
|----------|:-------------:|
| .ID |  Image ID |
| .Repository |  Image repository |
| .Tag |  Image tag |
| .Digest |  Image digest |
| .CreatedSince |  Elapsed time since the image was created |
| .CreatedAt |  Time when the image was created |
| .Size |  Image disk size |

When using the --format option, the image command will either output the data exactly as the template declares or, when using the table directive, will include column headers as well.

The following example uses a template without headers and outputs the ID and Repository entries separated by a colon for all images:
```
docker images --format "{{.ID}}: {{.Repository}}"
```

To list all images with their repository and tag in a table format you can use:
```
docker images --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"
```