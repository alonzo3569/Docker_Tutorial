## Docker commands

* Start a container
```console
$ docker run [image]
$ docker run -it [image]
#> -i : interactive mode (Allow docker to get usr input)
#> -t : Show stdout in the docker
#> --name : Decide the name of the "container"
#> --entrypoint : Change the entrypoint of the container
```
__Note :__  
1. The container will shut down automatically once there's no service or app running.
```console
$ docker run ubuntu
#> No service or command running, container will shut down immediately

$ docker run ubuntu sleep 5
#> The container will shut down after the command is finished
```
2. Run a container with the nginx:1.14-alpine image and name it webapp
```console
$ docker run --name webapp nginx:1.14-alpine
```

* List containers 
```console
$ docker ps
$ docker ps -a 
#> -a : including non-active container
```

* Stop a container
```console
$ docker stop [container ID/container name]
```

* Remove a container (free disk space)
```console
$ docker rm [container ID/container name]
```

* List images
```console
$ docker images
```

* Remove images : reomver all related containers before removing images
```console
$ docker rmi [image]
```
__Note :__ When removing or stoping containers or images, just input first 3 or 2 letters of container ID will be enough (since all ID should be unique).
```console
$ docker rm 345 e0a 773
```

* Download an image
```console
$ docker pull [image]
```

* Execute a command
```console
$ docker exec [existing image] cat /etc/hosts
```
__Note :__ Difference between `docker run` & `docker exec`


Every container gets a IP by default (Internal IP, only work inside docker)

Map docker host port to container(app) port. Then the user can access web app using docker host IP/docker host port

$ docker run –p [docker host port]:[container port] [image name or exe path]
Ex. $ docker run –p 80:5000 kodekloud/simple-webapp

If you're running docker in VM, open browser in VM and you can access docker web app using internal IP (use docker inspect to checkout internal IP). However, if you want to access web app using browser outside VM, you have to do port mapping first and then use docker host IP(= laptop IP?) + port to access it.
Test : So ideally, if I'm running docker on my linux machine, I can access docker web app using internal IP. 
Ans :  Correct.
$ docker run jenkins
$ docker ps => get port  info and container ID
$ docker inpect [container ID] => get internal IP
$ open browser and input internal IP and port


Volume mapping : import(connect) files into docker
$ docker run –v [path in your device]:[path in docker] [image]
Ex. $ docker run –v /opt/datadir:/var/lib/mysql mysql

Container logs : If you use -d (detach mode) to run your web app in the backend, but some how you want to check the stdout of you web app. Use docker logs.
 
docker attach will take the container back to foreground


* Questions :
Q : How app.sh beome kodekloud/simple-prompt-docker after dockerized?
Q : docker run kodekloud/web-app. Is kodekloud/web-app an image or exe file?
