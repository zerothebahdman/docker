# Essential Docker Commands

- To pull a docker image use the `pull` flag i.e `docker pull {image name}:latest`
  - _Note:_ Always use the alpine  version of the docker image cause its light weight and faster to pull. So always check for the alpine version of images and pull them.

  <br>
- To show the list of all docker images `docker images ls`
- To show all running docker containers use `docker ps` || `docker container ls`.
  - `docker ps` shows a list of the running containers.
    - To nicely format the output of output of docker ps use the `-format="ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n"` flag.
    - To shorten this store the value in a variable using this command `export FORMAT="ID\t{{.ID}}\nNAME\t{{.Names}}\nImage\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n"`. Now you can use `docker ps --format=$FORMAT` to show the nicely formatted output.
  
<br />

- To run a docker container use `docker run {name of the docker image}:{the version of the docker image}` || `docker run -d {name of the docker image}:{version of the docker image}`
  - Most time we run the `latest` version of the docker image.
  - `-d` flag means you are specify that this container should be detached and run in the background.  

  <br />
- To specify a port to attach a container to use the `-p` and then specifing the port flag when running the container `docker run -d -p 8000:80 {name of the docker image}:{version of the docker image}`
  - _Note:_ You can specify more than one port to attach to a container you want to run `docker run -d -p 8000:80 -p 3000:80 {name of the docker image}:{version of the docker image}`.

<br />

- To stop a docker container use `docker stop {the container id}` || `docker stop {container name}`
- To delete a container use `docker rm {the container id}`
- To delete a docker image `docker image rm {the image id}`
- To remove all containers from registry use `docker rm $(docker ps -aq)`

  - _Note:_ To forcefully remove a running container use `-f` flag i.e `docker rm -f {docker ps -aq}`.

<br />

- To name a container use the `--name` flag. i.e `docker run --name {what you want to name the container} -d -p 3000:80 {name of the docker image}:{version of the docker image}`

- To share a volume || folder || project with a docker container running on `nginx` for intance you need to use the `-v` flag or command which stringifies volume. first cd into the project directory and run `docker run --name {name you want to call the container} -v $(pwd):/usr/share/nginx/html:ro -d -p 8080:80 nginx:latest`
  - _NB:_ the `$(pwd)` command gives you the current working directory. In this instance its the folder you've cd into.
  - To share volumes between two docker containers, use the `--volume-from` flag for instance `sudo docker run --name divine-copy --volumes-from divine -d -p 3000:80 nginx:latest`
<br />

## Creating a DOCKER file

_Create a cutom docker image A image should contain all the things your application needs to run_

- First create a docker file ```touch Dockerfile``` inside the project you want to dockerize then. Inside this file specify
  - `FROM` => The ```FROM``` instruction initializes a new build stage and sets the Base Image for subsequent instructions. As such, a valid Dockerfile must start with a ```FROM``` instruction. The image can be any valid image – it is especially easy to start by pulling an image from the Public Repositories. for instance use the nodejs offical docker image `node:latest`
  - ```ADD``` => The ADD instruction copies new files, directories or remote file URLs from ```<src>``` and adds them to the filesystem of the image at the path. For instance to add all files || folders in the root directory use double dots ```. .```
  - ```RUN``` => The ```RUN``` instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile. For instance you can instal npm all packages inside the container using the ```RUN``` instruction i.e ```npm install```
  - ```CMD``` => There can only be one ```CMD``` instruction in a ```Dockerfile```. If you list more than one ```CMD``` then only the last ```CMD``` will take effect. The main purpose of a ```CMD``` is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ```ENTRYPOINT``` instruction as well. For instance you can run a nodejs application using the `RUN` instruction i.e `node app.js`.
  
  <br />
- To create a container in docker use the `docker build` commad. To see all available docker build command use `docker build --help`. _NB: always use `-t` or `--tag` flag to add a tag to a container_

## Tags, Versioning ang Tagging

### Tags =>

- To create a tag use the `tag` flag like so `docker tag {from latest version of the docker image} { to version 1.0 of the docker image}` eg `sudo docker tag divine-website:latest divine-website:1.1`

### Versioning =>

- To create a version for a container you need the specify the version when running the container like `docker run --name {name you want to call the container} -d -p 5000:80 {the docker image}:{the version}`. For instance I want to create a new container from an image I have already created, I will run `docker run --name divine-website-v1 -d -p 5000:80 divine-website:1.1`. _NB: `1.1` in this instance is the a tag for this docker image which specifies the version_
