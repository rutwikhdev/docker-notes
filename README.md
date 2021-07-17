# Docker →

- Virtual machines have their own individual OS and also use more cpu, ram, storage.
- Containers are in an isolated of OS environment, they can share the same OS. Use less cpu, ram, storage.
- Images contain the setup code, environment only.
- Containers provide runtime functionality, they are responsible for running.
- docker run image → also pulls the image if it doesn't exist locally.
- when we run `docker run` some interactive shell of the software/image is running inside the container but we might  not have access to it because the environment is isolated and  the interactive shell exposed by the container is not by default exposed to us. Use docker -it run node to do that.
- Every time we run docker run a new container instance spins up

```bash
docker pull nginx # Pulls an image from docker hub
docker run node # Runs a container containing image
docker ps -a # shows all containers(processes) (running and exited)
docker ps # shows only running processes
docker run -it node # expose an iteractive session from inside the container to host machine
docker build . # builds an image based on specified path
docker stop container_name/id
docker run -p 3000:80 container_name # publish localhost:container_expose_port
```

- Dockerfile is instructions to docker engine on how to build an image it doesn't run the container
- Images are read-only type so every time we make a small change to code we have to rebuild the image. The rebuilding is done by taking a snapshot and comparing(layer based). When you rebuild an image only the changes are updated
- Images are closed templates.

- Containers are just an extra thin layer on top of the image
- Image contains everything. You can run multiple containers based on images.
- A container does not copy the code from image, it just creates and extra layer on top of image and allocate resources, memory to run app and so on.
- Container is an isolated unite of software which is based on an image. a running instance of that image.

```bash
docker start container_name # running existing containers -- we're not able to interact with it from local machine but it's started and running
# start runs container in background and run in foreground
# run has attach mode as default and start has detached mode as default
docker start -a container_name # start in attached mode/ run default

# run in detached mode
docker run -p 8000:80 -d container_id
docker attach container_name # attach to container again

docker logs container_name # show the log output in detached mode
docker logs -f container_name # keep on listening / attached mode again
```

- The container needs to be removed first and then only you can remove image

```bash
docker ps -a
docker rm container_name1 container_name2 ....
docker images
docker rmi image_id1 image_id2 ....
docker image prune # removes all unused images by containers
docker run -p 3000:80 -d --rm container_name # remove the container when it stops
# Expose 80 should be same as the port nodeapp is running on
```

- Multiple containers using same image share code hence images are read only.

```bash
docker image inspect image_id
```

```bash
docker build -t rutwik/posts . # build an image based on cur-dir and tag it with name rutwik/posts
docker run rutwik/posts
docker run -it rutwik/posts sh # start a shell in dir instead running npm start
docker exec -it container_id sh # execute a given command in a running container
docker logs container_id # Print out logs from the given container
```

```bash
# REMOVE ALL CONTAINERS AND IMAGES AND DELETE VOLUMES
docker rm -vf $(docker ps -a -q)
docker rmi -f $(docker images -a -q)
```

- Copy code from local directory to already running folder

```bash
docker cp folder_name/. name_of_container:/path_of_folder_to_copy
# . = everything, path_of_folder is created if it doesn't exist.
docker cp name_of_container:/path_of_folder_to_copy
# this command will copy from docker container to local dir
```
