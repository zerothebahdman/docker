# Essential Docker Commands

- To show all running docker containers use `docker ps` || `docker container ls`.
- To run a docker container use `docker run {name of the docker image}:{the version of the docker image}` || `docker run -d {name of the docker image}:{version of the docker image}`
  - Most time we run the `latest` version of the docker image.
  - `-d` flag means you are specify that this container should be detached and run in the background.  

  <br />
- To specify a port to attach a container to use the `-p` and then specifing the port flag when running the container `docker run -d -p 8000:80 {name of the docker image}:{version of the docker image}`
  - _Note:_ You can specify more than one port to attach to a container you want to run `docker run -d -p 8000:80 -p 3000:80 {name of the docker image}:{version of the docker image}`.
