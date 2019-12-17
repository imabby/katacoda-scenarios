Now we have an image lets run it using the `docker run` command. This command first creates a writeable container layer over the specified image, and then starts it using the specified command.

#### Example image to run
Run the following command: `docker run docker/whalesay cowsay Hello there!`{{execute}}

This should print out the Docker whale ascii image.

*The first time you run an image, the docker looks for it on your local system. If the image isn’t there, then docker will download it from the hub.*

#### Running our python web app image

Run `docker run -p 8000:8000 myimage:mytag`{{execute}}

If all goes well, this should start the image in a new container and print the following:
```
 * Serving Flask app "server" (lazy loading)
 * Environment: production
   WARNING: Do not use the development server in a production environment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://0.0.0.0:8000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 555-356-043
```

You can now view the webpage using the link below:<br>
Render port 8000: https://[[HOST_SUBDOMAIN]]-8000-[[KATACODA_HOST]].environments.katacoda.com/

#### 


