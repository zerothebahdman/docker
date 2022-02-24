# Essential Docker Commands

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
- To remove all containers from registry use `docker rm $(docker ps -aq)`

  - _Note:_ To forcefully remove a running container use `-f` flag i.e `docker rm -f {docker ps -aq}`.

<br />

- To name a container use the `--name` flag. i.e `docker run --name {what you want to name the container} -d -p 3000:80 {name of the docker image}:{version of the docker image}`

- To share a volume || folder || project with a docker container running on `nginx` for intance you need to use the `-v` flag or command which stringifies volume. first cd into the project directory and run `docker run --name {name you want to call the container} -v $(pwd):/usr/share/nginx/html:ro -d -p 8080:80 nginx:latest`
  - _NB:_ the `$(pwd)` command gives you the current working directory. In this instance its the folder you've cd into.
  - To share volumes between two docker containers, use the `--volume-from` flag for instance `sudo docker run --name divine-copy --volumes-from divine -d -p 3000:80 nginx:latest`
<br />