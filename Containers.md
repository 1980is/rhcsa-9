# Container management

First install the container tools.

``dnf install container-tools``

## Registries

After the install we have "/etc/containers". There we have for example, "registries.conf". Here we can set the registries it uses for images. The line is: "unqualified-search-registries =".

Use ``podman login registry.redhat.io`` to login to Red Hat's registry.
Use ``podman login registry.redhat.io --get-login`` to get your current login credentials.

Users can have their own "registries.conf" file in "~/.config/containers/registries.conf".

Search your registries for an image.
``podman search alpine``

Manage and inspect images no matter where they are.
``skopeo inspect docker://path-to-image``

## Container File

To automate container builds. What we want in our container image.


## General Commands

``podman info``

### List downloaded images
``podman images``

### List running containers
``podman container ps``

### List all containers
``podman container ps -a``
``podman container list –all``

``podman stats``

``podman diff``


## Working with images

### List images
``podman images``
You can also do, ``podman image ls``

### Inspect image
``podman image inspect image-id or image name``

### Remove Image
``podman image rm "imageid"``

### Tag image
``podman image tag nginx:latest nginx:version1``  

### Push image
First you need to tag your image with your username for hub.docker.com and then the repo name.
``podman image tag nginx:latest alibabis/nginx``
The username for Docker Hub is alibabis, and the repo that's created is nginx. Let's push this image.
``podman push 1980is/nginx``

### Image history.
To see the image layers.
``podman image history nginx``

## Working with containers

### Run container
``podman container run -dit --name fedora-v1 fedora``
-d stands for detached mode. -i stands for interactive and -t stands for terminal. --name names the instance, you don't have to provide a name, then Docker will create a random name for the container. Fedora without any tags behind it, e.g., fedora:36, mean that Docker will pull the latest Fedora image, the equivalent of writing fedora:latest.

``podman run -d -p 8080:80 --name nginxtest  nginx:latest``

``podman container run --name webserv2 -d -p 9002:80 nginx``
This runs an nginx container named webserv1 in detached mode on port 9002. To check it out run http://localhost:9002/ in your brow

### Connect to a running container
``podman exec -it fedora-v1 bash``
To disconnect from the container write ``exit``.

### Stop container
``podman container stop fedora-v1``

### Kill container
``podman container kill fedora-v1``
When stopping doesn't work, you can kill the container.

### Remove Container
``podman rm "containerid"``

This command removes **all** stopped containers.
-a stands for all containers. -q returns only the container id.
``podman container ps -aq | xargs docker rm``

## Container Network

``podman network list``
``podman network inspect``
``podman network inspect bridge``


## Storage

### Local persistant volume storage 

In Podman the local volumes are created in the home directory.
``podman volume create myvol``
``podman volume inspect myvol``

### NFS

``podman volume create --driver local --opt type=nfs --opt o=addr=192.168.122.36,rw --opt device=:/nfsdata nfsvol``

Run a container that uses that NFS storage.   
``podman run -it --name voltest2 --rm --mount source=nfsvol,target=/data nginx sh``

## Debug

### Inspect container
``podman container inspect fedora-v1``
See container information. You can use the container name or container id.
``
### View container logs
``podman container logs fedora-v1``